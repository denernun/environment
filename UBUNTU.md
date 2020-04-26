## date/time
```text
$ sudo timedatectl set-timezone America/Sao_Paulo
```
## nginx
```text    
install

$ sudo curl -O https://nginx.org/keys/nginx_signing.key && sudo apt-key add ./nginx_signing.key
$ sudo apt update
$ sudo apt install nginx
$ sudo systemctl start nginx
$ sudo systemctl status nginx
```
## node
```text
$ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
$ sudo apt install -y nodejs
$ sudo nano ~/.bashrc
$ export NODE_ENV=[ production | release ]
$ node -v
$ npm -v
```
## pm2
```text
$ sudo npm install pm2@latest -g
$ pm2 startup systemd
$ sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
```
## netcore
```text
$ sudo wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
$ sudo dpkg -i packages-microsoft-prod.deb
$ sudo apt-get update
$ sudo apt-get install apt-transport-https
$ sudo apt-get update
$ sudo apt-get install dotnet-sdk-3.1
```
## netcore service
```text
/etc/systemd/system/xxx.service

sudo systemctl daemon-reload
sudo systemctl enable xxx.service
sudo systemctl status xxx.service
sudo systemctl start xxx.service

sudo journalctl -fxeu xxx.service

# service

[Unit]
Description=xxx

[Service]
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
## netcore service wsl
```text
# 
# /etc/init.d
# chmod +x <service>
# sudo update-rc.d <service> defaults
# ASPNETCORE_ENVIRONMENT=[Development,Release,Production]
# ASPNETCORE_URLS=[http://*:XXXX]
```
## chromium
```text
$ sudo apt install chromium-bsu
```
## certbot
```text
site

https://certbot.eff.org/#ubuntuxenial-nginx

install

$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository universe
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt update
$ sudo apt-get install certbot python-certbot-nginx
$ sudo openssl dhparam -out /etc/nginx/dhparam.pem 2048
```
## certbot renew
```text
$ sudo certbot renew
```
## certbot validation
```text
https://www.ssllabs.com/ssltest/
```    
## resize volume
```text
$ lsblk
$ df -h
$ sudo growpart /dev/xvda 1
$ sudo resize2fs /dev/xvda1
```       

