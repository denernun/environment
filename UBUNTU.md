## date/time
```terminal
$ sudo timedatectl set-timezone America/Sao_Paulo
$ sudo nano /etc/environment TMPDIR=/tmp
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
$ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
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
## netcore
**sdk**
```terminal
$ sudo wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
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
[site certbot](https://certbot.eff.org/#ubuntuxenial-nginx)
```
**install**
```terminal
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository universe
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt update
$ sudo apt-get install certbot python-certbot-nginx
$ sudo openssl dhparam -out /etc/nginx/dhparam.pem 2048
```
**renew**
```terminal
$ sudo certbot renew
```
**validation**

[ssllabs](https://www.ssllabs.com/ssltest/)

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

