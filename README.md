#Logitech K400 Plus - Linux helper scripts

###1. Script for Fn keys switch

__k400_plus_conf.c__ is modded version of [k810_conf.c](http://www.trial-n-error.de/posts/2012/12/31/logitech-k810-keyboard-configurator).
```
curl https://raw.githubusercontent.com/lenisko/k400_plus/master/k400_plus_conf.c > /tmp/k400_plus_conf.c
gcc /tmp/k400_plus_conf.c -o /usr/local/sbin/k400_plus_conf
chmod +x /usr/local/sbin/k400_plus_conf
```

###2. Script for wake-up enabling

We need `enable-wakeup` under `/usr/local/sbin/enable-wakeup` so just follow tutorial from [this](http://bernaerts.dyndns.org/linux/74-ubuntu/220-ubuntu-resume-usb-hid) site.

###3. udev rules

####3.1 Auto enable (normal) fn keys for keyboard
```
curl https://raw.githubusercontent.com/lenisko/k400_plus/master/90-k400-plus-set-fn-keys.rules > /etc/udev/rules.d/90-k400-plus-set-fn-keys.rules
udevadm control --reload-rules
```

####3.2 Auto enable wake-up for keyboard
```
curl https://raw.githubusercontent.com/lenisko/k400_plus/master/90-k400-plus-set-wake-up.rules > /etc/udev/rules.d/90-k400-plus-set-wake-up.rules
udevadm control --reload-rules
```
