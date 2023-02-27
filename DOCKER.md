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
# wsl unregister
```
