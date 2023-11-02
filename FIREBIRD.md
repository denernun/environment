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

ServerMode = Classic
RemoteServicePort = 3060
DatabaseAccess = Full
RemoteAccess = true
DataTypeCompatibility = 2.5
DefaultDBCachePages = 768 # MemoAvailable (1.024.000.000) (Max 30%) / Connections / PageSize
FileSystemCacheThreshold = 1M # (PageSize * Connections) + 1
WireCrypt = Enabled 
TempBlockSize = 1M
TempCacheLimit = 64M
LockMemSize = 30M
LockHashSlots = 30011
AuthServer = Srp
AuthClient = Srp
UserManager = Srp
```
**Configuration Remote**
```text
# sudo nano /opt/firebird/firebird.conf

ServerMode = Super
RemoteServicePort = 3060
DatabaseAccess = Full
RemoteAccess = true
DataTypeCompatibility = 2.5
DefaultDbCachePages = 100K
FileSystemCacheThreshold = 2M
TempBlockSize = 2M
TempCacheLimit = 1000M
TracePlugin = fbtrace
WireCrypt = Enabled
LockMemSize = 15M
LockHashSlots = 30011
AuthServer = Srp
AuthClient = Srp
UserManager = Srp
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
