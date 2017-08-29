This repository can be used to create an ArchLinuxARM image for the NanoPi Neo2
board.


Dependencies
============

- `make`
- `bsdtar` (`libarchive`)
- `python2`
- `uboot-tools`


Prerequisite
============

In order to build the image, you need a working ARM toolchain.

Here is a simple way to get one:

    git clone https://github.com/crosstool-ng/crosstool-ng
    cd crosstool-ng
    ./bootstrap
    ./configure --enable-local
    make
    ./ct-ng aarch64-unknown-linux-gnu
    ./ct-ng build


Preparing the files
===================

Run `make` (specifying jobs with `-jX` is supported and recommended).

This will provide:

- the ArchLinuxARM aarch64 default rootfs (`ArchLinuxARM-aarch64-latest.tar.gz`)
- an u-boot image compiled for the NanoPi Neo2 (`u-boot-sunxi-with-spl.bin`)
- a boot script (`boot.scr`) to be copied in `/boot`


Installing the distribution
===========================

This is similar to any other AllWinner ArchLinuxARM installation: pick any from
https://archlinuxarm.org/platforms/armv7/allwinner/.

In 4 steps:
- create and format one ext4 partition
- untar the rootfs into it
- dd the u-boot image at offset 8192
- copy the boot script in the `/boot` partition


Ethernet
========

In order to get ethernet working, you will need a recent kernel (>= 4.13).  At
the time I'm writing these lines, the latest stable is 4.12. Though, you can
grab the [kernel RC package from ArchLinux ARM][linux-rc] and install it from
the serial interface.

[linux-rc]: https://archlinuxarm.org/packages/aarch64/linux-aarch64-rc


Goodies
=======

If you have a serial cable and `miniterm.py` installed (`python-pyserial`),
`make serial` will open a session with the appropriate settings.


TODO
====

- remove u-boot patches when mainlined
- upstream to ArchLinuxARM


U-Boot patches status
=====================

Both patches are merged upstream, waiting for the next release including them.
