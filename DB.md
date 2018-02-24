# DB

----
Firebird
---

    http://www.firebirdsql.org/en/firebird-2-5/

    Firebird 2.5.7 x32 (UDF)

    Path

    C:\Program Files (x86)\Firebird\Firebird_2_5\bin

----
Postgresql
---

    Windows

    https://www.postgresql.org/download/windows/
    https://www.pgadmin.org/download/pgadmin-4-windows/

    user=postgres
    password=postgres

    Linux
    
    sudo apt-get update && sudo apt-get upgrade
    sudo apt-get install postgresql postgresql-contrib
        
    sudo nano /etc/postgresql/9.X/main/postgresql.conf
    listen_addresses = '*'
    
    sudo nano /etc/postgresql/9.X/main/pg_hba.conf
    host all all 0.0.0.0/0 md5
    host all all ::0/0 md5
    local all postgress trust
    
    sudo systemctl restart postgres
    
    sudo -i -u postgres
    sudo -u postgres psql
    \password postgres
    \q
        
    sudo -u postgres createdb db_name
    sudo -u postgres psql db_name
    alter user postgres with password 'new_password';
    
----
MySQL
---

    Windows


    Linux
    
----
Redis
---

    Windows

    # chocolatey package install
    https://chocolatey.org/install
    
    # chocolatey install
    choco install redis-64

    Windows Manual

    # download
    https://github.com/MicrosoftArchive/redis/releases

    # path
    C:\Program Files\Redis

    # install
    redis-server --service-install redis.windows.conf --loglevel verbose
    
    # uninstall
    redis-server --service-uninstall
    
    Linux

----
