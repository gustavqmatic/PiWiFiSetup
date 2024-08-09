# PiWiFiSetup

PiWiFiSetup is a program to headlessly configure a Raspberry Pi's WiFi
connection using any other WiFi-enabled device (much like the way
a Chromecast or similar device can be configured).

It was tested on Raspberry Pi Zero 2 with Raspberry Pi OS around summer 2024.
It include some fixes liek using nmcli instead of wpa_supplicant and turning
off Flask not using the depricated shut off script.


It is based on the wonderful work of Lukanet <https://github.com/Lukanet> and
Jason Burgett <https://github.com/jasbur/RaspiWiFi>
Update to use nmcli from https://github.com/muharremtac/BilirWiFi

However there are some key differences:

- It is intended to work as a standalone app launching any dependencies like
 hostpad and dnsmasq as sub-processes and stopping them on finish.

- It doesn't restart the device, just setups the WiFi and exits.


- There is no installation script and the decision on when to run the app depends
 entirely on the user/integrator

- When you connect to the AP it would act as a captive portal and take you to the
 configuration page without the need to open a specific address

## PACKAGING

To build a .deb package that you can install directly you can run:

``` bash
sudo apt-get install debhelper python3-all dh-python
dpkg-buildpackage -us -uc -b
```

The package would then be in the parent directory

## INSTALLATION

If you have build a package all you need to do is install it:

``` bash
apt install dnsmasq dhcpcd
apt install ./pi-wifi-setup_*_all.deb
```

Or you can install only the required packages.
On debian buster to satisfy the dependencies you need to run:

``` bash
apt install python3-flask dnsmasq-base hostapd
```

In the package are included .service and .timer systemd control files.
The service would only start if there isn't any connection in state UP.
The timer would run only once after boot.
You can override those defaults using:

``` bash
systemctl edit pi-wifi-setup.service
systemctl edit pi-wifi-setup.timer
```

## CONFIGURATION

The configuration file the app uses is /etc/PiWiFiSetup/PiWiFiSetup.conf.
The file can be missing in which case the defaults are as follows:

``` config
ssid_prefix=Pi $id Wifi Setup
wpa_enabled=1
wpa_key=1234567890
```

The $id is replaced with the serial-number of the device
In case you save the file via the web interface it would be update or created if missing.
