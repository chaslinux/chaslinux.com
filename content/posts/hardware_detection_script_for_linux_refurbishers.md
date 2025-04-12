---
date: '2023-02-15T14:29:08-04:00'
draft: false
title: 'Hardware detection script for Linux refurbishers'
cover:
    image: img/hardwaresh_script.webp
    alt: "The PDF that gets created showing the hardware specifications"
    caption: "Hardware specifications PDF for an Acer AT3-710 desktop"
tags: ["BASH","Hardware","Linux","Shell Script","Computer Refurbishing","Xubuntu","Linux Mint","Computer Recycling","Programming","PDF"]
categories: ["Computer Refurbishing","Hardware","Linux","Programming"]
---

### About the script

I wrote the hardware.sh BASH script to make it a bit simpler for volunteers at The Working Centre’s [Computer Recycling Project](https://www.theworkingcentre.org/cr/) to figure out what hardware was in a computer. For more than a dozen years we’ve been asking volunteers to gather information from the BIOS, or using phoronix-test-suite under our PXE booted Debian Live environment. Volunteers would write the information on quarter page-sized sheets we would attach to each computer. While this was a useful function to help volunteers get to know hardware in a computer, there were a few problems with this method:

- Not everyone prints legibly. Some of the “spec” sheets were difficult to read, with 8’s being confused with 0’s, 9’s and 4’s being confused, and so on.
- Information wasn’t always accurate. Mistakes were made transferring between what phoronix-test-suite suggested and what was written on the paper.
- Inconsistent amounts of information were being written down. One person would fill out a spec sheet completely, while another would leave sections blank.
- The Serial Number of an OEM was often left off the sheets. We used these serial numbers in our point-of-sale, having them on the spec sheets saved lots of time. Non-OEM systems don’t have a serial number, so we were having to show volunteers how to get the MAC address of the network card in a system to use as a serial number.

I also considered the fact that just reading off system information from [phoronix-test-suite](https://www.phoronix-test-suite.com/) really isn’t giving the volunteers the educational value of learning parts of the system. While this script doesn’t serve that purpose either, it does simplify a few things.

Hardware.sh installs a bunch of tools to query the computer it is run on. During the script, hardware.sh produces several files on the desktop of the currently logged-in user, which are deleted until 2 files remain, specs.tex and specs.pdf. Specs.tex is a [LaTeX](https://www.latex-project.org/) file which is used to create specs.pdf. While the LaTeX file isn’t needed, I use it sometimes to improve the script when people run into issues with the script.

The resulting PDF is a full 8 1/2 inch by 11 inch page with a significant amount of information:

- OEM manufacturer, model/product name, family, and serial number. For non-OEM systems some of these fields do not exist or are listed as “To be filled out by OEM.” I’ve written the script to set the serial number to the NIC MAC address of systems where there is no OEM.
- CPU manufacturer, model, core, and thread count. 
- RAM amount, maximum RAM capacity, and the type (for example: DDR3) of RAM.
- Graphics model, video RAM, and OpenGL support information (which can be useful for Linux games on Steam).
- Hard Drive manufacturer (model family), model, and capacity.
- DVD Drive information (this can be helpful if you run into issues where a DVD drive’s firmware might need to be updated).
- Network information, including wireless information.
- Sound information.

For laptop computers the PDF also includes:

- Battery design capacity, and the last full capacity of the battery.
- Resolution of the laptop LCD.

### Known bugs

Hardware.sh is far from perfect. There are several things I need to work on, and because OEM’s and manufacturers do not always fill out information fields about their products, the script cannot always give all the information above for every product.

For example: On a Lenovo ThinkPad X61 the script shows the RAM installed, maximum capacity, and the fact that the RAM is DDR2. On the Acer AT3-710 desktop I’m on hardware.sh shows the RAM installed, maximum capacity, the fact the RAM is DDR3, and the memory speed of the installed RAM.

For systems where manufacturer information is filled out as “To Be Filled Out By OEM” some areas will be lacking, or incorrect.

~~We only install 1 hard drive in most systems. Currently the script is limited to detecting only one drive. If you have multiple drives, only the first detected drive will be shown (unless it’s NVMe + HDD).~~

> **Update:** The script can now detect multiple hard drives, or one SSD/NVMe plus hard drives, but it still doesn't account for multiple SSDs.
> Our project receives so few SSD/NVMe drives that we don't build systems with multiple SSDs.

### Why so many dependencies?

When the script was originally developed, it only installed a handful of other programs. When I added the ability to embed a barcode (of the OEM serial number or MAC address if a custom build), that added dozens of extra dependencies to the script. Since the embedded barcode is one of the more handy features of the script the dependencies are staying.

### Why this script is useful?

Most hardware spec tools don’t cover the amount of information this script generates. It generates a barcode based either on the OEM serial number in the case of manufacturers like Dell, HP, Acer, or based on the MAC address of the network card for non-OEM systems. This barcode can be scanned with a hand scanner, making data entry into Point of Sale systems, or tracking systems, easier.

### Downloading and running the script

This script is intended to be run on Ubuntu-derived systems, but may work on other Debian-based systems with a bit of tweaking. Initially, the script was tested on Xubuntu 20.04 and 22.04, but has since been updated for Xubuntu 24.04.2 and Linux Mint from 21.3 to 22.1. I recommend running updates before running the script:

```shell
sudo apt update && sudo apt upgrade -y
```

First make a directory to hold the script. I’ve been working on several scripts for our project and have been putting all the scripts in a directory named code:

```shell
mkdir ~/Code
cd ~/Code
```

Next install git:

```shell
sudo apt install git -y
```

Then clone the hardware.sh github repository:

```shell
git clone https://github.com/chaslinux/hardware.sh
```

Now change into the hardware.sh directory and run the script:

```shell
cd hardware.sh
./hardware.sh
```

Note: if the above doesn’t work try:

```shell
cd ~/Code/hardware.sh
./hardware.sh
```

If that still doesn’t work, check to see that you cloned the hardware.sh directory inside the ~/Code directory. If the script doesn’t run check it has execute permission: ``chmod ugo+x hardware.sh``. It should have all these by default, but with the heavy changes I sometimes forget to ensure the script has execute permission.

> **Note:** do not run this script with sudo! The script will prompt when a sudo password is needed. The user running the script must have sudo access, but the script should be run as that user, not with sudo in front of the script.

The script may take a bit to work. One of the first things it does it update all the packages on a system.

If this script is useful for your project I’d love to hear from you on Mastodon: [@chaslinux@techhub.social](https://techhub.social/@chaslinux)

> **Note:** It’s also worth mentioning that the script does not look for SCSI drives. As I understand it modern SCSI drives use /dev/sg*. I may add this in the future, but we mostly work with desktop systems and don’t expect to put a desktop OS on a machine with SCSI drives since they’re often in servers. We have some systems with SCSI drives, so I may consider adding support for this in the future.

