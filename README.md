# Logitech K400 Plus - Linux helper scripts

This repository is targeting Logitech K400 Plus keyboard and common issue with switching to normal Fn functioning. You can find an C code which was rewritten a little for this devices purpose. I wasn't able to create "nice" solution to catch only this device upon a start, isntead I'm pointing stirght to /dev/hidraw* device, in my case /dev/hidraw2. Feel free to create issue with other solutions.

Edit: Looks like [Solaar](https://github.com/pwr/Solaar) (git version) is now supporting Fn swap in options for K400 Plus which is great, but after wake-up it's still messed up so I'm leaving this repo anyway.

### 1. Script used to switch Fn functioning back to normal

__k400_plus_conf.c__ is modded version of [k810_conf.c](http://www.trial-n-error.de/posts/2012/12/31/logitech-k810-keyboard-configurator).
```
curl https://raw.githubusercontent.com/lenisko/k400_plus/master/k400_plus_conf.c > /tmp/k400_plus_conf.c
gcc /tmp/k400_plus_conf.c -o /tmp/k400_plus_conf
rm /tmp/k400_plus_conf.c
sudo mv /tmp/k400_plus_conf /usr/local/sbin/k400_plus_conf
sudo chmod +x /usr/local/sbin/k400_plus_conf
```

### 2. Systemd service & timer for automation uppon start, sleep/hibernation wakeup
```
sudo curl https://raw.githubusercontent.com/lenisko/k400_plus/master/k400_plus.service > /etc/systemd/system/k400_plus.service
sudo curl https://raw.githubusercontent.com/lenisko/k400_plus/master/k400_plus.timer > /etc/systemd/system/k400_plus.timer
sudo systemctl enable --now k400_plus.service
sudo systemctl enable --now k400_plus.timer
```

### 3. Script for enabling wake-up event on K400 Plus keyboard

We need `enable-wakeup` under `/usr/local/sbin/enable-wakeup` so just follow tutorial from [this](http://bernaerts.dyndns.org/linux/74-ubuntu/220-ubuntu-resume-usb-hid) site.
```
sudo curl https://raw.githubusercontent.com/lenisko/k400_plus/master/90-k400-plus-set-wake-up.rules > /etc/udev/rules.d/90-k400-plus-set-wake-up.rules
sudo udevadm control --reload-rules
```
