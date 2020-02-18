# DB

---

### Firebird

**Windows**

```text
http://www.firebirdsql.org/en/firebird-2-5/

Firebird 2.5.9 x32 (UDF)

Path

C:\Program Files (x86)\Firebird\Firebird_2_5\bin
```

**Linux**

```text
# sudo apt install firebird2.5-superclassic
# sudo dpkg-reconfigure firebird2.5-superclassic

# sudo nano /etc/firebird/2.5/firebird.conf
  RemoteBindAddress=
  DatabaseAccess=Full

# sudo isql-fb
  connect "localhost:database.fdb" user 'USER' password 'password';
```

---

### Postgresql

**Autenticacao**

```text
user=postgres
password=postgres
```

**Windows**

```text
Download
https://www.postgresql.org/download/windows/

# criar banco
createdb -U postgres <db_name>

# dml
psql -U postgres <db_name>
```

**Linux**

```text

# install
sudo apt update  
sudo apt upgrade
sudo apt install postgresql postgresql-contrib

# access
sudo nano /etc/postgresql/9.X/main/postgresql.conf
listen_addresses = '*'

sudo nano /etc/postgresql/9.6/main/pg_hba.conf
host all all 0.0.0.0/0 md5
host all all ::0/0 md5
local all postgres trust

# services
sudo service postgresql start
sudo service postgresql stop
sudo service postgresql restart

# criar banco
sudo -u postgres createdb 'db_name'

# console
sudo -u postgres psql

# trocar senha
\password postgres
\q

# trocar senha
\alter user postgres with password 'new_password';
\q

```

---

### MySQL

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

#  password
UPDATE mysql.user SET authentication_string = PASSWORD('password') WHERE User = 'root';
FLUSH PRIVILEGES;

# database
CREATE DATABASE 'demodb';
DROP DATABASE 'demodb';
USE 'demodb';
SHOW DATABASES;

# user
CREATE USER 'demouser'@'localhost' IDENTIFIED BY 'demopassword';
FLUSH PRIVILEGES;

# permissions
GRANT ALL PRIVILEGES ON demodb.* to demouser@localhost;
FLUSH PRIVILEGES;
```
---

### Redis

**Windows**

download
https://github.com/MicrosoftArchive/redis/releases

```text
path
C:\Program Files\Redis

install
redis-server --service-install redis.windows.conf --loglevel verbose

uninstall
redis-server --service-uninstall
```

**Linux**

```text
# install
sudo apt install

```
