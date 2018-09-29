## date/time

    $ sudo timedatectl set-timezone America/Sao_Paulo

## nginx

    source
    deb http://nginx.org/packages/ubuntu/ xenial nginx
    deb-src http://nginx.org/packages/ubuntu/ xenial nginx

    install
    
    $ /etc/apt/sources.list
    $ sudo curl -O https://nginx.org/keys/nginx_signing.key && sudo apt-key add ./nginx_signing.key
    $ sudo apt-get update
    $ sudo apt-get install nginx
    $ sudo systemctl start nginx
    $ sudo systemctl status nginx
    
    update
    
    $ /etc/apt/sources.list
    $ /etc/nginx
    $ sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
    $ sudo apt-get remove nginx nginx-common nginx-full nginx-core
    $ sudo apt-get update
    $ sudo apt-get install nginx
    $ sudo systemctl unmask nginx
    $ sudo systemctl start nginx
    $ sudo systemctl enable nginx
    $ sudo systemctl status nginx

## node

    $ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    $ sudo apt-get install -y nodejs
    $ sudo vi ~/.bashrc
    $ export NODE_ENV=[ production | release ]
    $ node -v
    $ npm -v

## pm2

    $ sudo npm install pm2@latest -g
    $ pm2 startup systemd
    $ sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu

## php

    $ sudo apt-get install php7.0 php7.0-mcrypt
    $ sudo nano /etc/php/7.0/fpm/php.ini
      cgi.fix_pathinfo=0
    $ sudo service php7-fpm restart

## chromium

    $ sudo apt-get install chromium-bsu

## certbot

    https://certbot.eff.org/#ubuntuxenial-nginx

    $ sudo wget -O - https://www.startssl.com/certs/ca.pem https://www.startssl.com/certs/sub.class1.server.ca.pem | sudo tee -a /etc/ssl/ca-certs.pem > /dev/null
    $ sudo apt-get update
    $ sudo apt-get install software-properties-common
    $ sudo add-apt-repository ppa:certbot/certbot
    $ sudo apt-get update
    $ sudo apt-get install certbot
    $ sudo openssl dhparam -out /etc/letsencrypt/dhparam.pem 2048
    
    

