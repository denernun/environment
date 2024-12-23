## MONGO
**install**
```text
$ wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-4.4.gpg
$ echo "deb [signed-by=/usr/share/keyrings/mongodb-server-4.4.gpg] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

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
```text
**users**
```
**users**
```text
mongo

use database
show dbs
show users

# cria o usuario admin
db.createUser({user: "admin", pwd: "xxx", roles: [{ role: "root", db: "admin" }]})

db.createUser(
  {
    user: "superadmin",
    pwd: "suaSenhaSegura",
    roles: [
      { role: "userAdminAnyDatabase", db: "admin" },
      { role: "dbAdminAnyDatabase", db: "admin" },
      { role: "readWriteAnyDatabase", db: "admin" },
      { role: "clusterAdmin", db: "admin" }
    ]
  }
)

# cria o usuario do banco
db.createUser({user: "admin", pwd: "xxx", roles: [{ role: "dbOwner", db: "database" }]})
db.updateUser("admin", { pwd: "xxx" })
db.updateUser("admin", { roles: [{ role: "dbOwner", db: "database" }] })
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

