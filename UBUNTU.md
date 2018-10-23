## date/time

    $ sudo timedatectl set-timezone America/Sao_Paulo

## nginx

    source

    $ /etc/apt/sources.list
    deb http://nginx.org/packages/ubuntu/ xenial nginx
    deb-src http://nginx.org/packages/ubuntu/ xenial nginx

    install
    
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

    $ sudo apt-get install chromium
      set the pollInterval to 10000 in node_modules/chrome-launcher.js
      chromeFlags: ['--headless', '--disable-gpu', '--remote-debugging-address=0.0.0.0', '--no-sandbox']
      sudo apt -f install
      sudo rm /var/cache/apt/archives/chromium*
      sudo apt install chromium-browser

## certbot

    https://certbot.eff.org/#ubuntuxenial-nginx

    $ sudo wget -O - https://www.startssl.com/certs/ca.pem https://www.startssl.com/certs/sub.class1.server.ca.pem | sudo tee -a /etc/ssl/ca-certs.pem > /dev/null
    $ sudo apt-get update
    $ sudo apt-get install software-properties-common
    $ sudo add-apt-repository ppa:certbot/certbot
    $ sudo apt-get update
    $ sudo apt-get install certbot
    $ sudo openssl dhparam -out /etc/letsencrypt/dhparam.pem 2048
    
## certbot create

    $ sudo certbot certonly
    $ sudo certbot certonly --webroot -w /var/www/example/ -d www.example.com -d example.com

## certbot renew manual

    $ sudo certbot renew --dry-run

## certbot renew auto

    $ sudo crontab -e
    $ 15 3 * * * /usr/bin/certbot renew --quiet
    
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
    
## Private  Key

```console
ssh-keygen -t rsa -b 4096 -C "your@email.com"

Generating public/private rsa key pair.
Enter file in which to save the key (/home/<your-user>/.ssh/id_rsa):

Created directory '/home/<your-user>/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/<your-user>/.ssh/id_rsa.
Your public key has been saved in /home/<your-user>/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:lXhYzNtK37chmNGsV5/278yr6LrWuUygcYvqklcdtzI my.email@gmail.com
The key's randomart image is:
+---[RSA 4096]----+
|         o.      |
|         +o.     |
|        o +oo    |
|         +oo.o . |
|       .S+oo*.. o|
|       .=E+=.o.+o|
|    . .o .+.o o.+|
|   o ..  .oo.  +.|
|    +o  .o+=...oB|
+----[SHA256]-----+

cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3N...AAAAB3N your@gmail.com
```

