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
**Drop**
```text
$ SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity WHERE pg_stat_activity.datname = 'sys';
```
**Pool**
```text
$ sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
$ sudo wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/keyrings/ACCC4CF8.asc
$ sudo apt update
$ sudo apt install pgbouncer -y
$ sudo systemctl reload pgbouncer.service
$ sudo nano /etc/pgbouncer/userlist.txt
$ "postgres" "<password>"
$ sudo nano /etc/pgbouncer/pgbouncer.ini
  [databases]
  * = host=localhost port=5432
  [pgbouncer]
  listen_addr = *
  listen_port = 6432
  auth_type = md5
  auth_file = /etc/pgbouncer/userlist.txt
  unix_socket_dir = /var/run/postgresql
  logfile = /var/log/postgresql/pgbouncer.log
  pidfile = /var/run/postgresql/pgbouncer.pid
  admin_users = stats_users = postgres
  stats_users = postgres
  pool_mode = session
  max_client_conn = 100
  reserve_pool_size = 10
  application_name_add_host = 1
  ignore_startup_parameters = extra_float_digits
```
**Monitor**
```text
pg_top -C -I -W -h localhost -p 5432 -U postgres
```
**PGTune**
```text
# DB Version: 16
# OS Type: linux
# DB Type: desktop
# Total Memory (RAM): 4 GB
# CPUs num: 2
# Connections num: 200
# Data Storage: ssd

max_connections = 200
shared_buffers = 256MB
effective_cache_size = 1GB
maintenance_work_mem = 256MB
checkpoint_completion_target = 0.9
wal_buffers = 7864kB
default_statistics_target = 100
random_page_cost = 1.1
effective_io_concurrency = 200
work_mem = 546kB
huge_pages = off
min_wal_size = 100MB
max_wal_size = 2GB
```
