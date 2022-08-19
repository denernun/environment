## environment
```terminal
$ sudo timedatectl set-timezone America/Sao_Paulo

$ sudo nano /etc/environment
  TMPDIR=/tmp
```
## nginx
**install**
```terminal
$ sudo curl -O https://nginx.org/keys/nginx_signing.key && sudo apt-key add ./nginx_signing.key
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install nginx
$ sudo systemctl start nginx
$ sudo systemctl status nginx
```
## node
```terminal
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install gcc g++ make
$ curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
$ sudo apt install -y nodejs
$ sudo nano ~/.bashrc
$ export NODE_ENV=[ production | release ]
$ node -v
$ npm -v
```
## pm2
```terminal
$ sudo npm install pm2@latest -g
$ pm2 startup systemd
$ sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
$ pm2 install pm2-logrotate
$ pm2 set pm2-logrotate:max_size 10M
$ pm2 set pm2-logrotate:compress false
$ pm2 set pm2-logrotate:rotateInterval '* * * 1 * *'
```
## amplify
```terminal
$ sudo apt-get install python2.7
$ sudo nano /etc/apt/sources.list.d/nginx-amplify.list
  deb [arch=amd64] https://packages.amplify.nginx.com/py3/ubuntu focal amplify-agent
$ sudo apt-get install python3-setproctitle python3-lockfile python3-daemon python3-greenlet python3-gevent python3-ujson python3-rstr python3-pymysql  
$ sudo apt update
$ sudo apt upgrade
$ curl -L -O https://github.com/nginxinc/nginx-amplify-agent/raw/master/packages/install.sh
$ nano install.sh
  test -d /etc/apt/sources.list.d && \
  ${sudo_cmd} test -w /etc/apt/sources.list.d && \
  ${sudo_cmd} rm -f /etc/apt/sources.list.d/amplify-agent.list && \
  ${sudo_cmd} rm -f /etc/apt/sources.list.d/nginx-amplify.list && \
  echo "deb [arch=amd64] https://packages.amplify.nginx.com/py3/ubuntu focal amplify-agent" | \
  ${sudo_cmd} tee /etc/apt/sources.list.d/nginx-amplify.list > /dev/null 2>&1 && \
  ${sudo_cmd} chmod 644 /etc/apt/sources.list.d/nginx-amplify.list > /dev/null 2>&1
$ API_KEY='1145f635a3597c2d0960210ae1efcc1c' sh ./install.sh
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
$ sudo apt-get remove certbot
$ sudo apt update
$ sudo apt upgrade
$ sudo snap install core
$ sudo snap refresh core
$ sudo snap install --classic certbot
$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
$ sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096
```
**renew**
```terminal
$ sudo certbot renew --dry-run
```
**validation**
```terminal
$ https://www.ssllabs.com/ssltest/
```
## chromium
```terminal
$ sudo apt install chromium-bsu
```
## resize volume
```terminal
$ lsblk
$ df -h
$ sudo growpart /dev/xvda 1
$ sudo resize2fs /dev/xvda1
```       

