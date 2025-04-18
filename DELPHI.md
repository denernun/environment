### ANDROID
#### SDK MANAGER
```text
cmdline-tools

SDKManager.bat

.\sdkmanager.bat --help
.\sdkmanager.bat --list_installed
.\sdkmanager.bat --list
.\sdkmanager.bat --install "platform-tools"
.\sdkmanager.bat --install "platforms;android-35"
.\sdkmanager.bat --install "build-tools;35.0.0"
.\sdkmanager.bat --install "emulator"

AVDManager.bat

.\sdkmanager.bat --install "system-images;android-27;google_apis;x86"
.\avdmanager.bat create avd -k "system-images;android-27;google_apis;x86" -n Pixel6-Oreo-8.1 -d "pixel_6"
.\emulator.exe -avd Pixel6-Oreo-8.1

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
