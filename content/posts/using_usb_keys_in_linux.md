---
date: '2025-04-04T07:26:20-04:00'
draft: false
title: 'Using USB keys in Linux'
cover:
    image: img/ventoy_usb_can_now_safely_be_removed.webp
    alt: "Ventoy USB key can now be removed"
    caption: "USB keys need to be safely removed"
tags: ["Linux","Xubuntu","Linux Mint","Hardware","USB KEY","Flash Drive", "USB Drive", "USB","Safely Remove","Eject"]
categories: ["Linux","Hardware"]    
---

### Don't physically remove a USB key without unmounting or ejecting it first

I have destroyed my fair share of USB keys in the past by prematurely removing the key before it was *safe* to do so. I remember being particularly irked when my $70CDN 1GB Kingston flash drive stopped working. I think at the time I swore I'd never buy Kingston crap again, but I'm not so sure it was ever Kingston's fault (to be fair, USB keys were fairly new on the market back then). Like a lot of people, I assumed you could just save a document, or copy your files over, and then pull the USB drive out. Maybe this was just a bad habit I picked up from my days of removing floppy disks (they never got corrupted either)?

### Unmounting, Safely Removing, Ejecting via the file manager is a first step

Properly removing a USB key/flash drive is actually a really easy task. Most of the time it simply involves opening a file manager session (I use Xubuntu at home and we use Linux Mint XFCE at The Working Centre's Computer Recycling Project, both of which use the Thunar file manager) and clicking the ejection symbol beside the USB key you're trying to remove, then waiting for a message indicating that the **Device can be removed.**. 

> It's important to note that sometimes after you click the eject symbol a message may appear instructing you **Not to remove the device because it still has writing to do**. It's easy to think you can pull the key when a message appears in the top right, but be patient and make sure it's the correct message.

### What if the device cannot be removed?

There are instances where Linux distrubutions will warn you that a USB key can not be unmounted or safely removed. In these instances the issue is usually that some file is open on the drive. The following screenshot shows a message indicating **Volume is busy**, with a sub-message that says **one or more applications are keeping the volume busy**. In this case the reason the key cannot be ejected is because the screenshot/picture to the right is opened, and that screenshot/picture is a file that lives on the flash drive that I'm trying to eject.

![Volume is busy](/img/usb_volume_is_busy.webp)<figcaption>Fig 1. Volume is busy because a file is open from the USB key</figcaption>

I've seen this happen a lot where people have a resume from their flash drive open in a word processor. If you **Eject Anyway** you run the risk of corrupting the resume, and the USB key. The solution is to close the program, and try ejecting the key after the program closes. In the example above I found the key unmounted the moment I closed the screenshot/picture (which was preventing it from unmounting because it was open).

In some cases I've also found that the issue was I had a terminal window open and was running a program in a terminal, while in the directory/path of the USB key (usually something like /media/label).




