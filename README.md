## WAT

This repo helps me up to preboot a fresh installation of (right now) Manjaro gnome to a 
i3 based session including mu bindings and setup, before i continue finish provisioning with
all my configuration in stage 2.

This part is public, it taks a vanialla installation and makes it ready for auto-provisioning.

- The i3-session is run using `gnome-flashback` on top of a gnome-session. 

```
git clone https://github.com/eugenmayer/intial_dotfiles
cd initial_dotfiles
pamac install homemaker-git
homemaker homemaker.toml ./ 
```
