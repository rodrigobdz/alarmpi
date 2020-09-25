# alarmpi

> Arch Linux ARM (alarm) Installation and Configuration on RaspberryPi

## First Installation

- https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3

## Set up WiFi

`wifi-menu`

### Start WiFi if not started already

netctl start wlan0-red

### Connect on boot

netctl enable wlan0-red

## Vim

pacman -S vim

## Fix DNS problem

### DNSSEC validation failed: signature-expired

```sh
systemctl restart systemd-resolved.service
```

#### Resources

- https://archlinuxarm.org/forum/viewtopic.php?t=13614

## Upgrade system packages

### Fix 404 problem while trying to install any package

```sh
pacman -Syu
```

## Hostname alarmpi.local

```sh
pacman -S avahi
systemctl enable avahi-daemon
systemctl start avahi-daemon
```

### Resources

- https://www.howtogeek.com/167190/how-and-why-to-assign-the-.local-domain-to-your-raspberry-pi/

## SSH keys

https://wiki.archlinux.org/index.php/SSH_keys

### arch server

```sh
ssh-keygen -C "$(whoami)@$(uname -n)-\$(date -I)"
```

### ssh_config

```sh
Host pi
  Hostname alarmpi.local
  User alarm
```

### client

```sh
ssh-copy-id pi
```

## AirPlay

```sh
pacman -S shairport-sync
pacman -S alsa-utils
usermod -a -G audio alarm
pacman -S alsa-firmware

# Volume
alsamixer -c 0
```

### Resources

- [shairport sync - archlinux wiki](https://wiki.archlinux.org/index.php/Shairport_Sync)
- [Guide for RaspberryPi Audio](https://www.chaos-reins.com/2017-06-24-raspberry-pi-arch-audio/)

## Coming Soon

https://wiki.archlinux.org/index.php/Pi-hole#Making_devices_use_Pi-hole
