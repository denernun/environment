## date/time
```terminal
$ sudo timedatectl set-timezone America/Sao_Paulo
```
## environment
```terminal
$ sudo nano /etc/environment
  TMPDIR=/tmp
```
## nginx
**install**
```terminal
$ sudo curl -O https://nginx.org/keys/nginx_signing.key && sudo apt-key add ./nginx_signing.key
$ sudo apt update
$ sudo apt install nginx
$ sudo systemctl start nginx
$ sudo systemctl status nginx
```
**remove**
```terminal
$ sudo update-rc.d -f nginx remove
$ sudo rm /etc/init.d/nginx
$ sudo apt-get purge nginx nginx-common
$ sudo apt-get remove nginx-core nginx-full nginx-light nginx-extras nginx-naxsi nginx-common
```
**modules**
```terminal
50-mod-http-geoip.conf
50-mod-http-image-filter.conf
50-mod-http-xslt-filter.conf
50-mod-mail.conf
50-mod-stream.conf
```
## node
```terminal
$ sudo apt-get install gcc g++ make
$ curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
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
```
## amplify
```terminal
$ sudo nano /etc/apt/sources.list.d/nginx-amplify.list
  deb [arch=amd64] https://packages.amplify.nginx.com/py3/ubuntu focal amplify-agent
$ sudo apt-get install python3-setproctitle python3-lockfile python3-daemon python3-greenlet python3-gevent python3-ujson python3-rstr python3-pymysql
$ sudo apt-get update && sudo apt-get install nginx-amplify-agent
$ sudo cp /etc/amplify-agent/agent.conf.default /etc/amplify-agent/agent.conf
$ sudo service amplify-agent start
$ sudo service amplify-agent stop
$ sudo service amplify-agent restart
```
## netcore
**sdk**
```terminal
$ sudo wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
$ sudo dpkg -i packages-microsoft-prod.deb
$ sudo apt-get update
$ sudo apt-get install apt-transport-https
$ sudo apt-get update
$ sudo apt-get install dotnet-sdk-3.1
```
**service systemd**
```terminal
[Unit]
Description=xxx

[Service]
#Type=notify (only service worker)
WorkingDirectory=/var/www/xxx
ExecStart=/usr/bin/dotnet /var/www/xxx/xxx.dll
Restart=always
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=xxx
User=ubuntu
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=ASPNETCORE_URLS=http://localhost:5001
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target    
```
**service systemd install**
```terminal
/etc/systemd/system/xxx.service
sudo systemctl daemon-reload
sudo systemctl enable xxx.service
sudo journalctl -fxeu xxx.service
```
**service wsl**
```terminal
# /etc/init.d
# chmod +x <service>
# sudo update-rc.d <service> defaults
# ASPNETCORE_ENVIRONMENT=[Development,Release,Production]
# ASPNETCORE_URLS=[http://*:XXXX]
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
$ sudo snap install core
$ sudo snap refresh core
$ sudo snap install --classic certbot
$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
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

