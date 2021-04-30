---
title: Install Wifi Adapter Drivers for Ubuntu
date: 2020-12-18
categories: technology
---

One of the annoyance I have with using Ubuntu is installing the right drivers for wifi adapters. Some adapters work out of the box without any issue but others require installing additional drivers. This post will be a list of what drivers to install for different adapters I own. For reference, my Ubuntu version is 20.04 LTS but it might also work for other versions.

<!--more-->

## [Asus USB-N10](https://www.asus.com/us/Networking/USBN10/)

{% include image.html url="https://i.imgur.com/uiX8toW.jpg" text="Forest App Interface" %}

This is one of the rare adapters that is compatible with Ubuntu from the start. I've been using this adapter since 16.04 for multiple devices and it has never given me any issue. It's the fallback for me when I install Ubuntu on a new device without a nearby Ethernet cable. If you just want an adapter that works, get this.

## [TP-Link TL-WN725N V1](https://www.tp-link.com/us/home-networking/usb-adapter/tl-wn725n/)

{% include image.html url="https://i.imgur.com/fgVhixi.jpg" text="Forest App Interface" %}

### RTL8188EU

[Ask Ubuntu answer](https://askubuntu.com/questions/678134/how-to-install-tp-link-wn725n-wifi-usb-adapter-on-ubuntu-ubuntu-14-04-3-lts):

```shell
sudo apt-get update
sudo apt-get install linux-headers-$(uname -r)
sudo apt-get update
sudo apt-get install build-essential git
git clone https://github.com/lwfinger/rtl8188eu
cd rtl8188eu
make all
sudo make install
sudo modprobe 8188eu.ko
```

But the last command did not work for me:

```shell
sudo modprobe 8188eu.ko
modprobe: FATAL: Module 8188eu.ko not found in directory /lib/modules/5.4.0-58-generic
```

What I did instead was:

```shell
cd /lib/modules/5.4.0-58-generic/kernel/drivers/net/wireless
sudo insmod 8188eu.ko
reboot
```

I have been having some issues with this driver. The connection is slow and spotty at best. It's better to use RTL8192EU instead.

### RTL8192EU

This driver increased the speed of my connection significantly.

[ clnhub/rtl8192eu-linux README](https://github.com/clnhub/rtl8192eu-linux):

```shell
sudo apt install linux-headers-generic build-essential dkms git
git clone https://github.com/clnhub/rtl8192eu-linux.git
cd rtl8192eu-linux/
./install_wifi.sh
reboot
```

## [Tenda U12](https://www.tendacn.com/us/product/u12.html)

{% include image.html url="https://i.imgur.com/uLDAHmp.jpg" text="Forest App Interface" %}

[ gordboy/rtl8812au-5.9.3.2 README](https://github.com/gordboy/rtl8812au-5.9.3.2):

```shell
sudo apt install build-essential git dkms
git clone https://github.com/gordboy/rtl8812au-5.9.3.2.git
cd rtl8812au-5.9.3.2/
make
sudo make install
cd ..
sudo cp -r rtl8812au-5.9.3.2/ /usr/src
sudo dkms add -m rtl8812au -v 5.9.3.2
sudo dkms build -m rtl8812au -v 5.9.3.2
sudo dkms install -m rtl8812au -v 5.9.3.2
```

Run `sudo gedit /etc/NetworkManager/NetworkManager.conf` and add the lines below if they're not there:

```shell
[device]
wifi.scan-rand-mac-address=no
```

Reboot and it should work.

The problem with this adapter is that it sometimes doesn't pick up the 5 Ghz band. It's better just to use 2.4 Ghz so you don't encounter any connection issue.