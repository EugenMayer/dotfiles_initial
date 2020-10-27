## WAT

This repo helps me up to preboot a fresh installation of (right now) Manjaro GNOME to a 
i3 based session including my keyboard bindings. This is stage1 for the configuration of my linux devices (and config synchronisation).

- I usually run this step once when i pre-setup a new box.
- Everything else is then done in a (private) stage2 installer, where i actually sync all my configurations across all devices

This whole lot is only for configuration handling, setting up developmen environments and tools is done using Ansible and shared across multiple team members. Everything regards to projects, tools and so on.

- The i3-session is run using `gnome-flashback` on top of a gnome-session. 
- it will deploy a function i3 configuration to start with


## Installation

### Manajro Gnome

- Install it using the usual installing
- on first boot do a complete system update since usually the installer of Gnome is far behind the latest stable
```
# select a new mirror, since the first one is broken and leads to a broken upgrade
# use just pacman-mirror to list all the mirrors
sudo pacman-mirror -f 2
# now upgrade
sudo pacman -Suy
sudo update-grub
```

- be sure, before the reboot, that you still have a kernel installed. This tends to happend during the update above. Use
```
# check the installed kernel
mhwd-kernel -li
# install a kernel
sudo mhwd-kernel -i linnux59
```
- reboot once

### Stage1 provisioning

```
# be sure to enable AUR repos before you can install this
pamac install homemaker-git
# or alternatively without AUR for now
sudo curl -O /usr/local/bin/homemaker https://foosoft.net/projects/homemaker/dl/homemaker_linux_amd64.tar.gz && chmod +x /usr/local/bin/homemaker

git clone https://github.com/eugenmayer/dotfiles_initial
cd dotfiles_initial
homemaker homemaker.toml ./ 
```
