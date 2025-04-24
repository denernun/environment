## MONGO
**install**
```text
$ wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-6.0.gpg
$ echo "deb [ arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

$ sudo apt update
$ sudo apt install -y mongodb-org

$ sudo systemctl enable mongod
$ sudo systemctl start mongod
$ sudo systemctl status mongod

sudo apt install net-tools
ss -altnp | grep :27
```
**access**
```text
$ sudo nano /etc/mongod.conf

net:
  port: 27017
  binfIp: 0.0.0.0

security:
  authorization: enabled  
```
**users**
```text
mongosh -u "admin" -p "xxx" --authenticationDatabase admin

show dbs
use admin
show users

# cria o usuario admin
db.createUser({user: "admin", pwd: "xxx", roles: [{ role: "root", db: "admin" }]})
db.updateUser("admin",{ pwd: "xxx" })

# cria o usuario do banco
db.createUser({user: "admin", pwd: "xxx", roles: [{ role: "dbOwner", db: "<database>" }]})
```
**remove**
```text
$ sudo systemctl stop mongod
$ sudo systemctl disable mongod
$ sudo apt remove --purge --auto-remove mongodb-org
$ sudo apt-get purge mongodb-org*
$ sudo rm -r /var/log/mongodb /var/lib/mongodb
$ sudo rm -rf /var/lib/mongodb
$ sudo rm /etc/apt/sources.list.d/mongodb-org-8.0.list
```

