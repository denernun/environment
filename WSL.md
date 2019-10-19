
**windows**
```
$ wsl --set-default-version 2
$ wsl --list --all
$ wsl --setdefault <DistributionName>
$ wsl --distribution <DistributionName>
$ wsl --user <Username>
$ wsl --unregister <DistributionName>
```
**linux
```
$ sudo apt update
$ sudo apt full-upgrade
$ sudo apt install libcurl4-gnutls-dev build-essential
$ sudo apt autoremove
```
**linux xserver
```
xfce4-session
```
**linux x410**
```
$ echo 'sudo export LIBGL_ALWAYS_INDIRECT=1' >> .bashrc
$ echo "sudo export WSL_HOST=$(tail -1 /etc/resolv.conf | cut -d' ' -f2)" >> .bashrc
$ echo 'sudo export DISPLAY=$WSL_HOST:0' >> .bashrc

$ sudo apt install dbus-x11
$ sudo apt install vim-gtk3
```
**delphi
```
$ http://docwiki.embarcadero.com/RADStudio/en/Installing_the_Platform_Assistant_on_Linux
$ tar -xf LinuxPAServer20.0.tar.gz
$ mv PAServer-20.0/ PAServer
$ cd PAServer
$ ./paserver
$ wsl ~/paserver/paserver
```
