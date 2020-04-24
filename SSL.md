**links**

[How to get HTTPS working on your local development environment in 5 minutes](https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec/)

[How to trust the IIS Express Self-Signed Certificate](https://blogs.msdn.microsoft.com/robert_mcmurray/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate/)

**comands**
```terminal
openssl dhparam -out /etc/nginx/dhparam.pem 4096
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem
openssl req -new -sha256 -nodes -out localhost.csr -newkey rsa:2048 -keyout localhost.key -config cert.cnf
openssl x509 -req -in localhost.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out localhost.crt -days 500 -sha256 -extfile cert.ext

import the rootCA.pem to certicate local computer and certificate user personal and trusted root
import the localhost.pem to certicate local computer and certificate user personal and trusted root
```

**import**
```terminal
Certificates/Current User/Personal/Certificates/rootCA.pem
Certificates/Current User/Trusted Root/Certificates/rootCA.pem
Certificates/Local Computer/Personal/Certificates/rootCA.pem
Certificates/Local Computer/Trusted Root/Certificates/rootCA.pem

Certificates/Current User/Trusted Root/Certificates/localhost.pem
Certificates/Local Computer/Trusted Root/Certificates/localhost.pem
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

**firefox**
```
Browse to about:config
Search for “network.stricttransportsecurity.preloadlist”.
Set it to false.
```

**chrome**
```
chrome://flags/#allow-insecure-localhost
cors --disable-web-security --user-data-dir="C:/Users/Public/Chrome"
debug --remote-debugging-port=9222
```
