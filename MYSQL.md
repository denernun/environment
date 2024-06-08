## MySQL
**Linux**
```text
# install
$ sudo apt update && apt upgrade -y
$ sudo apt-get install mysql-server
$ sudo systemctl start mysql
$ sudo systemctl enable mysql
$ sudo mysql_secure_installation utility
$ sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
  bind-address = 0.0.0.0

# shell
sudo mysql -u root -p

# database
CREATE DATABASE <demodb>;
DROP DATABASE <demodb>;
SHOW DATABASES;
USE <demodb>;

# user
CREATE USER 'demouser'@'localhost' IDENTIFIED BY 'demopassword';
GRANT ALL PRIVILEGES ON *.* TO 'demouser'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;

# user
CREATE USER 'demouser'@'%' IDENTIFIED BY 'demopassword';
GRANT ALL PRIVILEGES ON *.* TO 'demouser'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

#  password
ALTER USER 'demouser'@'localhost' IDENTIFIED BY 'demopassword';
FLUSH PRIVILEGES;

# permissions
GRANT ALL PRIVILEGES ON <demodb>.* to demouser@localhost;
FLUSH PRIVILEGES;
```

