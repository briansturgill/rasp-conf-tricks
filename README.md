# rasp-conf-tricks
## Raspberry Pi Configuration Tricks

The raspi-config program can be used in a non-interactive mode to script changes, this is much faster than
going through the menus. Unfortunately, these are not documented. By reading through the raspi-config shell script I have figured out those that I needed. Any function in raspi-config can be called, so look through /usr/bin/raspi-config with a
text editor if you need other functions.

In all instances, the syntax is:

&nbsp;&nbsp;&nbsp;&nbsp;<tt>raspi-config nonint [<i>raspi-config_function_name</i> [<i>args ...</i>]]</tt>

### Functions I've tested:
### Change timezone
```sh
raspi-config nonint do_change_timezone "America/Denver"
```
For other timezone names see: <tt>/usr/share/zoneinfo</tt>

### Change locale
```sh
raspi-config nonint do_change_locale en_US.UTF-8
```
For other locale names run from the shell: <tt>cut -f 1 -d ' ' /usr/share/i18n/SUPPORTED | more</tt>

### Configure keyboard type
```sh
raspi-config nonint do_configure_keyboard us
```
For other locale names run from the shell: <tt>cut -f 1 -d ' ' /usr/share/i18n/SUPPORTED | more</tt>

### Configure wifi country
```sh
raspi-config nonint do_wifi_country US
```
For other country names see: <tt>/usr/shar/zoneinfo/iso3166.tab</tt>

### Functions I've figured out, but not tested:
### Change timezone
```sh
raspi-config nonint do_wifi_ssid_passphrase "Your_SSID" "Your PassPhrase"
# If you do this, then do:
chmod 600 /etc/wpa_supplicant/wpa_supplicant.conf
# raspi-config improperly protects this file as publically readable.

```
For other timezone names see: /usr/share/zoneinfo


## Information on configuing a headless-Pi.

Start with the official information at: https://www.raspberrypi.org/documentation/configuration/wireless/headless.md

Basically, after running etcher to build your sd card, remount the disks (remove and reinsert it).

On the _BOOT_ partion:
```sh
cd /path/to/boot/partition
touch ssh
cat > wpa_supplicant.conf <<EOF
country=us
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
 ssid="<Name of your WiFi>"
 psk="<Password for your WiFi>"
}
EOF
```

If you want static addresses for your machines edit _ON_THE_ROOT_ (not BOOT), edit the file <tt>etc/dhcpd.conf</tt> and
add the required information as you normally would.
