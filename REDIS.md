## Redis
**Linux**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install redis-server -y
redis-cli -v

sudo systemctl start redis-server
sudo systemctl enable redis-server

sudo nano /etc/redis/redis.conf
bind 127.0.0.1 ::1
protected-mode no
requirepass password
user default on >password ~* &* +@all

ACL SETUSER default on >password ~* &* +@all
```
