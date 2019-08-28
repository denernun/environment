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

# trocar senha
sudo -u postgres psql
\password postgres
\q

# trocar senha
\alter user postgres with password 'new_password';
\q

# criar banco
sudo -u postgres createdb 'db_name'
createdb -U postgres <db_name>
```

---

### MySQL

**Windows**

download
[https://dev.mysql.com/downloads/mysql/](MySQL)


```text
Windows

user=root
password: abc12345

Linux

```

---

### Redis

**Windows**

chocolatey package install
https://chocolatey.org/install

```text
chocolatey install
choco install redis-64
```

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
