---
title: Install Wifi Adapter Drivers for Ubuntu
date: 2020-12-18
categories: technology
---

One of the annoyance I have with using Ubuntu is installing the right drivers for wifi adapters. Some adapters work out of the box without any issue but others require installing additional drivers. This post will be a list of what drivers to install for different adapters I own. For reference, my Ubuntu version is 20.04 LTS but it might also work for other versions.

<!--more-->

1. 

2. [TP-Link TL-WN725N V1](https://www.tp-link.com/us/home-networking/usb-adapter/tl-wn725n/)

<p align="center">
  <img width="125" src="https://i.imgur.com/fgVhixi.jpg" alt="Forest App Interface">
</p>

[Original answer](https://askubuntu.com/questions/678134/how-to-install-tp-link-wn725n-wifi-usb-adapter-on-ubuntu-ubuntu-14-04-3-lts) on Ask Ubuntu:

```shell
sudo apt-get update
sudo apt-get install linux-headers-$(uname -r)
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install git
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

The speed is definitely slower and connection can be spotty at best. But at least the adapter is working.

