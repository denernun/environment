## Postgresql
**Linux**
```text
# install
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list
sudo apt update && sudo apt upgrade -y && sudo apt install postgresql-15 postgresql-client-15 -y

# access
sudo nano /etc/postgresql/15/main/postgresql.conf
listen_addresses = '*'

# access
sudo nano /etc/postgresql/15/main/pg_hba.conf
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
$ alter user postgres with password '<password>';
# create database <db_name>;
```
**Backup**
```text
$ pg_dump -h localhost -p 5432 -U postgres -d <dbname> -v -Fc -b -f /tmp/<dbname>.backup
# pg_restore -h localhost -p 5432 -U postgres -v -c -C -Fc -d <dbname> /tmp/<dbname>.backup
```
