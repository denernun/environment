## date/time

    $ sudo timedatectl set-timezone America/Sao_Paulo

## nginx
    
    install
    
    $ sudo curl -O https://nginx.org/keys/nginx_signing.key && sudo apt-key add ./nginx_signing.key
    $ sudo apt update
    $ sudo apt install nginx
    $ sudo systemctl start nginx
    $ sudo systemctl status nginx

## node

    $ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
    $ sudo apt install -y nodejs
    $ sudo nano ~/.bashrc
    $ export NODE_ENV=[ production | release ]
    $ node -v
    $ npm -v

## pm2

    $ sudo npm install pm2@latest -g
    $ pm2 startup systemd
    $ sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu

## netcore

    $ sudo wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
    $ sudo dpkg -i packages-microsoft-prod.deb
    $ sudo apt-get update
    $ sudo apt-get install apt-transport-https
    $ sudo apt-get update
    $ sudo apt-get install dotnet-sdk-3.1

## netcore service

    /etc/systemd/system/xxx.service
    
    sudo systemctl daemon-reload
    sudo systemctl enable xxx.service
    sudo systemctl status xxx.service
    sudo systemctl start xxx.service
    
    sudo journalctl -fxeu xxx.service

    # service
    
    

## netcore service wsl

    # 
    # /etc/init.d
    # chmod +x <service>
    # sudo update-rc.d <service> defaults
    # ASPNETCORE_ENVIRONMENT=[Development,Release,Production]
    # ASPNETCORE_URLS=[http://*:XXXX]

## chromium

    $ sudo apt install chromium-bsu

## certbot

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

## certbot renew

    $ sudo certbot renew

## validation certificates

    ## test
    https://www.ssllabs.com/ssltest/
    
## resize volume

    $ lsblk
    $ df -h
    $ sudo growpart /dev/xvda 1
    $ sudo resize2fs /dev/xvda1
       

