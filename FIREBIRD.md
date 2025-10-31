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

[Download](https://github.com/FirebirdSQL/snapshots/releases/tag/snapshot-v5.0-release)
```text
# sudo apt update && sudo apt upgrade -y && sudo apt install libtommath1 -y
# wget https://github.com/FirebirdSQL/firebird/releases/download/v5.0.3/Firebird-5.0.3.1683-0-linux-x64.tar.gz
# tar -xzvf Firebird-5.0.3.1683-0-linux-x64.tar.gz
# cd Firebird-5.0.3.1683-0-linux-x64.tar.gz
# sudo ./install.sh
# sudo mkdir /data
# sudo chown firebird:firebird /data
# sudo nano /opt/firebird/firebird.conf

colar no final do arquivo a configuracao

executar após a alteracao no arquivo anterior
# sudo service firebird restart

copiar e mover os arquivos
# sudo mv *.fdb /data
# sudo chown firebird:firebird /data/*

verificar o status do servico
# sudo service firebird status
```
```text
# ============================================================
# Configuração Firebird 5.0.3 para ERPClass
# Otimizada para performance e segurança
# ============================================================

# Modo do servidor (SuperClassic recomendado para ERPClass)
ServerMode = SuperClassic

# Portas de comunicação
RemoteServicePort = 3060
RemoteAuxPort = 3061

# Configurações de autenticação
AuthServer = Srp256,Srp,Legacy_auth
AuthClient = Srp256,Srp,Legacy_auth
UserManager = Srp,Legacy_UserManager

# Segurança de conexão
WireCrypt = Enabled

# Diretórios
DatabaseAccess = Full
ExternalFileAccess = Full

# Performance
DefaultDbCachePages = 2048
TempCacheLimit = 67108864

# Configurações de rede
RemoteBindAddress = 0.0.0.0
TcpNoDelay = 1

# Logs
AuditTraceConfigFile =
MaxUserTraceLogSize = 10485760

# Configurações específicas para ERPClass
LockMemSize = 1048576
LockHashSlots = 22111
EventMemSize = 65536
```

**IBSurgeon Calculator**
* [https://cc.ib-aid.com/democalc.html](https://cc.ib-aid.com/democalc.html)

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
