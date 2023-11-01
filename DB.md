## Redis
**Linux**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install redis-server -y
redis-cli -v

sudo nano /etc/redis/redis.conf
#bind 127.0.0.1 ::1
protected-mode no
```
