## Pi-hole

### Requisites

```sh
# Install pacaur deps
pacman --sync git base-devel sudo expac jq
# Probably not necessary after installing base-devel
# pacman --sync make cmake gcc automake autoconf tmux fakeroot logrotate patch php-sqlite php-cgi lighttpd sudo mlocate

# Enable swap
swapon --show
fallocate --length 1G /swapfile
chmod 600 /swapfile
swapon /swapfile
swapon --show

# Set sudo
gpasswd --add alarm wheel
visudo
# Uncomment %wheel ALL=(ALL) NOPASSWD: ALL

# Build auracle-git
pacman --sync meson gtest gmock fmt nlohmann-json
cd ~/
git clone https://aur.archlinux.org/auracle-git.git
cd auracle-git
makepkg --ignorearch
pacman --upgrade auracle-git-*

# Build pacaur
cd ~/
git clone https://aur.archlinux.org/pacaur.git
cd pacaur
makepkg --syncdeps --install

# Alternative: yay
# Build yay
pacman --sync go
cd ~/
git clone https://aur.archlinux.org/yay.git
cd yay
```

### Installation

```sh
pacman --sync nginx-mainline php-fpm
pacaur --sync pi-hole-server
```

## Related

To be implemented:

- [Making devices use Pi-hole](https://wiki.archlinux.org/index.php/Pi-hole#Making_devices_use_Pi-hole)
