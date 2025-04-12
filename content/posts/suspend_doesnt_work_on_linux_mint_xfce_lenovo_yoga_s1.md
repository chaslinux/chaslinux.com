---
date: '2024-11-13T12:38:06-04:00'
draft: false
title: "[Fix] Suspend doesn\'t work on Linux Mint XFCE Lenovo Yoga S1"
cover:
    image: img/linux_mint.webp
    alt: "Linux Mint XFCE desktop"
    caption: "Running the update manager on Linux Mint XFCE"
tags: [""]
categories: [""]
---

### Suspend doesn’t work on some Linux distributions – Lenovo Yoga S1

Our experience with Linux Mint XFCE has been pretty good so far at The Working Centre’s Computer Recycling Project, but we recently ran into an issue where a couple of Lenovo Yoga S1 laptops refused to suspend when the suspend button was clicked.

Now before someone goes on about Linux, I want to point out a couple of things:

- The issue does not happen in Fedora 41 Workstation, nor does it happen in Xubuntu 24.04.1.
- Windows has it’s own issues with software that should work, but doesn’t because of some quirk/bug (having been with the project for 23 years I’ve seen a lot of issues on different OS’s)

There are several threads relating to the issue, but the one that worked (with some modifications) for us was: (https://forums.linuxmint.com/viewtopic.php?t=391671)

### Test, test, and more testing

We tried several different potential solutions to fix the issue before finally finding the thread above. Things we tested were:

- Updating all software
- Changing to the latest kernel available for Linux Mint 21.3 (virginia)
- Installing Linux Mint XFCE version 22 (Wilma)
- In the BIOS changing USB so that ALWAYS ON USB was disabled.

Other threads gave a hint as to the culprit, and actually mentioned the solution, but didn’t mention how they went about the solution: (https://forums.linuxmint.com/viewtopic.php?t=411541)

We also tried Fedora Workstation 41 (which, by the way looked pretty stunning on the Yoga S1), and Xubuntu 24.04.1, both of which suspended properly when we clicked the suspend button. We also confirmed that the issue did not happen on the dozen other models of laptops we had on display with Linux Mint XFCE 21.3/22 installed. (So this wasn't a general bug across other Lenovo ThinkPads and Linux Mint)

### XHC – The culprit

Both of the laptops we ran into this issue on were Lenovo ThinkPad S1 Yogas with Intel Core i7-4600 CPUs, 8GB DDR3 SO-DIMM RAM, and 256GB Samsung SSDs. The S1 Yogas are nice little laptops with a 1920×1080 resolution screen, and a pen that can be used with the touch screen.

The first URL mentioned at the top mentions both XHC and XHCI. The thread makes suggestions that don’t work on the Yoga S1 as one of the methods results in a permission error, and the other indicates XHCI is the issue. On the Yoga S1s we have at the shop XHC is the culprit.

Solution – Creating a startup script to disable XHC, enabling, and starting the script on startup

The solution that worked for us is a combination of what both Karsti and t42 wrote in the thread. Create a text file called **usb-wakeup.service**. In that file paste the following:

```shell
[Unit]
Description=Disable wakeup events

[Service]
ExecStart=/bin/bash -c "echo XHC > /proc/acpi/wakeup"
Type=oneshot

[Install]
WantedBy=multi-user.target
```

The main difference between this and t42’s script is the changed ExecStart line. t42’s example uses XHC0, instead of XHC. This doesn’t work for our S1 Yoga.

Next be sure to set execute permission on the usb-wakeup.service file:

```shell
chmod ugo+x usb-wakeup.service
```

Once you’ve created the file copy it to the /etc/systemd/system directory:

```shell
sudo cp usb-wakeup.service /etc/systemd/system/
```

Finally, enable the service and start it:

```shell
sudo systemctl enable usb-wakeup.service
sudo systemctl start usb-wakeup.service
```

Now suspend should work. Reboot, and as long as you’ve run the enable line, the fix should work every time. If you’re using a different machine, XHC might be XHC0. See the second URL mentioned above for the complete thread.