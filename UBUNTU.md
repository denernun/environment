## date/time

    $ sudo timedatectl set-timezone America/Sao_Paulo

## nginx

    source

    $ sudo nano /etc/apt/sources.list
    deb http://nginx.org/packages/ubuntu/ xenial nginx
    deb-src http://nginx.org/packages/ubuntu/ xenial nginx

    install
    
    $ sudo curl -O https://nginx.org/keys/nginx_signing.key && sudo apt-key add ./nginx_signing.key
    $ sudo apt update
    $ sudo apt install nginx
    $ sudo systemctl start nginx
    $ sudo systemctl status nginx
    
    update
    
    $ sudo nano /etc/apt/sources.list
    $ cd /etc/nginx
    $ sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
    $ sudo apt remove nginx nginx-common nginx-full nginx-core
    $ sudo apt update
    $ sudo apt install nginx
    $ sudo systemctl unmask nginx
    $ sudo systemctl start nginx
    $ sudo systemctl enable nginx
    $ sudo systemctl status nginx
    
    folder
    
    $ sudo mkdir /var/www
    $ sudo chown ubuntu:root /var/www

## node

    $ curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
    $ sudo apt install -y nodejs
    $ sudo nano ~/.bashrc
    $ export NODE_ENV=[ production | release ]
    $ node -v
    $ npm -v

## pm2

    $ sudo npm install pm2@latest -g
    $ pm2 startup systemd
    $ sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu

## php

    $ sudo apt install php7.0 php7.0-mcrypt
    $ sudo nano /etc/php/7.0/fpm/php.ini
    # cgi.fix_pathinfo=0
    $ sudo service php7-fpm restart

## chromium

    $ sudo apt install chromium-bsu

## certbot

    site
    
    https://certbot.eff.org/#ubuntuxenial-nginx

    install
        
    $ sudo apt update
    $ sudo apt install software-properties-common
    $ sudo add-apt-repository ppa:certbot/certbot
    $ sudo apt update
    $ sudo apt install certbot
    $ sudo openssl dhparam -out /etc/letsencrypt/dhparam.pem 4096

## certbot renew manual

    $ sudo certbot renew --dry-run

## certbot renew auto

    $ sudo crontab -e
    $ 15 3 * * * /usr/bin/certbot renew --quiet

## validation certificates

    ## test
    https://www.ssllabs.com/ssltest/
    
## keys

    $ ssh-keygen -t rsa -b 4096 -C ubuntu

    # Generating public/private rsa key pair.
    # Enter file in which to save the key (/home/<your-user>/.ssh/id_rsa):

    # Private Key: /home/<your-user>/.ssh/id_rsa.
    # Public key: /home/<your-user>/.ssh/id_rsa.pub.

    # cat ~/.ssh/id_rsa.pub
    # ssh-rsa AAAAB3N...AAAAB3N ubuntu
