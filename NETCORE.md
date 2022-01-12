## netcore
**sdk**
```terminal
$ sudo wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
$ sudo dpkg -i packages-microsoft-prod.deb
$ sudo apt-get update
$ sudo apt-get install apt-transport-https
$ sudo apt-get update
$ sudo apt-get install dotnet-sdk-3.1
```
**service systemd**
```terminal
[Unit]
Description=xxx

[Service]
#Type=notify (only service worker)
WorkingDirectory=/var/www/xxx
ExecStart=/usr/bin/dotnet /var/www/xxx/xxx.dll
Restart=always
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=xxx
User=ubuntu
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=ASPNETCORE_URLS=http://localhost:5001
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target    
```
**service systemd install**
```terminal
/etc/systemd/system/xxx.service
sudo systemctl daemon-reload
sudo systemctl enable xxx.service
sudo journalctl -fxeu xxx.service
```
**service wsl**
```terminal
# /etc/init.d
# chmod +x <service>
# sudo update-rc.d <service> defaults
# ASPNETCORE_ENVIRONMENT=[Development,Release,Production]
# ASPNETCORE_URLS=[http://*:XXXX]
```
