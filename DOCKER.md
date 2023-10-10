### INSTALL
```text
$ sudo apt update
$ sudo apt install apt-transport-https curl gnupg-agent ca-certificates software-properties-common -y
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
$ sudo apt install docker-ce docker-ce-cli containerd.io -y
$ sudo usermod -aG docker $USER
$ newgrp docker
$ docker version
$ sudo service docker status
$ sudo service docker stop
$ sudo service docker start
$ docker run hello-world
```
### INIT
```text
$ sudo nano /etc/wsl.conf
  [boot]
  command="service docker start"
$ wsl --shutdown
```
### INIT SYSTEMD
```text
$ sudo nano /etc/wsl.conf
  [boot]
  systemd=true
$ wsl --shutdown
$ sudo systemctl enable docker
$ sudo systemctl disable docker
$ systemctl list-unit-files --type=service
```
### CONECT
```text
$ docker ps
$ docker exec -it postgres /bin/bash
```
### ISSUE
```text
Docker-credential-desktop.exe executable file not found in $PATH using wsl2
$ sudo nano ~/.docker/config.json
change credsStore to credStore
```
### DICAS
[https://github.com/codeedu/wsl2-docker-quickstart#docker-engine-docker-nativo-diretamente-instalado-no-wsl2](https://github.com/codeedu/wsl2-docker-quickstart#docker-engine-docker-nativo-diretamente-instalado-no-wsl2)
