## MONGO
**install**
```text
$ sudo apt-cache policy libssl1.1
$ sudo -i
$ wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2_amd64.deb
$ sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2_amd64.deb

$ sudo apt install gnupg curl

$ curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
$ echo "deb [signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

$ curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /etc/apt/trusted.gpg.d/mongo.gpg --dearmor 
$ echo "deb [arch=amd64,arm64] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb.list

$ sudo apt update
$ sudo apt install -y mongodb-org

$ sudo systemctl enable mongod
$ sudo systemctl start mongod
$ sudo systemctl status mongod

sudo apt install net-tools
ss -altnp | grep :27
```
**config**
```text
$ 
```
**remove**
```text
$ sudo systemctl stop mongod
$ sudo apt remove --purge --auto-remove mongodb-org
$ sudo rm -rf /var/lib/mongodb
```

