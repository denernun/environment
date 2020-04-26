## windows
```terminal
# wsl --list
# wsl --set-version <Distro> 2
# wsl --set-default-version 2
# wsl --list --verbose
# wsl --user <Username>
# wsl --unregister <Distro>
```
## linux
```terminal
$ sudo apt update
$ sudo apt full-upgrade
$ sudo apt install libcurl4-gnutls-dev build-essential
$ sudo apt autoremove
```
## linux x410
```terminal
# echo 'export LIBGL_ALWAYS_INDIRECT=1' >> ~/.bashrc
# echo "export WSL_HOST=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0.0" >> ~/.bashrc
# echo "export DISPLAY=$WSL_HOST" >> ~/.bashrc

$ sudo apt install dbus-x11
$ sudo apt install vim-gtk3
```
