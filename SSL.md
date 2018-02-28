## Config

    ## remove a mensagem do chrome para certificados inválidos
    chrome://flags/#allow-insecure-localhost

    # self-signed
    openssl req -newkey rsa:2048 -x509 -nodes -keyout server.key -new -out server.crt -subj /CN=localhost -sha256 -days 3650
    
    # self-signed validation
    openssl x509 -in server.crt -noout -text -pubkey
    openssl rsa -in server.key -check -pubout
    openssl rsa -in server.key -pubout
    openssl x509 -noout -modulus -in server.crt| openssl md5
    openssl rsa -noout -modulus -in server.key| openssl md5

    openssl genrsa -des3 -out rootCA.key 2048
    openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem -config sslgen.cnf
    openssl req -sha256 -new -nodes -out server.csr -newkey rsa:2048 -keyout server.key -config sslgen.cnf
    openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 500 -sha256 -extfile sslgen.cnf

    # sslgen.cnf
    [alt_names]
    DNS.1 = localhost

    [req]
    default_bits = 2048
    prompt = no
    default_md = sha256
    distinguished_name = dn

    [dn]
    CN = localhost

    [usr_cert]
    authorityKeyIdentifier=keyid,issuer
    basicConstraints=CA:FALSE
    keyUsage = digitalSignature, keyEncipherment

    [ v3_ca ]
    subjectAltName = @alt_names

## Validation

    ## test
    https://www.ssllabs.com/ssltest/

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
    
