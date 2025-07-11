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
# sudo apt update
# sudo apt upgrade
# sudo apt install libtommath1 -y
# wget https://github.com/FirebirdSQL/snapshots/releases/download/snapshot-v5.0-release/Firebird-5.0.3.1679-88943f3-linux-x64.tar.gz
# tar -xzvf Firebird-5.0.3.1679-88943f3-linux-x64.tar.gz
# cd Firebird-5.0.3.1679-88943f3-linux-x64.tar.gz
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

comandos para ver o status, parar e iniciar o servico
# sudo service firebird status
# sudo service firebird stop
# sudo service firebird start
```
```text
ServerMode = SuperClassic
RemoteServicePort = 3060
RemoteAuxPort = 3061
TcpNoNagle = 1
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
