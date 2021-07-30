# PiWiFiSetup

PiWiFiSetup is a program to headlessly configure a Raspberry Pi's WiFi
connection using any other WiFi-enabled device (much like the way
a Chromecast or similar device can be configured).

It was tested on Raspberry Pi 3B+ with debian buster

If is based on the wonderful work of Jason Burgett <https://github.com/jasbur/RaspiWiFi>

However there are some key diffrences:

- It is inteded to work as a standalone app launching any dependencies like
 hostpad and dnsmasq as subprocesses and stoping them on finish.

- It doesn't restart the device, just setups the wifi and exits.

- It doesn't regenerate wpa_supplicant.conf on every run but instead just edit
 the first instance of a network={} block and leave every other setting intact.

- There is no installation script and the decision on when to run the app depends
 entirelly on the user/implementator

- When you connect to the AP it would act as a captive portal and take you to the
 configuration page without the need to open a specific address

## INSTALLATION

On debian buster to setisfy the dependencies you need to run:

``` bash
apt install python3-flask dnsmasq hostapd
```

## CONFIGURATION

You can create a file in the apps directory called PiWiFiSetup.conf and set the following settings

- ssid_prefix - defaults to "Pi Wifi Setup"
- wpa_enabled - 0/1 defaults to 1
- wpa_key     - defaults to "1234567890"
