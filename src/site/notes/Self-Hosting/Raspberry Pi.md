---
{"dg-publish":true,"permalink":"/self-hosting/raspberry-pi/"}
---

# Raspberry Pi

## Discussion
I looked at self-hosting using a [Virtual Private Server (VPS)](https://en.wikipedia.org/wiki/Virtual_private_server), but there's a saying in the security community: "If you can touch it, can own it." Basically, if somebody at a VPS vendor wants to load malware on a server I'm hosting on their system, there's absolutely no way for me to keep it from happening. I really like the processing power vs electrical power draw of Raspberry Pi devices, so I decided to put together a Raspberry Pi with a large amount of storage for the house and another at a remote location for backups. Below is my first attempt at my personal VPS.
## Hardware
- [Raspberry Pi 5 (16GB)](https://www.amazon.com/dp/B0DSPYPKRG) - $129
- [Pi 5 Active Cooler](https://www.amazon.com/Raspberry-Pi-Active-Cooler/dp/B0CLXZBR5P) - $10
- [CanaKit 45W USB-C Power Supply](https://www.amazon.com/dp/B07H125ZRL) - $20
- [2-pack Sandisk Ultra 64GB MicroSDXC cards](https://www.amazon.com/dp/B07XDCZ9J3) - $16
- [Pimoroni dual-nvme base](https://www.amazon.com/NVMe-Raspberry-Extension-Board-Supported/dp/B0D4SGF2QT) - $40
- [Micro USB to USB adapter](https://www.amazon.com/dp/B09LYPXPH6) - $9
- [WD Black 2TB NVME SSD](https://www.amazon.com/dp/B0DN6ZQ3PD) - $129 x2 = $258
- [Pimoroni Base Case](https://www.pishop.us/product/nvme-base-case-for-raspberry-pi-5) - $21
Total cost (minus tax): $503.
## Configuration

### Raspbian onto SD

### Raspbian onto SSD

### Nextcloud
- https://snapcraft.io/install/nextcloud/raspbian

## Backups
Still figuring this part out. I want to use two forms of backup to easily recover if I have a catastrophic hardware failure. 
- The first backup type I want is a [disk image](https://en.wikipedia.org/wiki/Disk_image) backup that I can restore to new hardware.  This will only happen rarely when I make significant changes to the configuration of the Pi. While I can't easily take out the boot SSD (it sits on the Dual NVME bottom board, so I'd have to completely disassemble the Pi), one of the cool things I came across in this design ***insert link to configuration section here*** is that I can set the firmware to boot either off of the SD card or the NVME SSD. For production purposes I boot off of the NVME. For image backups I intend to change the firmware ^[insert link to configuration section here] to boot from the SD card and use utilities there to backup the partitions on the SSD.
- The second backup type is the normal stage, using rsync to backup data and settings and such for the installed system. I'll have to figure out each subsystem for this backup type. For instance, I'm using [nextcloud.export](https://github.com/nextcloud-snap/nextcloud-snap/wiki/How-to-backup-your-instance)
### Research
- image backup utilities
	- [PiSafe](https://github.com/RichardMidnight/pi-safe)
	- https://forums.raspberrypi.com/viewtopic.php?t=332000
	- [resize2fs](https://linux.die.net/man/8/resize2fs) 
	- [PiShrink](https://github.com/Drewsif/PiShrink)
- file backup utilities
	- 
## References
- https://shop.pimoroni.com/products/nvme-base-duo-for-raspberry-pi-5?variant=41434434895955