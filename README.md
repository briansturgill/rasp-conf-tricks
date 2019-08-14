# rasp-conf-tricks
Raspberry Pi Configuration Tricks

Information on speeding up configuring your Pi.

  TODO

Information on configuing a headless-Pi.

  TODO

For the moment, I'll just list the script from the talk:
```bash

raspi-config nonint do_change_locale en_US.UTF-8

raspi-config nonint do_configure_keyboard us

raspi-config nonint do_wifi_ssid_passphrase "Your_SSID" "Your PassPhrase"

# Then:

chmod 600 /etc/wpa_supplicant/wpa_supplicant.conf

# raspi-config leaves it publically readable!


--- To boot into ssh headlessly:
touch $SDCARD_BOOT_MOUNT/boot/ssh
# Copy a copy a correct wpa_supplicant.conf file to $SDCARD_BOOT/boot
#If you need to set a static address:
# Edit $SDCARD_ROOT_MOUNT/etc/dhcpcd.conf
# Note this on is on the ROOT mount, not the BOOT mount.
```
