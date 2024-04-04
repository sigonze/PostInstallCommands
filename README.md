# Linux Post Install


> List of the operations I usually perform after installing Linux.


## Table of contents

1. [Disable sleep/suspend/hibernate](#1-disable-sleepsuspendhibernate)
2. [Crackling sounds (Pulseaudio only)](#2-crackling-sounds-pulseaudio-only)
3. [Increase VM map count](#3-increase-vm-map-count)
4. [Disable Dualshock/DualSense touchpad in desktop environment](#4-disable-dualshockdualsense-touchpad-in-desktop-environment)
5. [Enable Freesync (X11 only)](#5-enable-freesync-x11-only)

---
<br>

## 1. Disable sleep/suspend/hibernate

```
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

<br>

## 2. Crackling sounds (Pulseaudio only)

```
sudo sed -i.bak '/default-sample-rate = 44100/cdefault-sample-rate = 48000' /etc/pulse/daemon.conf
sudo pulseaudio -k
```

<br>

## 3. Increase VM map count

```
wget https://raw.githubusercontent.com/sigonze/PostInstallCommands/master/10-vm-map-count.conf
sudo cp 10-vm-map-count.conf /etc/sysctl.d/
```
To update without restarting:
```
sudo sysctl -p
```
To check the current value:
```
cat /proc/sys/vm/max_map_count
```

<br>

## 4. Disable Dualshock/DualSense touchpad in desktop environment

```
wget https://raw.githubusercontent.com/sigonze/PostInstallCommands/master/99-libinput-ignore.rules
sudo cp 99-libinput-ignore.rules /etc/udev/rules.d/
```

<br>

## 5. Enable Freesync (X11 only)

```
wget https://raw.githubusercontent.com/sigonze/PostInstallCommands/master/20-amdgpu.conf
sudo cp 20-amdgpu.conf /etc/X11/xorg.conf.d/
```
