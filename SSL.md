## self-signed
**windows**
```bash
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem -config cert.cnf
# add rootCA.pem do certificates trusted
openssl req -new -sha256 -nodes -out localhost.csr -newkey rsa:2048 -keyout localhost.key -config cert.cnf
openssl x509 -req -in localhost.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out localhost.crt -days 500 -sha256 -extfile cert.ext
```
**linux**
```bash
sudo openssl dhparam -out /etc/nginx/dhparam.pem 2048
sudo openssl genrsa -des3 -out rootCA.key 2048
sudo openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem -config cert.cnf
# add rootCA.pem do certificates trusted
sudo openssl req -new -sha256 -nodes -out localhost.csr -newkey rsa:2048 -keyout localhost.key -config cert.cnf
sudo openssl x509 -req -in localhost.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out localhost.crt -days 500 -sha256 -extfile cert.ext
```
**cert.cnf**
```bash
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
```bash
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
```
## import
```bash
Certificates/Current User/Personal/Certificates/rootCA.pem
Certificates/Current User/Trusted Root/Certificates/rootCA.pem
```
## keys
```bash
ssh-keygen -t rsa -b 4096 -C "denernun@gmail.com"

Generating public/private rsa key pair.
Enter file in which to save the key (~/.ssh/id_rsa):

Private Key: ~/.ssh/id_rsa.
Public key: ~/.ssh/id_rsa.pub.

cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3N...AAAAB3N ubuntu authorized_keys

puttygen
```
## firefox
```text
about:config
network.stricttransportsecurity.preloadlist=false
```
## chrome
```text
chrome://flags/#allow-insecure-localhost
cors --disable-web-security --user-data-dir="C:/Users/Public/Chrome"
debug --remote-debugging-port=9222
```
## netcore
```text
dotnet dev-certs https --help
dotnet dev-certs https --trust
```
###### links
[https://www.hanselman.com/blog/DevelopingLocallyWithASPNETCoreUnderHTTPSSSLAndSelfSignedCerts.aspx](https://www.hanselman.com/blog/DevelopingLocallyWithASPNETCoreUnderHTTPSSSLAndSelfSignedCerts.aspx)\
[https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec](https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec)\
[https://blogs.msdn.microsoft.com/robert_mcmurray/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate](https://blogs.msdn.microsoft.com/robert_mcmurray/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate)
