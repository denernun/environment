## environment
## nginx
```bash
$ sudo nano nginx.sh
$ sudo chmod +x nginx.sh
$ sudo ./nginx.sh

#!/bin/bash

set -e

echo "Atualizando a lista de pacotes..."
sudo apt update

echo "Instalando Nginx..."
sudo apt install nginx -y

echo "Iniciando o serviço Nginx..."
sudo systemctl start nginx

echo "Verificando o status do Nginx..."
sudo systemctl status nginx

echo "Criando a configuração do servidor virtual general.conf..."
cat <<EOF | sudo tee /etc/nginx/general.conf
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header X-Content-Type-Options "nosniff" always;
add_header Referrer-Policy "no-referrer-when-downgrade" always;
add_header Content-Security-Policy "default-src 'self' http: https: data: blob: wss: 'unsafe-inline' 'unsafe-eval'" always;
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;

underscores_in_headers on;
	
location ~ /\.(?!well-known) {
  deny all;
  log_not_found off;
  access_log off;
}
 
location = /favicon.ico {
  log_not_found off;
  access_log off;
}

location = /robots.txt {
  allow all;
  log_not_found off;
  access_log off;
}

location ~* \.(?:css(\.map)?|js(\.map)?|jpe?g|png|gif|ico|cur|heic|webp|tiff?|mp3|m4a|aac|ogg|midi?|wav|mp4|mov|webm|mpe?g|avi|ogv|flv|wmv)$ {
  expires max;
  access_log off;
}

location ~* \.(?:svgz?|ttf|ttc|otf|eot|woff2?)$ {
  add_header Access-Control-Allow-Origin "*";
  expires max;
  access_log off;
}
EOF

cat <<EOF | sudo tee /etc/nginx/options.conf
ssl_session_timeout 1d;
ssl_session_cache shared:SSL:10m;
ssl_session_tickets off;

ssl_dhparam /etc/nginx/dhparam.pem;

ssl_protocols TLSv1.2 TLSv1.3;
ssl_prefer_server_ciphers on;
ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
ssl_ecdh_curve secp384r1;

ssl_stapling on;
ssl_stapling_verify on;

resolver 8.8.8.8 8.8.4.4 valid=60s;
resolver_timeout 2s;
EOF

cat <<EOF | sudo tee /etc/nginx/proxy.conf
proxy_http_version                  1.1;
proxy_cache_bypass                  $http_upgrade;

proxy_set_header Upgrade            $http_upgrade;
proxy_set_header Connection         "upgrade";
proxy_set_header Host               $host;
proxy_set_header X-Real-IP          $remote_addr;
proxy_set_header X-Forwarded-For    $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto  $scheme;
proxy_set_header X-Forwarded-Host   $host;
proxy_set_header X-Forwarded-Port   $server_port;

proxy_redirect                      off;
client_max_body_size                10m;
client_body_buffer_size             128k;
proxy_connect_timeout               90;
proxy_send_timeout                  90;
proxy_read_timeout                  90;
proxy_buffers                       32 4k;
EOF

cat <<EOF | sudo tee /etc/nginx/nginx.conf
user www-data;
pid /run/nginx.pid;
worker_processes auto;
worker_rlimit_nofile 65535;

include /etc/nginx/modules-enabled/*.conf;

events {
  multi_accept on;
  worker_connections 65535;
}

http {

  charset utf-8;
  sendfile on;
  tcp_nopush on;
  types_hash_max_size 2048;
  keepalive_timeout 29;
  client_body_timeout 10;
  client_header_timeout 10;
  send_timeout 10;
  tcp_nodelay on;
  server_tokens off;
  client_max_body_size 16M;
  client_body_buffer_size 16M;

  include /etc/nginx/mime.types;
  default_type application/octet-stream;

  include /etc/nginx/options.conf;

  # -------------------------------------------------------------------
  # LOG FORMAT
  # -------------------------------------------------------------------

  log_format main_ext '$remote_addr - $remote_user [$time_local] "$request" '
  '$status $body_bytes_sent "$http_referer" '
  '"$http_user_agent" "$http_x_forwarded_for" '
  '"$host" sn="$server_name" '
  'rt=$request_time '
  'ua="$upstream_addr" us="$upstream_status" '
  'ut="$upstream_response_time" ul="$upstream_response_length" '
  'cs=$upstream_cache_status bs="$bytes_sent" rl="$request_length" gz="$gzip_ratio" '
  'upt="$upstream_connect_time" uht="$upstream_header_time"  ';

  # -------------------------------------------------------------------
  # LOGS
  # -------------------------------------------------------------------

  access_log /var/log/nginx/access.log main_ext;
  error_log /var/log/nginx/error.log warn;

  # -------------------------------------------------------------------
  # COMPRESSION
  # -------------------------------------------------------------------

  gzip on;
  gzip_vary on;
  gzip_proxied any;
  gzip_comp_level 6;
  gzip_types text/plain text/css text/xml application/json application/javascript application/rss+xml application/atom+xml image/svg+xml;

  # -------------------------------------------------------------------
  # STATUS
  # -------------------------------------------------------------------

  server {
    listen 127.0.0.1:80;
    server_name 127.0.0.1;
    location /stub_status {
      stub_status on;
      access_log off;
      allow 127.0.0.1;
      deny all;
    }
  }

  # -------------------------------------------------------------------
  # CONF
  # -------------------------------------------------------------------
  include /etc/nginx/conf.d/*.conf;
  
}
EOF

echo "Reiniciando o serviço Nginx..."
sudo systemctl reload nginx

exit 0
```
## node
```bash
$ sudo nano node.sh
$ sudo chmod +x node.sh
$ sudo ./node.sh

#!/bin/bash

set -e # Sai do script imediatamente se um comando falhar

NODE_MAJOR=${1:-22} # Usa a versão 22 por padrão, mas permite especificar como argumento

echo "Instalando dependências e configurando o repositório NodeSource para Node.js ${NODE_MAJOR}.x..."

sudo apt update
sudo apt install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_${NODE_MAJOR}.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
sudo apt update && sudo apt upgrade -y
sudo apt install nodejs -y
sudo apt install gcc g++ make -y

echo "Configurando variáveis de ambiente..."
echo "export NODE_ENV=production" | sudo tee -a ~/.bashrc
source ~/.bashrc # Aplica as alterações ao terminal atual

echo "Instalação concluída!"
echo "Node.js versão: $(node -v)"
echo "npm versão: $(npm -v)"

exit 0
```
## pm2
```bash
$ sudo nano pm2.sh
$ sudo chmod +x pm2.sh
$ sudo ./pm2.sh

#!/bin/bash

set -e

echo "Iniciando a instalação e configuração do PM2 e PM2 Logrotate..."

# Instala o PM2 globalmente sem interação
echo "Instalando PM2 globalmente..."
sudo npm install pm2@latest -g --yes

# Instala o plugin PM2 Logrotate sem interação
echo "Instalando o plugin PM2 Logrotate..."
pm2 install pm2-logrotate --silent

# Define a configuração do PM2 Logrotate sem interação
echo "Configurando o PM2 Logrotate..."
pm2 set pm2-logrotate:max_size 10M
pm2 set pm2-logrotate:compress false
pm2 set pm2-logrotate:rotateInterval '* * * 1 0 0'

echo "PM2 e PM2 Logrotate instalados e configurados com sucesso!"
echo "Verifique a configuração com os comandos 'pm2 show pm2-logrotate' e 'pm2 logs'."

exit 0
```
## certbot
```terminal
$ sudo snap install --classic certbot
$ sudo snap set certbot trust-plugin-with-root=ok
$ sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096
```
**wildcard**
```terminal
$ sudo apt update && apt install -y python3-certbot-dns-route53 -y

$ AWS uses permission route53:ChangeResourceRecordSets

$ ~/.aws/credentials:
  [default]
  aws_access_key_id = SEU_ACCESS_KEY_ID
  aws_secret_access_key = SEU_SECRET_ACCESS_KEY

$ ~/.aws/config:
  [default]
  region = sa-east-1

$ sudo certbot --dns-route53 --dns-route53-hosted-zone-id="???" -d "*.domain.com.br" -d "domain.com.br" --agree-tos --server https://acme-v02.api.letsencrypt.org/directory --email denernun@gmail.com
$ sudo certbot certonly --manual -d *.domain.com.br -d domain.com.br --agree-tos --preferred-challenges dns-01 --server https://acme-v02.api.letsencrypt.org/directory
```
**renew**
```terminal
$ renew.sh

#!/bin/bash
# Renova todos os certificados
sudo service nginx stop
sudo certbot renew
sudo service nginx start
# Reinicia o Nginx
sudo systemctl reload nginx

$ crontab -e (todo 1 dia do mes as 3:00 da manha)
# 0 3 1 * * /etc/letsencrypt/renew.sh
```
**validation**
```terminal
$ https://www.ssllabs.com/ssltest/
```
