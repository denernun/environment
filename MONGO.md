## MONGO
**install**
```text

$ wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-5.0.gpg
$ echo "deb [signed-by=/usr/share/keyrings/mongodb-server-5.0.gpg] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list

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
mongosh

use database
show dbs
show users

db.createUser({user: "admin", pwd: "xxx", roles: [{ role: "dbOwner", db: "database" }]})
db.updateUser("admin", { pwd: "xxx" })
db.updateUser("admin", { roles: [{ role: "dbOwner", db: "database" }] })
```
**remove**
```text
$ sudo systemctl stop mongod
$ sudo systemctl disable mongod
$ sudo apt remove --purge --auto-remove mongodb-org
$ sudo rm -rf /var/lib/mongodb
$ sudo rm /etc/apt/sources.list.d/mongodb-org-8.0.list
```

