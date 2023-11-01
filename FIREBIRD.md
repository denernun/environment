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

# sudo service firebird status
# sudo service firebird stop
# sudo service firebird start
```
**Configuration**
```text
# sudo nano /opt/firebird/firebird.conf

?? Wirecopression
?? wirecrypt

DefaultDBCachePages
  MemoryAvailable (Max 30%) / Connections / PageSize
  1.024.000.000 / 30 / 8192 = 4167

FileSystemCacheThreshold
  (PageSize * Connections) + 1
  (4167 * 30) + 1 = 125011

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
**Aliases**
```text
# sudo nano /opt/firebird/database.conf

ALIAS_DATABASE = /path/of/file/file.fdb {
	RemoteAccess = true
	DefaultDbCachePages = x
}

ALIAS_DATABASE = /path/of/file/file.fdb
```
**Replication**
* [https://www.youtube.com/watch?v=COdWtRn4hgs](https://www.youtube.com/watch?v=COdWtRn4hgs)
* [https://www.youtube.com/watch?v=OAeqTDz5OaM](https://www.youtube.com/watch?v=OAeqTDz5OaM)
* [https://www.youtube.com/watch?v=hZmSW93W9r0](https://www.youtube.com/watch?v=hZmSW93W9r0)
* [https://www.youtube.com/watch?v=VD_7wtuOXos](https://www.youtube.com/watch?v=VD_7wtuOXos)
```text
# sudo nano /opt/firebird/firebird.conf


```
