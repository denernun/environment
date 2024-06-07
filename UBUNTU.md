## environment
```terminal
$ sudo nano /etc/environment
  TMPDIR=/tmp
```
## nginx
**install**
```terminal
$ sudo apt update && sudo apt upgrade
$ sudo apt install nginx php-fpm php-mysql
$ sudo systemctl start nginx
$ sudo systemctl status nginx
```
## node
```terminal
$ sudo apt install -y ca-certificates curl gnupg
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
$ NODE_MAJOR=20
$ echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
$ sudo apt update
$ sudo apt install -y nodejs
$ sudo apt install gcc g++ make -y
$ sudo nano ~/.bashrc
$ export NODE_ENV=[ production | release ]
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
## amplify
**install**
```terminal
$ sudo apt install build-essential libssl-dev libffi-dev zlib1g-dev
$ wget https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tgz
$ tar -xvf Python-2.7.18.tgz
$ cd Python-2.7.18
$ ./configure
  make
  sudo make install
$ curl -fsSL http://nginx.org/keys/nginx_signing.key | sudo gpg --dearmor -o /etc/apt/keyrings/nginx_signing.key
$ sudo apt update & sudo apt upgrade -y
$ curl -L -O https://github.com/nginxinc/nginx-amplify-agent/raw/master/packages/install.sh
$ API_KEY='1145f635a3597c2d0960210ae1efcc1c' sh ./install.sh
```
**config**
```terminal
$ sudo nano /etc/amplify-agent/agent.conf
[nginx]
user = www-data
configfile = /etc/nginx/nginx.conf
```
**update**
```terminal
$ sudo apt update && sudo apt install nginx-amplify-agent
```
**service**
```terminal
$ sudo service amplify-agent start
$ sudo service amplify-agent stop
$ sudo service amplify-agent restart
```
## certbot
**site**
```terminal
$ https://certbot.eff.org/lets-encrypt/ubuntufocal-nginx
```
**install**
```terminal
$ sudo apt remove certbot
$ sudo apt update && sudo apt upgrade -y
$ sudo snap install core
$ sudo snap refresh core
$ sudo snap install --classic certbot
$ sudo snap set certbot trust-plugin-with-root=ok
$ sudo snap install certbot-dns-route53
$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
$ sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096
```
**wildcard**
```terminal
$ sudo apt install python3-certbot-dns-route53
$ sudo nano ~/.aws/credentials
  [default]
  aws_access_key_id = YOUR_ACCESS_KEY_ID
  aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
$ sudo chmod 600 ~/.aws/credentials
$ sudo certbot certonly --dns-route53 -d '*.domain.com.br' -m denernun@gmail.com --agree-tos --server https://acme-v02.api.letsencrypt.org/directory
```
**renew**
```terminal
$ sudo certbot renew --dry-run

$ sudo certbot renew --dns-route53 --dry-run
$ sudo crontab -e
  0 0,12 * * * /usr/bin/certbot renew --quiet --dns-route53 >> /var/log/letsencrypt/renew.log 2>&1
```
**validation**
```terminal
$ https://www.ssllabs.com/ssltest/
```
**root**
```terminal
$ sudo adduser ubuntu
$ sudo usermod -aG sudo ubuntu
$ sudo apt update
$ sudo mkdir -p ~ubuntu/.ssh
$ sudo cp ~administrador/.ssh/authorized_keys ~ubuntu/.ssh/
$ sudo chown -R ubuntu:ubuntu ~ubuntu/.ssh
```
