This page documents using pure Debian on the Helios 4.

## Creating USB Installer
The process for creating a bootable usb installer for 32 bit arm platforms os fully documented in the 
[Debian Manual](view-source:https://www.debian.org/releases/buster/armhf/ch05s01.en.html#boot-installer-sd-image).

The short-hand is as follows:

- format a USB drive with either fat32 or ext4
- unpack [hd-media.tar.gz](http://http.us.debian.org/debian/dists/buster/main/installer-armhf/current/images/hd-media/hd-media.tar.gz) to the usb drive
- optional: download a [full XFCE CD](https://cdimage.debian.org/cdimage/buster_di_rc2/armhf/iso-cd/debian-buster-DI-rc2-armhf-xfce-CD-1.iso) to the usb drive

## Install
The only requirement for installing Debian is the availability of U-Boot somewhere on the device. Installing it once to SPI flash is recommended to avoid thinking about the bootloader ever again.

- Plug the prepared drive into one of the Helios-4 USB ports
- attach the serial console to a PC
- power on the device
- watch as Debian Installer starts up

If an operating system was already installed on any of the drives it may be necessary to force booting from USB:

- break into U-Boot console by pressing any key at the `Hit any key to stop autoboot` prompt
- specify boot order: `setenv boot_targets usb0 usb1`
- boot: `boot`

Finally follow the Instructions on the serial console for installing Debian.

## Known Issues
- Only one of the fans PWM signals can be controlled by software due to a limitation of the gpio-mvebu driver in linux. A patch is available [here](https://github.com/helios-4/linux-marvell/commit/743ae971934d0636e5e2be50fe09807974d0ce6d) but has yet to be upstreamed.
