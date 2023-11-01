## Firebird 5.0
**Windows**
```text
# .\instsvc.exe i -n Firebird_5.0
# .\isql.exe
# connect security.fdb user SYSDBA;
# create user SYSDBA password 'masterkey';
# commit;
# connect security.fdb user SYSDBA password masterkey;
# select * from sec$users;
```
**Linux**
```text
# sudo apt update  
# sudo apt upgrade
# wget https://github.com/FirebirdSQL/firebird/releases/download/R2_5_9/FirebirdSS-2.5.9.27139-0.amd64.tar.gz
# tar -xzvf FirebirdSS-2.5.9.27139-0.amd64.tar.gz
# cd FirebirdSS-2.5.9.27139-0.amd64
# sudo ./install.sh
# sudo nano /opt/firebird/firebird.conf
```
**Configuration**
```text
ServerMode = Classic
RemoteServicePort = 3060
DefaultDBCachePages = 2048
UseFileSystemCache = true
TempCacheLimit = 1024M
InlineSortThreshold = 16384
ExtConnPoolSize = 64
ExtConnPoolLifeTime = 3600
DataTypeCompatibility = 2.5
AuthServer = Srp256, Legacy_Auth
UserManager = Srp, Legacy_UserManager
DatabaseAccess = Restrict /var/xxx
```
**Replication**
```text
```


