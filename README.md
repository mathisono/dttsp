# dttsp
This is a program that implements a Software-Defined Radio

This repository is a fork of the author's SVN repository.  The 'svn info'
of that repository at the time of check-out was:

Path: .
URL: https://www.cgran.org/cgran/projects/dttsp/branches/ab2kt/sdr-core/base
Repository Root: https://www.cgran.org/cgran
Repository UUID: 948f8045-528a-dd11-95b9-00e08143843c
Revision: 318
Node Kind: directory
Schedule: normal
Last Changed Author: ab2kt
Last Changed Rev: 233
Last Changed Date: 2009-02-04 06:08:38 -0600 (Wed, 04 Feb 2009)


Packages needed to build dttsp:

sudo apt-get install automake build-essential subversion 
sudo apt-get install libfftw3-dev jackd2 libjack-jackd2-dev 
sudo apt-get install liblo-dev libgsl0-dev
When installing jack, answer 'yes' to the question about setting up real-time priorities.

In the src dir/ run "biuld"

Packages needed to build usbsoftrock:

sudo apt-get install libusb++-dev libncurses5-dev

Packages needed to build ?????:

Packages needed to build sdr-shell:

https://github.com/glenoverby/sdr-shell-v4

sudo apt-get install qt4-qmake libqt4-dev 
sudo apt-get install libhamlib++-dev pkg-config

Run 'qmake-qt4' to build the Makefile, then 'make' to build sdr-shell.

Add yourself to the audio and video groups in /etc/group.

sudo usermod -G audio -a sudo usermod -G video -a
If you did not answer 'yes' to the jack installation question about real-time priorities, you may reconfigure it for real-time priorities with:
sudo dpkg-reconfigure -p high jackd
Configure udev to set usbsoftrock permissions (see below)

All Linux Systems

The following udev rules works well to allow the group softrock to use usbsoftrock without root privileges. You can put it in /etc/udev/rules.d and call it softrock.rules.

Fedora 9:

BUS=="usb", ACTION=="add", SSSYSFS{idVendor}=="16c0", SYSFS{idProduct}=="05dc",MODE="660", GROUP="softrock"

Fedora 12+, openSUSE 11+, Ubuntu 9.10+:

SUBSYSTEM=="usb", ACTION=="add", ATTR{idVendor}=="16c0", ATTR{idProduct}=="05dc", MODE="0660", GROUP="admin", SYMLINK="softrock"
the group "softrock" must exist in /etc/group, or substitute another group name.

