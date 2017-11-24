## config

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

        add_header Strict-Transport-Security "max-age=15768000" always;
        add_header Strict-Transport-Security "max-age=15768000; includeSubDomains" always;

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        gzip on;
        gzip_disable "msie6";
        gzip_vary on;
        gzip_comp_level 6;
        gzip_buffers 16 8k;
        gzip_min_length 1000;
        gzip_proxied expired no-cache no-store private auth;
        gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml text/javascript application/vnd.ms-fontobject application/x-font-ttf image/svg+xml;

## html

    # www
    server {

        listen 80;
        listen [::]:80;

        listen 443 ssl http2;
        listen [::]:443 ssl http2;

        root /var/www/html;
        index index.html;
        server_name www.domain.com;

        location / {
            try_files $uri $uri/ =404;
        }

        ssl_certificate /etc/letsencrypt/live/www.domain.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/www.domain.com/privkey.pem;
        ssl_dhparam /etc/letsencrypt/dhparam.pem;

        ssl_stapling on;
        ssl_stapling_verify on;
        ssl_trusted_certificate /etc/ssl/ca-certs.pem;

        if ($scheme != "https") {
                return 301 https://$server_name$request_uri;
        }

    }

## node

    server {

        listen 80;
        listen [::]:80;

        listen 443 ssl http2;
        listen [::]:443 ssl http2;

        server_name api.domain.com;

        ssl_certificate /etc/letsencrypt/live/api.domain.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/api.domain.com/privkey.pem;
        ssl_dhparam /etc/letsencrypt/dhparam.pem;

        ssl_stapling on;
        ssl_stapling_verify on;
        ssl_trusted_certificate /etc/ssl/ca-certs.pem;

        location / {
                proxy_pass https://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
        }

    }
