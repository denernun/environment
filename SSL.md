## self-signed localhost
**chrome**

![image](https://user-images.githubusercontent.com/3607988/132902478-8cf8da91-1237-4d5d-aabc-ad7b7a495a7e.png)

**firefox**

![image](https://user-images.githubusercontent.com/3607988/132902392-eb722a37-3bcd-43fd-b794-4059435b8c54.png)

**edge**

![image](https://user-images.githubusercontent.com/3607988/132902600-b4569f98-2f54-4b97-a90b-99c4813a3063.png)

**create**
```terminal
$env:RANDFILE=".rnd"
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1095 -out rootCA.pem -config cert.conf -reqexts v3_req -extensions v3_ca
openssl req -new -sha256 -nodes -newkey rsa:2048 -out localhost.csr -keyout localhost.key -config cert.conf
openssl x509 -req -in localhost.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out localhost.crt -days 1095 -sha256 -extfile cert.conf -extensions v3_req
```
**cert.conf**
```terminal
[req]
default_bits = 2048
prompt = no
default_md = sha256
x509_extensions = v3_req
distinguished_name = dn

[v3_ca]
basicConstraints = critical,CA:TRUE
subjectKeyIdentifier = hash
authorityKeyIdentifier = keyid:always,issuer:always

[v3_req]
subjectAltName = @alt_names
basicConstraints = CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
extendedKeyUsage = serverAuth
authorityKeyIdentifier = keyid,issuer

[dn]
CN = localhost

[alt_names]
DNS.1 = localhost
```
**verify**
```bash
openssl req -text -noout -verify -in localhost.csr
openssl rsa -in localhost.key -check
openssl x509 -in localhost.crt -text -noout
openssl pkcs12 -info -in localhost.pfx
```
**export**
```bash
openssl pkcs12 -export -in localhost.crt -inkey localhost.key -out localhost.p12
openssl pkcs12 -inkey localhost.key -in localhost.crt -export -out localhost.pfx
```
**import**
```bash
import rootCA.pem to "Manage User Certificates/Trusted Root Certification Authorities"
```
**edge**
```text
edge://flags/#allow-insecure-localhost
edge://net-internals/#hsts
domain localhost delete
clean cache
HKEY_LOCAL_MACHINE\Software\Policies\Google\Chrome\HSTSPolicyBypassList
100 SZ localhost
```
**chrome**
```text
chrome://flags/#allow-insecure-localhost
chrome://net-internals/#hsts
domain localhost delete
clean cache
HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Edge\HSTSPolicyBypassList
100 SZ localhost
```
**firefox**
```bash
import rootCA.pem to "Options/Privacy & Security/View Certificates/Authorities"
```
**use**
```bash
localhost.crt (Certificates)
localhost.key (Private Key)
```
**export to pfx**
```bash
openssl pkcs12 -in localhost.pfx -out localhost.txt -nodes
copy -----BEGIN CERTIFICATE----- to -----END CERTIFICATE----- to localhost.crt
copy -----BEGIN PRIVATE KEY----- to -----END PRIVATE KEY----- to localhost.key
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
