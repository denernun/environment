## Postgresql
**Linux**
```text
# install
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list
sudo apt update && sudo apt upgrade -y && sudo apt install postgresql-1x postgresql-client-1x -y

# access
sudo nano /etc/postgresql/1x/main/postgresql.conf
listen_addresses = '*'

# access
sudo nano /etc/postgresql/1x/main/pg_hba.conf

@versao 12
host all all 0.0.0.0/0 md5
host all all ::0/0 md5
local all postgres trust

@versao 15
host all all 0.0.0.0/0 scram-sha-256
host all all ::0/0 scram-sha-256

# services
sudo service postgresql start
sudo service postgresql stop
sudo service postgresql restart
```
**Console**
```text
$ sudo su postgres
$ psql
$ alter user postgres with password '<password>';
# create database <db_name>;
```
**Backup**
```text
$ pg_dump -h localhost -p 5432 -U postgres -d <dbname> -v -Fc -b -f /tmp/<dbname>.backup
# pg_restore -h localhost -p 5432 -U postgres -v -c -C -Fc -d <dbname> /tmp/<dbname>.backup
```
**PSQL**
```text
$ \l
$ \c
$ \dt
```
**Remove**
```text
$ sudo apt-get --purge remove postgresql postgresql-*
$ dpkg -l | grep postgres
$ sudo apt-get --purge remove postgresql postgresql-doc postgresql-common
```


