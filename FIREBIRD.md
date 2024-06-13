## Firebird 5.0
**Windows**
```text
# .\instsvc.exe i -n Firebird_5.0
# .\isql.exe
# connect security5.fdb user SYSDBA;
# create user SYSDBA password 'masterkey';
# commit;
# connect security5.fdb user SYSDBA password masterkey;
# select * from sec$users;

# gsec -user SYSDBA 
# gsec>add SYSDBA -pw masterkey 
# gsec>quit
```
**Linux**
```text
# sudo apt update  
# sudo apt upgrade
# wget https://github.com/FirebirdSQL/firebird/releases/download/v5.0.0-RC1/Firebird-5.0.0.1227-ReleaseCandidate1-linux-x64.tar.gz
# tar -xzvf Firebird-5.0.0.1227-ReleaseCandidate1-linux-x64.tar.gz
# cd Firebird-5.0.0.1227-ReleaseCandidate1-linux-x64.tar.gz
# sudo ./install.sh -path=/opt/firebird
# sudo service firebird.opt_firebird5 start

# gsec -user SYSDBA 
# gsec>add SYSDBA -pw masterkey 
# gsec>quit

# /etc/sysctl.conf
  vm.max_map_count = 256000
# sysctl -p /etc/sysctl.conf 

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
AuthServer = Srp, Win_Sspi
AuthClient = Srp, Win_Sspi
UserManager = Srp, Win_Sspi
```
**Configuration Remote**
```text
# sudo nano /opt/firebird/firebird.conf

ServerMode = Super
RemoteServicePort = 3050
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
AuthServer = Srp, Win_Sspi
AuthClient = Srp, Win_Sspi
UserManager = Srp, Win_Sspi
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
**IBSurgeon**
* [https://ib-aid.com/en/articles/how-to-install-firebird-3-0-and-4-0-on-linux](https://ib-aid.com/en/articles/how-to-install-firebird-3-0-and-4-0-on-linux)
* [https://ib-aid.com/en/articles/23-more-ways-to-speed-up-firebird](https://ib-aid.com/en/articles/23-more-ways-to-speed-up-firebird)
* [https://ib-aid.com/en/simple-insert-update-delete-test-for-firebird](https://ib-aid.com/en/simple-insert-update-delete-test-for-firebird)

**Replication**
* [https://www.youtube.com/watch?v=COdWtRn4hgs](https://www.youtube.com/watch?v=COdWtRn4hgs)
* [https://www.youtube.com/watch?v=OAeqTDz5OaM](https://www.youtube.com/watch?v=OAeqTDz5OaM)
* [https://www.youtube.com/watch?v=hZmSW93W9r0](https://www.youtube.com/watch?v=hZmSW93W9r0)
* [https://www.youtube.com/watch?v=VD_7wtuOXos](https://www.youtube.com/watch?v=VD_7wtuOXos)
```text
# sudo nano /opt/firebird/firebird.conf


```
