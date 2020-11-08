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
# Update and select a new german mirrors since the included onces are broken
# use just pacman-mirrors
sudo pacman-mirrors -c Germany
# now upgrade - remove --noconfirm for interactive .. but for a fresh system that does not really make any sense
sudo pacman -Suy --noconfirm
sudo update-grub
```

- be sure, before the reboot, that you still have a kernel installed. This tends to happend during the update above. Use
```
# check the installed kernel
mhwd-kernel -li

# install a kernel, might only be possible after a reboot ... otherwise "no target"
# TODO: out of any reason this does not work "not target"

# we should downgrade / upgrade only to 5.4, not higher. Otherwise bluetooth will not work properly 
# - headset cannot be paried / are not shown as audio devices
# - paired devices cannot be reconnected after a reboot
sudo mhwd-kernel -i linux54
```
- reboot once

### Stage1 provisioning

```
# PRECONDITION: enable AUR repos in the pamac-gtk gui or using those commands below
sudo -s
echo "EnableAUR" >> /etc/pamac.conf
echo "KeepBuiltPkgs" >> /etc/pamac.conf
echo "CheckAURUpdates" >> /etc/pamac.conf
echo "CheckAURVCSUpdates" >> /etc/pamac.conf
pamac update
exit

pamac install homemaker-git
# OR alternatively without AUR for now
sudo curl -O /usr/local/bin/homemaker https://foosoft.net/projects/homemaker/dl/homemaker_linux_amd64.tar.gz && chmod +x /usr/local/bin/homemaker

git clone https://github.com/eugenmayer/dotfiles_initial
cd dotfiles_initial
homemaker homemaker.toml ./
# if you need/like resilio sync
homemaker --task resilio homemaker.toml ./
# extra packagaes for the early stage
homemaker --task packagaes_extra homemaker.toml ./
```
