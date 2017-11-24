## config

    $ sudo timedatectl set-timezone America/Sao_Paulo

## nginx

    $ sudo apt-get update
    $ sudo apt-get install nginx

    $ sudo mkdir /var/www/html
    $ sudo chown ubuntu -R /var/www/html

## node

    $ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    $ sudo apt-get install -y nodejs
    $ sudo vi ~/.bashrc
    $ export NODE_ENV=[ production | release ]
    $ node -v
    $ npm -v

## PM2

    $ sudo npm install pm2@latest -g
    $ pm2 startup systemd
    $ sudo env PATH=$PATH:/usr/bin /usr/local/lib/node_modules/pm2/bin/pm2 startup upstart -u ubuntu --hp /home/ubuntu

