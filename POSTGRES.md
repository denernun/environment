## Postgresql
**Windows**
```text
Download
https://www.postgresql.org/download/windows/
```
**Linux**
```text
# install
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list
sudo apt update && sudo apt upgrade -y && sudo apt install postgresql-12 postgresql-client-12 -y

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
$ alter user postgres with password '<password>';
# create database <db_name>;
```
**Backup**
```text
$ pg_dump -h localhost -p 5432 -U postgres -d <dbname> -v -Fc -b -f /tmp/<dbname>.backup
# pg_restore -h localhost -p 5432 -U postgres -v -c -C -Fc -d <dbname> /tmp/<dbname>.backup
```
**Pool**
```text
$ https://www.scaleway.com/en/docs/tutorials/install-pgbouncer/
$ sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
$ sudo wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
$ sudo apt update
$ sudo apt install pgbouncer -y

$ sudo nano /etc/pgbouncer/pgbouncer.ini
  [databases]
  * = host=localhost port=5432
  [pgbouncer]
  logfile = /var/log/postgresql/pgbouncer.log
  pidfile = /var/run/postgresql/pgbouncer.pid
  user = <username>
  listen_addr = localhost
  listen_port = 6432
  unix_socket_dir = /var/run/postgresql
  auth_type = md5
  auth_file = /etc/pgbouncer/userlist.txt

$ sudo nano /etc/pgbouncer/userlist.txt
  echo -n "md5"; echo -n "<password><username>" | md5sum | awk '{print $1}'
  "<username>" "<md5>"

$ sudo systemctl reload pgbouncer.service
$ sudo psql -h localhost -U <username> -p 6432
```
**Monitor**
```text
pg_top -C -I -W -h localhost -p 5432 -U postgres
```

