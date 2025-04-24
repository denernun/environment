## environment
```terminal
$ sudo nano /etc/environment
  TMPDIR=/tmp
```
## nginx
**install**
```terminal
$ sudo apt update && sudo apt upgrade -y
$ sudo apt install nginx
$ sudo systemctl start nginx
$ sudo systemctl status nginx

$ sudo add-apt-repository ppa:ondrej/nginx
$ sudo apt update && sudo apt upgrade -y
$ sudo apt install php7.4 php7.4-fpm php7.4-common php7.4-mysql php7.4-cli php7.4-curl php7.4-json php7.4-cgi php7.4-mbstring php7.4-xml php7.4-zip -y
$ sudo systemctl start php7.4-fpm
$ sudo systemctl enable php7.4-fpm
```
## node
```terminal
$ sudo apt install -y ca-certificates curl gnupg
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
$ NODE_MAJOR=22
$ echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
$ sudo apt update && sudo apt upgrade
$ sudo apt install -y nodejs
$ sudo apt install gcc g++ make -y
$ sudo nano ~/.bashrc
$ export NODE_ENV=production
$ node -v
$ npm -v
```
## pm2
```terminal
$ sudo npm install pm2@latest -g
$ pm2 install pm2-logrotate
$ pm2 set pm2-logrotate:max_size 10M
$ pm2 set pm2-logrotate:compress false
$ pm2 set pm2-logrotate:rotateInterval '* * * 1 0 0'
```
## certbot
**site**
```terminal
$ https://certbot.eff.org/lets-encrypt
```
**install**
```terminal
$ sudo snap install --classic certbot
$ sudo snap set certbot trust-plugin-with-root=ok
$ sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096
```
**wildcard**
```terminal
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
