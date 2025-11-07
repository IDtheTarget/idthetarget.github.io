---
{"dg-publish":true,"permalink":"/self-hosting/platform/raspberry-pi/","updated":"2025-11-06T18:08:37.382-06:00"}
---

# Raspberry Pi

## Discussion
I looked at self-hosting using a [Virtual Private Server (VPS)](https://en.wikipedia.org/wiki/Virtual_private_server), but there's a saying in the security community: "If you can touch it, you own it." Basically, if somebody at a VPS vendor wants to load malware on a server I'm hosting on their system, there's absolutely no way for me to keep it from happening. I really like the processing power vs electrical power draw of Raspberry Pi devices, so I decided to put together a Raspberry Pi with a large amount of storage for the house and another at a remote location for backups. Below is my first attempt at my personal VPS.
## Hardware
- [Raspberry Pi 5 (16GB)](https://www.amazon.com/dp/B0DSPYPKRG) - $129
- [Pi 5 Active Cooler](https://www.amazon.com/Raspberry-Pi-Active-Cooler/dp/B0CLXZBR5P) - $10
- [CanaKit 45W USB-C Power Supply](https://www.amazon.com/dp/B07H125ZRL) - $20
- [# SanDisk 128GB MAX Endurance microSDXC](https://www.amazon.com/dp/B084CJ9T2R) - $25
- [Pimoroni dual-nvme base](https://www.amazon.com/NVMe-Raspberry-Extension-Board-Supported/dp/B0D4SGF2QT) - $40
- [Micro USB to USB adapter](https://www.amazon.com/dp/B09LYPXPH6) - $9
- [WD Black 4TB NVME SSD](https://www.amazon.com/dp/B0DZK9C789) - $250 x2 = $500
- [Pimoroni Base Case](https://www.pishop.us/product/nvme-base-case-for-raspberry-pi-5) - $21
Total cost (minus tax): $754. 

You can do this for a ***lot*** less (say, a Pi 4 with a spare SSD you may have lying around), but I prefer to buy the best I can afford at the time of a project  and then not have to worry about upgrades for 5-10 years. I guess I'm lazy.

I know that I could get a NUC for that much, but most of the cost was the storage, which I would still have had to purchase with another computer. I wanted as much storage as I could afford due to how many pictures my wife takes.

Because I'm using a custom base and case, I used the pointers from the [manufacturer on assembly](https://learn.pimoroni.com/article/assembling-nvme-case). 

One ***very*** cool thing about this setup. The Pimoroni dual-nvme base has a ribbon cable to connect the board to the Pi. That ribbon cable blocks access to the micro-SD card. At first I thought of that as a negative, since I always intended to boot from the NVME. It turns out to be a huge plus. What you'll see below is that I use Raspberry Pi Imager to initially configure the SD card, then put the Pi together. Then I VNC into the Pi and use the Raspbian version of the imager to image the NVME. Then I change a setting in the firmware and boot from the NVME.  The cool thing about leaving the SD card in is that I can change the firmware back to boot from the SD card and do an image backup of the environment on the primary NVME to the second one, then either rsync that image file to an offsite location or just copy it to a thumb drive. Either way, I have an image backup that's easy to restore in addition to the other backup methods I'll document as I implement them.
## Configuration

### Burn the Raspberry Pi OS onto the Micro-SD card
- Download [Raspbery Pi Imager](https://www.raspberrypi.com/software/). My [[Laptop/Laptop\|Laptop]] was still running Windows at the time, so I used the Windows version.
- Run the app
	- Choose Device: Raspberry Pi 5
	- Choose OS: Raspberry Pi OS (64-bit)
	- Choose Storage: SDXC Card - 127.9 GB
	- Click the "Next" button
	- Click the "Edit Settings"
	- Enter everything under "General" (I'm redacting my personal choices for security reasons)
	- Under "Services", enable SSH. If you have the knowledge, use the public-key authentication, it's more secure.
	- Click the "Save" button
	- Click the "Yes" button
	- Double-check that you've selected the SD card, then click the "Yes" button
	- When done, put the SD card into the Pi now. If you wait until you start the [assembly process](https://learn.pimoroni.com/article/assembling-nvme-case), you may forget. It's not easy taking it apart again, trust me.

### Assemble the parts and put into the case
- Assembly process [here](https://learn.pimoroni.com/article/assembling-nvme-case)

### Log into the Pi and update
**NOTE:** Everything in this section is updating the Micro-SD card. This is important for three reasons:
1. You're going to use the SD card to install Raspberry Pi OS on the NVME SSD, and you don't want problems with that process
2. The SSD is your "Recovery" system. If you end up with problems with the boot process on the NVME SSD, you can always revert to the Micro-SD for troubleshooting.
3. In order to do an image backup of the SSD environment, we're going to be booting back into the Micro-SD card. So we want it up-to-date.

- If you enabled 'ssh' in the Raspberry Pi Imager step above, then all you need is the IP address of your Pi. You can then use [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) to log in.
- I set up a DHCP reservation on my firewall/router. You can check for DHCP leases or use some other method, that process is really beyond the scope of this document
- Update everything
	- `sudo apt update`
	- `sudo apt upgrade -y`
	- `sudo reboot`
	- `sudo rpi-eeprom-update`
		- If the version shown isn't at least May 2024, then type `sudo raspi-config` and select "Advanced Options -> Bootloader Version" to update the eeprom. 
- Enable VNC
	- `sudo raspi-config`
		- Down-arrow twice to `Interface Options` and press the "Enter" key
		- Down-arrow twice more to "VNC" and press the "Enter" key again
		- Left-arrow to highlight "Yes", then press the "Enter" key again
		- Press the "Enter" key again to select "OK"
- Update the Bootloader
	- While in `raspi-config`
		- Down-arrow to "Advanced Options" and press the "Enter" key
		- Down-arrow to "Bootloader Version" and press the "Enter" key
		- Select "Latest" and press the "Enter" key
		- Press the "ESC" key to go back to the command line
### Burn the Raspberry Pi OS onto the NVME SSD
- "Getting Started" from pimoroni:
	- https://learn.pimoroni.com/article/getting-started-with-nvme-base-duo
- Check that the dual-NVME card is installed correctly:
	- `lsblk`
	- look for entries with 'nvme'. Mine show up as:
		- nvme0n1
		- nvme1n1
- Log onto the Raspberry Pi using VNC 
	- On my windows laptop I use the [RealVNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)
	- Just so that I know which environment I'm using, I change the desktop background for the two different installations. I use a red background for the MicroSD environment and a green background for the SSD environment. That way I know where I am.
- Click on the Raspberry at the top left
- Click on "Accessories" and then "Raspberry Pi Imager"
	- Raspberry Pi Device: Raspberry Pi 5
	- Operating System: Raspberry Pi OS (64-BIT)
	- Choose Storage: (it's hard to know which is 0 and which is 1, so I just pick the top one)
	- Edit your settings, then choose "yes" to burn to the SSD
- Set the Pi to boot from SSD
	- Down-arrow three times to "Boot Order"
	- Down-arrow once to "NVMe/USB Boot" and press the "Enter" key
	- Press the "ESC" key to get back to the command line
	- `sudo reboot`
- **NOTE:** You're now booting off of the SSD, so you'll have to go through [[Self-Hosting/Platform/Raspberry Pi#Log into the Pi and update\|Raspberry Pi#Log into the Pi and update]] again, or the next time you reboot you'll be back on the Micro-SD card.

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