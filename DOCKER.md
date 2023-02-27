## ISSUES
```text
@ run as administrator
# net stop com.docker.service
# net start com.docker.service
# tasklist /svc /fi "imagename eq svchost.exe" | findstr LxssManager
# sc queryex LxssManager
# wmic process where ProcessID=XXXXX delete
# net start LxssManager
# wsl -l -v
# wsl --unregister

https://cloudcone.com/docs/article/how-to-install-docker-on-ubuntu-22-04-20-04/

Docker-credential-desktop.exe executable file not found in $PATH using wsl2
In ~/.docker/config.json change credsStore to credStore

docker exec -it postgres /bin/bash
```
