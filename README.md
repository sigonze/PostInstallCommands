# Linux Post Install


> List of the operations after installing Linux.


## Table of contents

[Disable sleep/suspend/hibernate](disable-sleepsuspendhibernate)
[Crackling sounds (Pulseaudio only)](crackling-sounds-pulseaudio-only)
[Increase VM map count](increase-vm-map-count)
[Disable Dualshock/DualSense touchpad in desktop environment](disable-dualshockdualsense-touchpad-in-desktop-environment)
[Enable Freesync (X11 only)](enable-freesync-x11-only)
[Solus customization](solus-customization)
[Fanatec Wheel Driver](fanatec-wheel-driver)
[HP Smart Tank Scanner](hp-smart-tank-scanner)

---
<br>

## Disable sleep/suspend/hibernate

```
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

<br>

## Crackling sounds (Pulseaudio only)

```
sudo sed -i.bak '/default-sample-rate = 44100/cdefault-sample-rate = 48000' /etc/pulse/daemon.conf
sudo pulseaudio -k
```

<br>

## Increase VM map count

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

## Disable Dualshock/DualSense touchpad in desktop environment

```
wget https://raw.githubusercontent.com/sigonze/PostInstallCommands/master/99-libinput-ignore.rules
sudo cp 99-libinput-ignore.rules /etc/udev/rules.d/
```

<br>

## Enable Freesync (X11 only)

```
wget https://raw.githubusercontent.com/sigonze/PostInstallCommands/master/20-amdgpu.conf
sudo cp 20-amdgpu.conf /etc/X11/xorg.conf.d/
```

## Solus customization

```
sudo eopkg rm thunderbird
sudo eopkg up
sudo eopkg rmo
sudo eopkg it bitwarden-desktop discord steam
```

## Fanatec Wheel Driver

Add Solus missing components:

```
sudo eopkg it git
sudo eopkg install -c system.devel
sudo eopkg install linux-current-headers
sudo mkdir -p /etc/udev/rules.d/
```

Install the driver:
```
git clone https://github.com/gotzl/hid-fanatecff.git
make
sudo make install
```

## HP Smart Tank Scanner

```
sudo eopkg it sane-airscan
sudo eopkg it skanpage
```
