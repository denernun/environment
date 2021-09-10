## self-signed
**create**
```terminal
$env:RANDFILE=".rnd"
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1095 -out rootCA.pem -config cert.cnf -reqexts v3_req -extensions v3_ca
openssl req -new -sha256 -nodes -newkey rsa:2048 -out localhost.csr -keyout localhost.key -config cert.cnf
openssl x509 -req -in localhost.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out localhost.crt -days 1095 -sha256 -extfile cert.cnf -extensions v3_req
```
**export**
```bash
openssl pkcs12 -export -in localhost.crt -inkey localhost.key -out localhost.p12
openssl pkcs12 -inkey localhost.key -in localhost.crt -export -out localhost.pfx
```
**verify**
```bash
openssl req -text -noout -verify -in localhost.csr
openssl rsa -in localhost.key -check
openssl x509 -in localhost.crt -text -noout
openssl pkcs12 -info -in localhost.pfx
```
**import**
```bash
rootCA.pem to "Manage User Certificates/Trusted Root Certification Authorities"
```
**use**
```bash
localhost.crt
localhost.key
```
**firefox**
```bash
rootCA.pem to "Options/Privacy & Security/View Certificates/Your Certificates"
```
**chrome**
```text
chrome://flags/#allow-insecure-localhost
```
**keys**
```bash
ssh-keygen -t rsa -b 2048 -C "denernun@gmail.com"

Generating public/private rsa key pair.
Enter file in which to save the key (~/.ssh/id_rsa):

Private Key: ~/.ssh/id_rsa.
Public key: ~/.ssh/id_rsa.pub.

cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3N...AAAAB3N ubuntu authorized_keys

puttygen to generate .ppk
```
## netcore
```text
dotnet dev-certs https --help
dotnet dev-certs https --trust
```
###### donwload
[https://sourceforge.net/projects/openssl/](https://sourceforge.net/projects/openssl/)\
[https://opendec.wordpress.com/](https://opendec.wordpress.com/)\
[https://indy.fulgan.com/SSL/](https://indy.fulgan.com/SSL/)
###### links
[https://gist.github.com/princeppy/d00bad66d9caac86d9b7d3ce9e35fc12](https://gist.github.com/princeppy/d00bad66d9caac86d9b7d3ce9e35fc12)\
[https://github.com/jsha/minica](https://github.com/jsha/minica)\
[https://www.hanselman.com/blog/DevelopingLocallyWithASPNETCoreUnderHTTPSSSLAndSelfSignedCerts.aspx](https://www.hanselman.com/blog/DevelopingLocallyWithASPNETCoreUnderHTTPSSSLAndSelfSignedCerts.aspx)\
[https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec](https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec)\
[https://blogs.msdn.microsoft.com/robert_mcmurray/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate](https://blogs.msdn.microsoft.com/robert_mcmurray/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate)
