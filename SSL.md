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
