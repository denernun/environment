## comands
**windows**
```terminal
@echo off
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem -config cert.cnf
echo adicione o rootCA.pem no Certificates/Current User/Personal
@pause
openssl req -new -sha256 -nodes -out localhost.csr -newkey rsa:2048 -keyout localhost.key -config cert.cnf
openssl x509 -req -in localhost.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out localhost.crt -days 500 -sha256 -extfile cert.ext
del rootCA.srl
del localhost.csr
```
**linux**
```terminal
#/bin/sh
sudo openssl dhparam -out /etc/nginx/dhparam.pem 2048
sudo openssl genrsa -des3 -out rootCA.key 2048
sudo openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem -config cert.cnf
sudo openssl req -new -sha256 -nodes -out localhost.csr -newkey rsa:2048 -keyout localhost.key -config cert.cnf
sudo openssl x509 -req -in localhost.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out localhost.crt -days 500 -sha256 -extfile cert.ext
sudo rm localhost.csr
sudo rm rootCA.srl
```
**cert.cnf**
```terminal
[req]
deafault_bits = 2048
prompt = no
default_md = sha256
distinguished_name = dn

[dn]
C=BR
ST=Sao Paulo
L=Maua
O=Dener Rocha
OU=Dener Rocha
CN=localhost
emailAddress=denernun@gmail.com
```
**cert.ext**
```terminal
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
```
## import
```terminal
Certificates/Personal/Certificates/*.pfx

Certificates/Current User/Personal/Certificates/rootCA.pem
Certificates/Current User/Personal/Certificates/localhost.pem

Certificates/Current User/Trusted Root/Certificates/rootCA.pem
Certificates/Current User/Trusted Root/Certificates/localhost.pem
```
## keys
```terminal
ssh-keygen -t rsa -b 4096 -C ubuntu

Generating public/private rsa key pair.
Enter file in which to save the key (/home/<your-user>/.ssh/id_rsa):

Private Key: /home/<your-user>/.ssh/id_rsa.
Public key: /home/<your-user>/.ssh/id_rsa.pub.

cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3N...AAAAB3N ubuntu authorized_keys
```
## firefox
```terminal
Browse to about:config
Search for “network.stricttransportsecurity.preloadlist”.
Set it to false.
```
## chrome
```terminal
chrome://flags/#allow-insecure-localhost
cors --disable-web-security --user-data-dir="C:/Users/Public/Chrome"
debug --remote-debugging-port=9222
```
## netcore
```terminal
dotnet dev-certs https --help
dotnet dev-certs https --trust
```

**links**\
[developing locally with netcore under https ssl and self-signed certs](https://www.hanselman.com/blog/DevelopingLocallyWithASPNETCoreUnderHTTPSSSLAndSelfSignedCerts.aspx\)\
[how to get https working on your local development environment in 5 minutes](https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec/)\
[how to trust the iis express self-signed certificate](https://blogs.msdn.microsoft.com/robert_mcmurray/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate/)\
