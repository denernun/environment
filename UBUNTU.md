## environment
```terminal
$ sudo timedatectl set-timezone America/Sao_Paulo

$ sudo nano /etc/environment
  TMPDIR=/tmp
```
## nginx
**install**
```terminal
$ sudo apt update && sudo apt upgrade
$ sudo apt install nginx
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
```terminal
$ sudo apt install python3-setproctitle python3-lockfile python3-daemon python3-greenlet python3-gevent python3-ujson python3-rstr python3-pymysql -y
$ sudo apt install python3-certifi python3-chardet python3-idna python3-netifaces python3-psutil python3-requests python3-urllib3
$ sudo apt install python-psutil-doc python3-openssl python3-socks python-requests-doc
$ sudo apt update & sudo apt upgrade -y
$ curl -L -O https://github.com/nginxinc/nginx-amplify-agent/raw/master/packages/install.sh
$ API_KEY='1145f635a3597c2d0960210ae1efcc1c' sh ./install.sh
$ sudo service amplify-agent start
$ sudo service amplify-agent stop
$ sudo service amplify-agent restart
$ sudo apt update && sudo apt install nginx-amplify-agent
$ sudo nano /etc/amplify-agent/agent.conf
[nginx]
user = www-data
configfile = /etc/nginx/nginx.conf
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
$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
$ sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096
```
**wildcard**
```terminal
sudo certbot certonly --manual -d *.domain.com.br -d domain.com.br --agree-tos --preferred-challenges dns-01 --server https://acme-v02.api.letsencrypt.org/directory
```
**renew**
```terminal
$ sudo certbot renew --dry-run
```
**validation**
```terminal
$ https://www.ssllabs.com/ssltest/
```
