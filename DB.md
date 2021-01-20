## Firebird
**Linux**
```text
# https://github.com/FirebirdSQL/firebird/releases/download/R2_5_9/FirebirdSS-2.5.9.27139-0.amd64.tar.gz
# sudo tar -xf FirebirdSS-2.5.9.27139-0.amd64.tar.gz
# sudo apt install libncurses5
# sudo ./install
# sudo nano /opt/firebird/2.5/firebird.conf
  DatabaseAccess = Restrict /var/db
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
sudo apt update  
sudo apt upgrade
sudo apt install postgresql-12 postgresql-client-12

# access
sudo nano /etc/postgresql/12/main/postgresql.conf
listen_addresses = '*'

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
# alterar senha
sudo su - postgres
psql -U postgres
psql -c "alter user postgres with password 'StrongAdminP@ssw0rd'"

# criar banco
sudo -u postgres createdb <db_name>
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
```
