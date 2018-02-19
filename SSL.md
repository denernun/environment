## Config

    ## remove a mensagem do chrome para certificados inválidos
    chrome://flags/#allow-insecure-localhost

    # sslgen.bat
    @echo off
    openssl genrsa -des3 -out rootCA.key 2048
    openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem
    openssl req -new -sha256 -nodes -out server.csr -newkey rsa:2048 -keyout server.key -config sslgen.cnf
    openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 500 -sha256 -extfile sslgen.ext
    
    # sslgen.cnf
    [alt_names]
    DNS.1 = localhost
        
    [req]
    default_bits = 2048
    prompt = no
    default_md = sha256
    distinguished_name = dn

    [dn]
    C=BR
    ST=Sao Paulo
    L=Maua
    O=Denernun
    OU=Denernun
    emailAddress=denernun@gmail.com
    CN = localhost

    # sslgen.ext
    authorityKeyIdentifier=keyid,issuer
    basicConstraints=CA:FALSE
    keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
    subjectAltName = @alt_names

## Validation

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
    $ sudo certbot certonly --webroot -w /var/www/example/ -d www.example.com -d example.com

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

