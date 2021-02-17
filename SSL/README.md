## self-signed
**create**
```terminal
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem -config cert.cnf
openssl req -new -sha256 -nodes -out localhost.csr -newkey rsa:2048 -keyout localhost.key -config cert.cnf
openssl x509 -req -in localhost.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out localhost.crt -days 500 -sha256 -extfile cert.ext
```
## import
```bash
rootCA.pem to "Manage User Certificates/Trusted Root Certification Authorities"
```
## use
```bash
localhost.crt
localhost.key
```
## firefox
```text
Options/Privacy & Security/View Certificates/Authorities/Import/rootCA.pem
Options/Privacy & Security/View Certificates/People/Import/localhost.key
```
## chrome
```text
chrome://flags/#allow-insecure-localhost
```
## keys
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
[https://github.com/jsha/minica](https://github.com/jsha/minica)\
[https://www.hanselman.com/blog/DevelopingLocallyWithASPNETCoreUnderHTTPSSSLAndSelfSignedCerts.aspx](https://www.hanselman.com/blog/DevelopingLocallyWithASPNETCoreUnderHTTPSSSLAndSelfSignedCerts.aspx)\
[https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec](https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec)\
[https://blogs.msdn.microsoft.com/robert_mcmurray/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate](https://blogs.msdn.microsoft.com/robert_mcmurray/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate)
