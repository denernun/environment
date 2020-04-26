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
$ sudo apt update
$ sudo apt full-upgrade
$ sudo apt install libcurl4-gnutls-dev build-essential
$ sudo apt autoremove
```
**x410**
```terminal
# echo 'export LIBGL_ALWAYS_INDIRECT=1' >> ~/.bashrc
# echo "export WSL_HOST=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0.0" >> ~/.bashrc
# echo "export DISPLAY=$WSL_HOST" >> ~/.bashrc

$ dbus-launch --exit-with-x11
$ if error command not found
$ sudo apt install dbus-x11
$ if Session lifetime based on X11 requested
$ sudo dbus-uuidgen --ensure
```
**xfce**
```terminal
$ sudo apt update && sudo apt -y upgrade
$ sudo apt install xfce4 xfce4-terminal
$ sudo apt install vim-gtk3
```
