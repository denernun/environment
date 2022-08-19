## Firebird
**Linux**
```text
# sudo apt update  
# sudo apt upgrade
# sudo apt install libncurses5
# https://github.com/FirebirdSQL/firebird/releases/download/R2_5_9/FirebirdSS-2.5.9.27139-0.amd64.tar.gz
# sudo tar -xf FirebirdSS-2.5.9.27139-0.amd64.tar.gz
# sudo ./install.sh
# sudo nano /opt/firebird/firebird.conf
  DatabaseAccess = Restrict /var/nginx/softclass/db
```
## Postgresql
**Autenticacao**
```text
user=postgres
password=postgres
```
**Windows**
```text
Download
https://www.postgresql.org/download/windows/
```
**Linux**
```text
# install
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list
sudo apt update  
sudo apt upgrade
sudo apt install postgresql-12 postgresql-client-12

# access
sudo nano /etc/postgresql/12/main/postgresql.conf
listen_addresses = '*'

# access
sudo nano /etc/postgresql/12/main/pg_hba.conf
host all all 0.0.0.0/0 md5
host all all ::0/0 md5
local all postgres trust

# services
sudo service postgresql start
sudo service postgresql stop
sudo service postgresql restart
```
**Console**
```text
$ sudo su postgres
$ psql
$ alter user postgres with password '94HHC$Z4uV8go'
$ psql -c "createdb <db_name>"

$ psql
# alter user postgres with password 'StrongAdminP@ssw0rd';
# create database <db_name>;
```

## MySQL
**Linux**
```text
# install
sudo apt-get update
sudo apt-get install mysql-server
sudo mysql_secure_installation utility
sudo systemctl start mysql
sudo systemctl enable mysql
sudo pico /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 0.0.0.0

# shell
sudo mysql -u root -p

# database
CREATE DATABASE 'demodb';
DROP DATABASE 'demodb';
SHOW DATABASES;
USE 'demodb';

# permissions
GRANT ALL PRIVILEGES ON demodb.* to demouser@localhost;
FLUSH PRIVILEGES;

# user
CREATE USER 'demouser'@'localhost' IDENTIFIED BY 'demopassword';
FLUSH PRIVILEGES;

#  password
ALTER USER 'demouser'@'localhost' IDENTIFIED BY 'demopassword';
FLUSH PRIVILEGES;
```
## Redis
**Linux**
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install redis-server
redis-cli -v

sudo nano /etc/redis/redis.conf
#bind 127.0.0.1 ::1
protected-mode no
```
