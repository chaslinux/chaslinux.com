---
date: '2024-07-09T18:38:13-04:00'
draft: false
title: 'Linux on the Lenovo Thinkstation C20 (MT-M 4265-93u)'
cover:
    image: img/lenovo_thinkstation_c20.webp
    alt: "Lenovo ThinkStation C20"
    caption: "Lenovo ThinkStation C20 (released Q4 of 2010)"
tags: ["Computer Recycling","Computer Refurbishing","Linux Mint","Xubuntu","Hardware", "Lenovo"]
---

> **Note:** This is an older post, reposted from the old web site. The project has since mostly switched to Linux Mint XFCE 
> versions 21.3 (Virginia) and 22.1 (Xia). We still have Xubuntu 24.04.2 on our PXE server, but only install it on request.
> Our checklist has evolved and we've separated some steps into other checklists. 
> See my [github repositories](https://github.com/chaslinux) for more info.

### Workstation class hardware at a deeply discounted price

Every now and then the [Computer Recycling Project](https://www.theworkingcentre.org/cr/) at The Working Centre gets a really interesting piece of hardware donated. As a not-for-profit project, most of our equipment is aimed at people who are lower income. This generally translates into lower prices, even for some equipment others would list for a lot more. But that doesn’t mean the project just wipes the machines, installs Linux, and dumps the equipment on a sales shelf… often equipment requires a little, or a lot more work.

### Beyond the checklist

When Computer Recycling receives a computer, we normally either remove the hard drive and replace it with an already wiped drive, or wipe the drive on the spot in the case of solid state storage. Every computer that gets refurbished at Computer Recycling goes through a frequently changing [checklist](https://github.com/chaslinux/laptop-build-checklist) that’s broken down into a number of categories:

1. Computer Externals : the steps in this stage are mostly to determine if the computer is worth building.
2. First Boot : at this stage we turn on the computer, boot to our network server, and check that all fans are working.
3. Computer Specifications : using software on our PXE network boot server we check to make sure the system meets our minimum build specifications (currently 3rd gen i-Series with 8GB RAM).
4. Memory Test : all computers undergo a RAM test using Memtest86+ version 6.2. Once all RAM passes we move on to the next step. Any failed RAM sticks are replaced and the system is retested.
5. Drive Testing : it’s not enough for us to just wipe a drive, we always test, wipe, and re-test after a wipe. Amy drives with reallocated sectors are replaced. This means we sometimes scrap potentially usable drives, but better safe than sorry. 
6. OS Installation : at this point we PXE boot and install Xubuntu Linux 22.04 from our network installer.
7. Post-Install Setup : at this step we use a script we pull from github to install extra software we think would appeal to average computer users. Things like DVD playback, sound, webcams, and USB ports are also tested at this stage.
8. Quality Assurance : Someone else takes over at this stage and goes through a separate checklist to ensure the computer is in good working order.
9. Sales Preparation : This is the final stage where the computer will be priced, a barcode and information sticker attached to the computer, and the computer information goes into our Point-Of-Sale (POS) system.

This is a very generalized list of steps, the actual process is a fair bit longer, and we sometimes run into issues… The Lenovo ThinkStation C20 is one of those times where we ran into a minor issue and needed to reconsider which version of Linux we were installing on the machine.

### The Lenovo ThinkStation C20

The Lenovo ThinkStation C20 is a very old machine by today’s standards – it appears to have come out Q4 of 2010. The machine we received had a single XEON E5620 CPU (4 cores, 8 threads) running at 2.4GHz. One of the things that makes this workstation interesting is there is a spot for a second XEON CPU on the motherboard (along with another 3 RAM slots – 3 for each CPU). I’m not sure if the machine had the standard install of 4GB of DDR3 and we upgraded that to 8GB, or the person who donated the machine upgraded it to 8GB. Either way the machine currently has a single 8GB stick installed. The graphics card is the original [NVidia Quadro 2000](https://www.techpowerup.com/gpu-specs/quadro-2000.c900) card that would have come with this workstation. The Quadro 2000 ended up being a pain-point for building the machine, but more on this later.

Normally the ThinkStation C20 would have come with a 300GB 10,000 RPM hard drive. We always pull drives out of desktops to be batch wiped with other drives. Finding good 10,000 RPM hard drives is difficult these days. And while most of the world has moved on to solid state drives, we don’t see a lot of SSDs at Computer Recycling. We do see a lot of 500GB hard drives, so that’s what we put in the C20. Sadly, we chose a WD Blue drive. This wouldn’t have been my first choice, a WD black drive would have been a better choice, but the blue drive tested fine and was what ended up being put in.

It’s possible the Computer Recycling project might have another XEON E5620 CPU lying around, but even if we found one, we don’t have the heat sink needed to cool the extra CPU. So for now, we’re just using the single XEON processor.

### Initial Xubuntu Install

One of our volunteers initially installed [Xubuntu 22.04](https://xubuntu.org/) on the C20. Xubuntu appeared to work great, but one of the benchmarks we run (Xonotic game), was really low (39.54 FPS for high detail at 1024×768). Checking the driver I noticed that they were using the open source driver, rather than the available (Nvidia-390) proprietary driver. Our new checklists mention checking 
for proprietary drivers using the drivers program in Xubuntu/Linux Mint, but the checklist this volunteer was working from 
was older and didn't mention this step.

However, even if the volunteer followed the newer checklist, they still would have failed to install the driver. It turns out that the proprietary driver fails to install in Xubuntu 22.04 (and Linux Mint with a newer kernel). After a bit of digging I discovered that the NVidia-390 driver needs an old kernel. The kernel in Xubuntu 22.04 is too new to support the old proprietary NVidia driver. 

### Installing Linux Mint

While I fully expect whomever buys this machine won’t use it as a gaming machine (it’s 2010 remember), squeezing a few extra FPS out would be nice. Knowing that Linux Mint XFCE (21.3 – Virginia) uses an older kernel I decided to try installing Linux Mint to see if the proprietary NVidia driver would work. Yes, it did. And it turned out that it was significantly better, 172.20 FPS (vs the 39.54 FPS using the open source driver).

![Linux Mint](/img/linux_mint.webp)<figcaption>Fig. 1 - Linux Mint</figcaption>

Before people go slagging the open source driver developers, the bad performance of this old NVidia card is not their fault. Traditionally, NVidia hasn’t been very helpful to the open source community (thus the infamous [Linus Torvalds cursing NVidia video](https://www.youtube.com/watch?v=iYWzMvlj2RQ)). 

While NVidia has a page full of open source projects, I am sure they’re not interested in spending the time to update ancient drivers like this to work with modern versions of Linux. It’s a bit sad, as a machine like this C20 could still be a very useful workstation, especially with the max 192GB of RAM, and an SSD.

After installing the NVidia driver I also ran [Timeshift](https://github.com/linuxmint/timeshift), and set up a restore point for the computer. I figured I would try updating the kernel on Linux Mint, because they make it dead simple to do so. Sadly this resulted in the machine not booting to the desktop, as it had done with Xubuntu. This wasn’t an issue because I was able to just switch to a virtual terminal (CTRL + ALT + F1), login, and run:

```shell
timeshift --restore 
```

Timeshift then displays the restore points you’ve set up and lets you choose a point to restore to. I restored back to the kernel the proprietary driver worked on, and voila, the machine was ready to go, back at the desktop. This also confirmed that the issue is compiling the source against a newer kernel.

![Timeshift](/img/timeshift.webp)<figcaption>Fig. 2 - Timeshift</figcaption>

### Considered changing video cards

I also considered changing the video card in the C20 to an ASUS branded AMD HD7750, which scores about 47% better on synthetic tests than the Quadro 2000, but sadly the height of that card is about 10 mm too high to fit in the case properly. The other video cards we have that don’t have a PCIe power connector are all much older, so the Quadro 2000 ended up being the best fit. Something like a low profile GTX 1030 might be the cheapest price/performance card that would actually fit in this machine, but then again we’re dealing with NVidia.

### Still More Work To Do

There’s still a bit more work to do on this system. The lid has a lot of very deep scratches on it, so I plan to take it out an spray paint it matte black to get it looking similar to the rest of the system. It’s a neat machine with potential. Once done we’ll likely sell it for around $50 CDN, but for the moment it’s back in our to be refurbished area until we can clean it up a bit more.

