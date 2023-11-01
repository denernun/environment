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

# user
CREATE USER 'demouser'@'localhost' IDENTIFIED BY 'demopassword';
FLUSH PRIVILEGES;

#  password
ALTER USER 'demouser'@'localhost' IDENTIFIED BY 'demopassword';
FLUSH PRIVILEGES;

# permissions
GRANT ALL PRIVILEGES ON demodb.* to demouser@localhost;
FLUSH PRIVILEGES;
```

