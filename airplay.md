# AirPlay

Install Shairport Sync to enable AirPlay in your network.

## Setup

```sh
pacman --sync shairport-sync
# Install Advanced Linux Sound Architecture (ALSA)
pacman --sync alsa-utils
# Add alarm user to audio group
usermod --append --groups audio alarm
# Install ALSA firmware
# Source: https://github.com/alsa-project/alsa-firmware
pacman --sync alsa-firmware
```

## Usage

- Control volume in soundcard 0

  ```sh
  alsamixer --card 0
  ```

## Related

- [shairport sync - archlinux wiki](https://wiki.archlinux.org/index.php/Shairport_Sync)
- [Guide for RaspberryPi Audio](https://www.chaos-reins.com/2017-06-24-raspberry-pi-arch-audio/)
