---
{"dg-publish":true,"permalink":"/services-yet-to-be-implemented/backups/","updated":"2025-11-07T08:47:29.065-06:00"}
---

Still figuring this part out. I want to use two forms of backup to easily recover if I have a catastrophic hardware failure. 
- The first backup type I want is a [disk image](https://en.wikipedia.org/wiki/Disk_image) backup that I can restore to new hardware.  This will only happen rarely when I make significant changes to the configuration of the Pi. While I can't easily take out the boot SSD (it sits on the Dual NVME bottom board, so I'd have to completely disassemble the Pi), one of the cool things I came across in this design ***insert link to configuration section here*** is that I can set the firmware to boot either off of the SD card or the NVME SSD. For production purposes I boot off of the NVME. For image backups I intend to change the firmware ^[insert link to configuration section here] to boot from the SD card and use utilities there to backup the partitions on the SSD.
- The second backup type is the normal stage, using rsync to backup data and settings and such for the installed system. I'll have to figure out each subsystem for this backup type. For instance, I'm using [nextcloud.export](https://github.com/nextcloud-snap/nextcloud-snap/wiki/How-to-backup-your-instance)
### Research
- image backup utilities
	- [PiSafe](https://github.com/RichardMidnight/pi-safe)
	- https://forums.raspberrypi.com/viewtopic.php?t=332000
	- [resize2fs](https://linux.die.net/man/8/resize2fs) 
	- [PiShrink](https://github.com/Drewsif/PiShrink)