---
date: '2023-03-27T13:58:08-04:00'
draft: false
title: 'A Linux BASH shell script to create a PDF of monitor information - findmonitor.sh'
cover:
    image: img/findmonitor.webp
    alt: "The PDF created by the script of monitor information"
    caption: "PDF of monitor information"
tags: ["Computer Refurbishing","Hardware","Display","Monitor","Programming","BASH","Shell Script","DVI"]
categories: ["Computer Refurbishing","Hardware","Programming","Linux"]
---

### About findmonitor.sh

> **Note:** Note: This script is NOT compatible with systems running Wayland. We use Xubuntu Linux at our project. 

The Working Centre’s not-for-profit [Computer Recycling Project](https://www.theworkingcentre.org/cr/) sometimes receives donations of many monitors all at once. Our previous method for handling monitors was to set them up, run them through a bunch of tests, print a label on our label printer, and enter the monitor into our point of sale. This method hasn’t worked very well for us when we’ve received a lot of monitors all at once. Large amounts of monitors were sitting untested for awhile because we didn’t have the resources to do the old process for each monitor. We needed a faster way to figure out some of the details of monitors, and make them easier to sell without needing to create labels and enter everything into the point of sale.

![A monitor with both the old and new script results](/img/findmonitor-result.webp)<figcaption>Fig 1. Updated version of the script adds a price</figcaption>

Enter my findmonitor.sh script available on github at: (https://github.com/chaslinux/findmonitor/). The findmonitor.sh Linux BASH shell script uses a couple of tools, xrander and ddcutil, to create a PDF on the user’s desktop with information about the monitor connected to the system.

### Benefits of using the script

If you have to process a bunch of monitors, findmonitor.sh can be quite handy. The script produces a PDF that includes the manufacturer name, model of the monitor, maximum resolution, and sometimes includes information about the connections on the monitor (this depends on ddc information, which not all monitors support). The PDF also has a barcode that’s produced based on the serial number of the monitor. This comes in really handy because you can use a barcode reader to scan the barcode into your point of sale, or spreadsheet, making data entry simpler.

The findmonitor.sh shell script collects EDID and DDC information from monitors. The script then produces a single letter-size page PDF with a box around the following monitor information:

- Manufacturer
- Model
- Serial Number
- Resolution
- Date of manufacture

If the monitor also supports DDC, and the DDC information is correctly filled out by the manufacturer in the monitor’s firmware, it will show the inputs on the back: VGA/DVI/HDMI, DisplayPort.

The script also takes information from the monitor’s Serial Number and produces a barcode, making it easy to input into a Point-Of-Sale system.

As of this post, the script now also produces a price in the top right corner, based on the size of the monitor. In the script I’ve set prices as:

- 24" - $30
- 22" - 23" - $20
- 20" - 21" - $10
- 17" - 19" - $5
- anything unrecognized or smaller gets a $SEE STAFF price

All these are easily changeable in the script. The feature image at the top of this post shows changes between the old version (left) and the new version (right).

### Shortcomings of the script

Currently the script has several shortcomings. Some of the problems involve garbage in, garbage out situations where manufacturers don’t fill out EDID information about their monitors. For example, there’s a field for serial number, that often isn’t filled out by manufacturers, so the resulting serial number isn’t always accurate. Of course this also means the barcode may end up not being what’s expected. There are a couple of fields for serial number, if a manufacturer doesn’t fill out the main serial number field, the script looks at another serial number field, which isn’t the normal one on the back of the monitor, but should be unique.

Another shortcoming is that the script doesn’t always process monitors correctly without a reboot of the computer. We noticed this with monitors that ONLY had VGA connections. **Most monitors with DVI (except one or two) could be hot swapped, the script rerun, and new information generated for the new monitor.** We tested this with HDMI and it also seems to be okay for hot swapping, but check the resulting PDF just to make sure it isn’t the previous monitor.

This script is intended for desktop monitors, not laptops.

This script is also wasteful. The PDF it generates has a box in the middle of a page. What we do at the project is make a couple of cuts vertically and staple that normally wasted paper together to use as a message scratch pad beside out telephone. 

### Installing the script

The script is hosted on github. The simplest way to install the script is to clone it using git and do updates with git pull. First install git if you haven’t already:

```shell
sudo apt update
sudo apt install git
```

Next make a directory to clone the repository into. You can clone it into your home directory, but I like to clone things into a sub-directory. Making a sub-directory ensures you keep your home directory clean. I like to clone projects into a directory called Code.

```shell
mkdir ~/Code
```

Next, change into the directory where you want to put the findmonitor project and clone the project:

```shell
cd ~/Code
git clone https://github.com/chaslinux/findmonitor
```

This will make a directory called findmonitor inside the Code directory. In that ~/Code/findmonitor directory will be the findmonitor.sh script. Change into the directory and run the script:

```shell
cd ~/Code/findmonitor
./findmonitor.sh
```

If you’re unfamiliar with Linux, it’s important to note that Linux treats small and capital letters differently. So Code and code are different directories in Linux. If you’re used to Windows, this is one difference worth knowing. The first line changes into the ~/Code/findmonitor directory. Note: ~ is a shortcut for the currently logged in user’s home directory. If your username is chaslinux, cd ~ would take you to /home/chaslinux. If your username is linuxuser, cd ~ would take you to /home/linuxuser. Putting a period and forward slash in front of the findmonitor.sh script name tells the BASH shell to run the program.

Occasionally you may run into a situation where a script doesn’t run. I sometimes make a change that affects whether the program is run-able, and forget to set the executable bit. To make a script executable run the following command:

```shell
chmod ugo+x findmonitor.sh
```

> Note: you need to be in the directory findmonitor.sh is in, in order to set the executable bit. 

Chmod stands for change file mode. The u after chmod stands for user, g for group, and o for others. With the command above we are adding the +x executable bit to the user’s account, the group’s account, and any others. This means anyone who can access the directory can also execute the script. Be careful setting the execute bit on programs you don’t know, or don’t have access to the code to. Allowing any user to execute a program could be a vector into your system, particularly if you don’t know what the program does, but also if the program is written in a way that touches other parts of the system.

The findmonitor.sh script should be run as a non-root user, but with sudo access. On Ubuntu/Xubuntu/Kubuntu and other Ubuntu-derived distributions this is the first user you created. Don’t run the script with sudo, it will prompt you for the sudo password.

### Before running the script

Before you run findmonitor.sh, for best results run on monitors with a digital connection. This means DVI, DisplayPort, or HDMI. If you run on a system with DSUB/VGA be prepared to log-out or reboot each time, or the script will produce information for the last monitor.

**Be aware**: Not all manufacturers add all EDID or DDC information, but this script tries to make a best guess. Some manufacturers do no fill out the main serial number field, but use another serial number field. Or the serial number field is only partially filled compared to what you might find on the back of the monitor.

### Notes about the PDF

The PDF produced is a full page PDF for a single monitor. This is wasteful. What we do at our project is turn the page and cut the long strips of paper away from the rectangle. These long strips are then stapled together and used as scratch pads by our phone. The other small pieces are recycled in our paper recycling, or used as a quick price tag for something else.

### How price is determined

We’ve based price on monitor size. As mentioned earlier, we charge $30 for a 24″ monitor, $20 for a 22″ monitor, and so on. Sadly there is no EDID information that indicates monitor size. We use the monitor model as a best guess for the size of the monitor. For example: the Dell U221H monitor in the image is parsed as a 22″ monitor and gets a price of $20. The script trims the letters out of the model, then cuts the model to the first couple of characters. On some models this doesn’t work. For example: The BenQ FP951 is detected, but when the script parses this it ends up being read as 95, not a 19″ monitor, so a price of Price: $SEE STAFF is produced.

It’s not a perfect script, but it works for a lot of monitors. 

### Updates

When the script is updated on github it’s possible to get new updates by changing into the findmonitor directory and doing a git pull (provided you haven’t made your own changes):

```shell
cd ~/Code/findmonitor
git pull
```

I update the script from time to time. At the moment I’m just working on adding new monitor manufacturers, but I plan on adding support for other Linux distributions in the near future. Also, this script currently doesn’t work for systems running the Wayland display system.

### If you find findmonitor.sh helpful

If you find the findmonitor.sh script helpful, I’d love to hear from you. This project was started for our not-for-profit computer refurbishing project, but I’d love to see it get used elsewhere. Feel free to reach out to me via email, my email is in the script, or via Mastodon: [@chaslinux@techhub.social](https://techhub.social/@chaslinux).