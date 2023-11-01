## Firebird 2.5
**Linux**
```text
# sudo apt update  
# sudo apt upgrade
# sudo apt install libncurses5
# https://github.com/FirebirdSQL/firebird/releases/download/R2_5_9/FirebirdSS-2.5.9.27139-0.amd64.tar.gz
# sudo tar -xf FirebirdSS-2.5.9.27139-0.amd64.tar.gz
# sudo ./install.sh
# sudo nano /opt/firebird/firebird.conf
  DatabaseAccess = Restrict /var/nginx/softclass/db
```
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
```
