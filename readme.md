# alarmpi

> Arch Linux ARM (alarm) Installation and Configuration on RaspberryPi

- [alarmpi](#alarmpi)
  - [Setup](#setup)
    - [Network](#network)
      - [WiFi](#wifi)
      - [SSH](#ssh)
  - [Install](#install)

## Setup

- [First Installation](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3)

### Network

- Enable hostname `alarmpi.local`

  ```sh
  pacman --sync avahi
  systemctl enable avahi-daemon
  systemctl start avahi-daemon
  ```

  [Blog](https://www.howtogeek.com/167190/how-and-why-to-assign-the-.local-domain-to-your-raspberry-pi/) about why to enable `.local` domain

#### WiFi

- Set up WiFi connection

  ```sh
  wifi-menu
  ```

- Connect to WiFi network, if not already connected

  ```sh
  # Placeholder wlan0-red needs to be replaced by your profile name, which is created after executing 'wifi-menu'
  netctl start wlan0-red
  ```

  [Source](https://wiki.archlinux.org/index.php/netctl#Starting_a_profile)

- Connect to WiFi network automatically on boot

  ```sh
  netctl enable wlan0-red
  ```

- (Optional) Manually assign IP address

  ```sh
  # Placeholder wlan0 is interface name. List interfaces using ifconfig
  ip address add 192.168.0.123/24 broadcast + dev wlan0
  ```

- Fix DNS problem

  > DNSSEC validation failed: signature-expired

  ```sh
  systemctl restart systemd-resolved.service
  ```

  [Source](https://archlinuxarm.org/forum/viewtopic.php?t=13614)

#### SSH

[Source](https://wiki.archlinux.org/index.php/SSH_keys)

- Generate SSH keys on archlinux server

  ```sh
  # -C stands for comment
  ssh-keygen -C "$(whoami)@$(uname -n)-\$(date -I)"
  ```

- Add archlinux server to SSH config (`~/.ssh/config`) on another computer in the same network

  ```sh
  Host pi
    Hostname alarmpi.local
    User alarm
  ```

- Copy SSH public key to archlinux's authorized keys

  ```sh
  ssh-copy-id pi
  ```

## Install

- Upgrade system packages

  ```sh
  pacman --sync --refresh --sysupgrade
  ```

- Install `vim`

  ```sh
  pacman --sync vim
  ```

- [Airplay](./airplay.md)
- [Pi-hole](./pihole.md)
