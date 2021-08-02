# PiWiFiSetup

PiWiFiSetup is a program to headlessly configure a Raspberry Pi's WiFi
connection using any other WiFi-enabled device (much like the way
a Chromecast or similar device can be configured).

It was tested on Raspberry Pi 3B+ with debian buster

If is based on the wonderful work of Jason Burgett <https://github.com/jasbur/RaspiWiFi>

However there are some key differences:

- It is intended to work as a standalone app launching any dependencies like
 hostpad and dnsmasq as sub-processes and stopping them on finish.

- It doesn't restart the device, just setups the WiFi and exits.

- It doesn't regenerate wpa_supplicant.conf on every run but instead just edit
 the first instance of a network={} block and leave every other setting intact.

- There is no installation script and the decision on when to run the app depends
 entirely on the user/integrator

- When you connect to the AP it would act as a captive portal and take you to the
 configuration page without the need to open a specific address

## PACKAGING

To build a .deb package that you can install directly you can run:

``` bash
dpkg-buildpackage -us -uc -b
```

The package would then be in the parent directory

## INSTALLATION

If you have build a package all you need to do is install it:

``` bash
apt install ./pi-wifi-setup_*_all.deb
```

Or you can install only the required packages.
On debian buster to satisfy the dependencies you need to run:

``` bash
apt install python3-flask dnsmasq-base hostapd
```

## CONFIGURATION

You can create a file in the apps directory called PiWiFiSetup.conf and set the following 
 settings showed here with their defaults

``` config
ssid_prefix="Pi Wifi Setup"
wpa_enabled=1
wpa_key="1234567890"
```
