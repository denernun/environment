## Config

    ## remove a mensagem do chrome para certificados inválidos
    chrome://flags/#allow-insecure-localhost

    ## cria um certificado sem senha para o localhost
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout privkey.pem -out fullchain.pem -subj /CN=localhost

    ## adicionar o certificado no chrome
    copy begin/end certificate, paste in server.crt and import on chrome manager certificates trust root

    ## test
    https://www.ssllabs.com/index.html

## Install

    https://certbot.eff.org/#ubuntuxenial-nginx

    $ sudo wget -O - https://www.startssl.com/certs/ca.pem https://www.startssl.com/certs/sub.class1.server.ca.pem | sudo tee -a /etc/ssl/ca-certs.pem > /dev/null
    $ sudo apt-get update
    $ sudo apt-get install software-properties-common
    $ sudo add-apt-repository ppa:certbot/certbot
    $ sudo apt-get update
    $ sudo apt-get install certbot
    $ sudo openssl dhparam -out /etc/letsencrypt/dhparam.pem 2048

## Create

    $ sudo certbot certonly

## Renew Manual

    $ sudo certbot renew --dry-run

## Renew Auto

    $ sudo crontab -e
    $ 15 3 * * * /usr/bin/certbot renew --quiet

## Update

    update.sh

    #/bin/sh
    sudo systemctl stop nginx.service
    sudo /usr/bin/certbot renew --quiet
    sudo systemctl start nginx.service
    sudo pm2 stop api
    sudo cp /etc/letsencrypt/live/domain/fullchain.pem /var/www/api/certs
    sudo cp /etc/letsencrypt/live/domain/privkey.pem /var/www/api/certs
    sudo pm2 start api
