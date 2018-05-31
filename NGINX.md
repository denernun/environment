## config

```
user www-data;
worker_processes auto;
pid /run/nginx.pid;

events {
    worker_connections 768;
    multi_accept on;
}

http {

    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;

    include /etc/nginx/mime.types;
    default_type application/octet-stream;

	include /etc/letsencrypt/options-ssl-nginx.conf;

	add_header Strict-Transport-Security "max-age=15768000; includeSubDomains" always;
    add_header X-Frame-Options DENY;

	log_format main_ext '$remote_addr - $remote_user [$time_local] "$request" '
						'$status $body_bytes_sent "$http_referer" '
						'"$http_user_agent" "$http_x_forwarded_for" '
						'"$host" sn="$server_name" '
						'rt=$request_time '
						'ua="$upstream_addr" us="$upstream_status" '
						'ut="$upstream_response_time" ul="$upstream_response_length" '
						'cs=$upstream_cache_status' ;

	access_log /var/log/nginx/access.log main_ext;
	error_log /var/log/nginx/error.log warn;

	gzip on;
	gzip_disable "msie6";
	gzip_vary on;
	gzip_proxied any;
	gzip_comp_level 6;
	gzip_buffers 16 8k;
	gzip_http_version 1.1;
	gzip_min_length 256;
	gzip_types
			text/plain
			text/css
			text/javascript
			application/json
			application/javascript
			application/x-javascript
			text/xml
			application/xml
			application/xml+rss
			application/vnd.ms-fontobject
			application/x-font-ttf
			image/svg+xml
			font/opentype
			image/x-icon;

    # -------------------------------------------------------------------
    # METRICS
    # -------------------------------------------------------------------

	server {

		listen 127.0.0.1:80;
		server_name 127.0.0.1;

		location /nginx_status {
			stub_status on;
			allow 127.0.0.1;
			deny all;
		}

	}

    # -------------------------------------------------------------------
    # WWW
    # -------------------------------------------------------------------

    server {

        listen 80;
		listen [::]:80;

        server_name host.domain;

        return 301 https://$host$request_uri;

    }

    server {

        listen 443 ssl http2;
		listen [::]:443 ssl http2;

        root /var/www/domain;
        index index.html;
        server_name host.domain;

        location / {
            try_files $uri $uri/ /index.html;
        }

		ssl_certificate /etc/letsencrypt/live/domain/fullchain.pem;
		ssl_certificate_key /etc/letsencrypt/live/domain/privkey.pem;
		ssl_dhparam /etc/letsencrypt/dhparam.pem;
		ssl_stapling on;
		ssl_stapling_verify on;

    }

    # -------------------------------------------------------------------
    # API
    # -------------------------------------------------------------------

	server {

        listen 80;
		listen [::]:80;

		server_name host.domain;

        return 301 https://$host$request_uri;

	}

	server {

		listen 443 ssl http2;
		listen [::]:443 ssl http2;

		server_name host.domain;

		ssl_certificate /etc/letsencrypt/live/domain/fullchain.pem;
		ssl_certificate_key /etc/letsencrypt/live/domain/privkey.pem;
		ssl_dhparam /etc/letsencrypt/dhparam.pem;
		ssl_stapling on;
		ssl_stapling_verify on;

        location / {
                proxy_pass https://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
        }

	}

}
```
    
## google pagespeed

https://www.modpagespeed.com/doc/build_ngx_pagespeed_from_source
https://www.modpagespeed.com/doc/configuration
    

    

    
