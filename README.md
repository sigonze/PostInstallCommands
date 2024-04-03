# Linux Post Install


> List of the operations I usually perform after installing Linux.


* Disable sleep/suspend/hibernate
```
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

* Crackling sounds (Pulseaudio only)
```
sudo sed -i.bak '/default-sample-rate = 44100/cdefault-sample-rate = 48000' /etc/pulse/daemon.conf
sudo pulseaudio -k
```

* Increase VM map count
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

* Disable Dualshock/DualSense touchpad in desktop environment
```
wget https://raw.githubusercontent.com/sigonze/PostInstallCommands/master/99-libinput-ignore.rules
sudo cp 99-libinput-ignore.rules /etc/udev/rules.d/
```

* Enable Freesync (X11 only)
```
wget https://raw.githubusercontent.com/sigonze/PostInstallCommands/master/20-amdgpu.conf
sudo cp 20-amdgpu.conf /etc/X11/xorg.conf.d/
```
