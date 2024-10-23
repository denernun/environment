## MONGO
**install**
```text

$ wget -qO - https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-7.0.gpg
$ echo "deb [signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

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
mongo
use admin
db.createUser({
  user: "admin",
  pwd: "Abc@010203@2021",
  roles: [{ role: "userAdminAnyDatabase", db: "admin" }]
})
exit
```
**remove**
```text
$ sudo systemctl stop mongod
$ sudo apt remove --purge --auto-remove mongodb-org
$ sudo rm -rf /var/lib/mongodb
```

