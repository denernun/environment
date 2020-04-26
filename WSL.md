## windows
```terminal
# wsl --list
# wsl --set-version <Distro> 2
$ wsl --set-default-version 2
$ wsl --setdefault <Distro>
$ wsl --distribution <Distro>
$ wsl --user <Username>
$ wsl --unregister <Distro>
```
## linux
```terminal
$ sudo apt update
$ sudo apt full-upgrade
$ sudo apt install libcurl4-gnutls-dev build-essential
$ sudo apt autoremove
```
## linux xserver
```terminal
xfce4-session
```
## linux x410
```terminal
$ echo 'sudo export LIBGL_ALWAYS_INDIRECT=1' >> .bashrc
$ echo "sudo export WSL_HOST=$(tail -1 /etc/resolv.conf | cut -d' ' -f2)" >> .bashrc
$ echo 'sudo export DISPLAY=$WSL_HOST:0' >> .bashrc

$ sudo apt install dbus-x11
$ sudo apt install vim-gtk3
```
