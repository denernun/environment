### ANDROID
#### SDK MANAGER
```text
cmdline-tools

SDKManager.bat

.\sdkmanager.bat --help
.\sdkmanager.bat --list_installed
.\sdkmanager.bat --list
.\sdkmanager.bat --install "platform-tools"
.\sdkmanager.bat --install "platforms;android-34"
.\sdkmanager.bat --install "build-tools;34.0.0"
.\sdkmanager.bat --install "system-images;android-19;google_apis;x86" (KitKat 4.4)
.\sdkmanager.bat --install "system-images;android-27;google_apis;x86" (Oreo 8.1)
.\sdkmanager.bat --install "emulator"

AVDManager.bat

.\avdmanager.bat create avd -k "system-images;android-19;google_apis;x86" -n Nexus10 -d "Nexus 10"
.\avdmanager.bat create avd -k "system-images;android-27;google_apis;x86" -n Nexus10 -d "Nexus 10"
```
### LINUX
#### PAServer
```text 
sudo apt install build-essential zlib1g-dev libcurl4-gnutls-dev gcc [joe wget p7zip-full curl]
```
#### SYSTEMD
```text 
[Unit]
Description=Socket Service
After=network.target

[Service]
Type=simple
ExecStart=/web/erpclass/socket/socket.service
WorkingDirectory=/web/erpclass/socket/
Restart=always
RestartSec=1
StartLimitInterval=0
User=root

[Install]
WantedBy=multi-user.target
```
#### SYSTEMD COMMANDS
```text 

/etc/systemd/system/socket.service

sudo systemctl daemon-reload

sudo systemctl enable xxx.service
sudo systemctl disable xxx.service

sudo systemctl start xxx.service
sudo systemctl start xxx.service
sudo systemctl stop xxx.service

sudo journalctl -fxeu xxx.service
```
#### KILL
```text 
sok-ps 		=> 	ps -ux | grep socket
sok-kill	=>	sudo pkill socket.service
sok-listen	=>	sudo lsof -i -P -n | grep LISTEN
sok-tail 	=>	sudo tail -f /var/log/syslog | grep socket
sok-start	=> 	sudo service socket start
sok-stop	=> 	sudo service socket stop
sok-status	=>  sudo journalctl -fxeu socket.service
```
#### DICAS
```text 
CnPack Wizard Access Vilation
[https://www.andrecelestino.com/solucao-para-o-access-violation-no-rad-studio-causado-pelo-cnpack/](https://www.andrecelestino.com/solucao-para-o-access-violation-no-rad-studio-causado-pelo-cnpack/)
```
