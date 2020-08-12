**windows**
```terminal
# wsl --list
# wsl --set-version <Distro> 2
# wsl --set-default-version 2
# wsl --list --verbose
# wsl --user <Username>
# wsl --unregister <Distro>
```
**linux**
```terminal
$ sudo apt update && sudo apt -y upgrade
$ sudo apt autoremove
```
**x410**
```terminal
# export LIBGL_ALWAYS_INDIRECT=1
# export WSL_HOST=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0.0
# export DISPLAY=$WSL_HOST
```
**xfce4**
```terminal
$ sudo apt purge xrdp
$ sudo apt install xrdp
$ sudo apt install xfce4 xfce4-terminal xfce4-goodies firefox
```
**rdp**
```terminal
$ sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak
$ sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini
$ sudo sed -i 's/max_bpp=32/#max_bpp=32\nmax_bpp=128/g' /etc/xrdp/xrdp.ini
$ sudo sed -i 's/xserverbpp=24/#xserverbpp=24\nxserverbpp=128/g' /etc/xrdp/xrdp.ini
$ sudo echo xfce4-session > ~/.xsession
$ sudo nano /etc/xrdp/startwm.sh
  - test -x
  - exec /bin/sh
  + startxfce4
$ sudo /etc/init.d/xrdp start
```
