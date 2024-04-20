### ANDROID
#### SDK MANAGER
```text
cmdline-tools

SDKManager.bat

sdkmanager.bat --help
sdkmanager.bat --list_installed
sdkmanager.bat --list
sdkmanager.bat --install "platform-tools"
sdkmanager.bat --install "platforms;android-34"
sdkmanager.bat --install "build-tools;34.0.0"
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
