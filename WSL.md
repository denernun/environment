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
$ sudo apt autoremove
```
