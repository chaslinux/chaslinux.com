---
date: '2024-06-25T19:12:27-04:00'
draft: false
title: 'Xubuntu 24.04 bugs so far - May 3 2024'
cover:
    image: img/steam_on_xubuntu_2404.webp
    alt: "Steam on Xubuntu 24.04"
    caption: "Steam client on Xubuntu 24.04"
tags: ["Linux","Xubuntu","Hardware","Computer Refurbishing","Shell Scripting"]
categories: ["Linux"]
---

> **Note:** While I tried using Linux Mint XFCE at home for awhile, I still found Xubuntu 24.04.2 works best for my use
> cases. There are some filesystem differences, and while I was adverse to snaps because of control issues, I'm finding they
> have some advantages over flatpak that I like. This is a repost from the old website.

### Xubuntu Linux version 24.04 is out

Version 24.04 of [Xubuntu](https://xubuntu.org) Linux is now out! Xubuntu Linux has been a staple of the [Computer Recycling Project](https://www.theworkingcentre.org/cr/) @ The Working Centre since 2010. With the project switching mostly to Linux, it’s now more important than ever that we’re up to date on trends, and new developments that affect the project. This new version of Xubuntu has a number of nice improvements, but in my testing on several different machines I’ve run into a number of issues as well.

> **Note:** We've since switched to Linux Mint XFCE at the project, but we continue to offer Xubuntu to anyone who wants it.

### The good stuff

The biggest, baddest (in the good sense), improvement to Xubuntu Linux is the desperately needed improvement to the “Software Center” application. Gone is the slow-as-molasses GNOME SOFTWARE application. It’s been replaced by the “App Center,” an application/program installer made with flutter (a user interface development kit developed by Google and the community). The new App Center looks much better, loads much faster, and it’s a lot more intuitive. It no longer takes minutes for a simple app search.

The most obvious change to Xubuntu is the vibrant new green wallpaper and theme. The theme is still Greybird, but the menu icons are a lot more vibrant, and the overall look is just a cleaner. I love the new theme and wallpaper.

![Software - the software installation app is faster](/img/app_bundles.webp)<figcaption>Fig 1. Software - the software installation app is much faster</figcaption>

Thunar, the file manager, now supports the long-awaited split pane feature. ``Windows + F`` launches the Thunar file manager in Xubuntu, and with it opened, and in focus, if you press ``F3`` you’ll split the panes, making it easy to navigate and copy files between directories.

Xubuntu 24.04 also includes firmware-updater, a nice flutter application that checks for firmware updates for various devices (for example, NVMe/SSD/HDD, UEFI/BIOS) in your PC. and lets you update those devices to the latest firmware. There was a firmware update program in 22.04, but when I tried it, it only indicated updates were available for devices. The “software” program in Xubuntu 22.04 was also capable of downloading BIOS updates, which would get implemented on reboot. This new flutter firmware-updater is really well done, at least in our limited testing.

### The bad stuff

The new installer seems to have issues loading up, even on “stock” machines. I tried the installer on a stock Acer Aspire AT3-710-EB62 (6th gen i7-6700) paired with a Dell 27″ monitor and the display was “glitched” and wouldn’t map correctly. The system was previously working perfectly with Xubuntu 22.04. My first thought was issues with the 27″ display, but this particular Aspire has a Radeon R9 360 2GB video card, which shouldn’t have any issues with the 1080p 27″ display, at least not for normal/basic use. I wasn’t able to click on things, and the system just locked up. Shortly after I tested the same USB-based Xubuntu 24.04 install on a stock Dell machine with lesser specs (4th gen), and it worked just fine. The display issues only seem to happen with some machines.

The App Center is a huge improvement, and while it’s still in the list when you type “software” in the whisker menu, I feel like renaming it the App Center is a not a good move. This is more a personal annoyance. The Software Centre was previously renamed Software, and now it’s being renamed App Center. Changing the name of software leads to confusion across versions and makes it harder to document, and harder for less experienced users trying to follow documentation. I tend to think of “Apps” as lightweight/limited phone programs, rather than full-fledged software. One of the complaints we’ve heard at the project is the fact that things don’t work because someone is looking at old documentation where something has changed. A minor grievance, but I think a valid one.

I was also a bit disappointed to see that the new wallpaper only extended to the default green wallpaper. While I love the change, and the bright new icons, it seems to be the only new wallpaper included with 24.04. Again, this is something that’s very minor, but I’ve come to look forward to seeing new wallpaper with each release. It would be nice to see new themes with each release as well, but as someone who was involved with a Linux distribution many years ago (2001-2004) I realize how hard it can be.

Another issue I ran into was Window snapping. It appears to be gone in Xubuntu 24.04. In version 22.04 you could grab a window, drag it to the right or left side of the screen, and it would snap against the right or left side, and open a 1/2 page view of that window. This made it easy to see a couple of pages side by side. That feature appears to be disabled in the default install of Xubuntu 24.04.

### Flutter installer just doesn’t work in a live PXE install

> **Update:** This issue was fixed in Xubuntu 24.04.1 and still appears to be okay in 24.04.2

At The Working Centre’s Computer Recycling Project we deploy Linux using a network boot PXE (Pre-eXecution Environment) server. This is a fancy way of saying rather than setting a computer to boot from a USB key and installing from the key, we set the computer to boot from the network card, which connects to a server, that tells it to get instructions/downloads from another server. I set up a couple of different ways to boot the Xubuntu 24.04 Live image on our PXE server. Both methods load up the image into RAM, but when you click the installer icon on the desktop, the flutter installer window opens up a window that says “Preparing Xubuntu”, but it never gets past the Preparing Xubuntu window. Eventually, a “System Problem detected” window pops up, but the preparing Xubuntu flutter window never disappears, and clicking report the crash appears not to work.

![The flutter installer used to hang via PXE install](/img/preparing_xubuntu_flutter.webp)<figcaption>Fig 2. The flutter installer used to hang via PXE install</figcaption>

### Snaps

Of course I haven’t tackled the 6000 kg elephant in the room, snap packages. There’s a lot of hate for snap packages. Some of the reasons people cite for disliking snaps are:

- Speed : although some of this has been corrected with recent updates, applications still load slower than their .deb counterparts.
- The snap store is controlled by Canonical. Debian packages are mirrored, so if you have an issue with a mirror, you can change mirrors, no so with the snap store. 
- Canonical started replacing software like Firefox, Chromium, and Steam with snap versions, something they initially said they wouldn’t do. How do you trust them not to behave badly later on?
- Connectivity speed : this is something I added because we found issues trying to install snap packages during the release of 24.04. Again, having more mirrors might help with this problem.
- Security : while Canonical did catch a crypto miner that a company placed in it’s software, the initial malware scanner missed the miner. Not being able to audit the code, and having auto-updates, could pose a problem. Canonical’s own advice is to “only install snaps from sources you trust.” So why force snaps on people, if you don’t have 100% confidence. Default to Debian packages and let people choose snaps.
- Debian packages fail after snap versions appear : some have complained that the Debian packages they used in previous versions of *buntu don’t work in new versions, and have been replaced with snap packages. While we haven’t directly experienced this, we’ve found on some machines the (22.04) Debian package of VLC crashed while the snap package worked (loading a DVD).
- Space : snap packages take up more space.

I still feel Debian packages are the best way to go. That said the Computer Recycling Project did use to install a few snaps:

- [ANTSY Alien Attack](https://www.lexaloffle.com/bbs/?tid=52988) : a pico8 SHMUP game made by the developer of Ubuntu Mate
- [Fre:ac](https://www.freac.org/) : a CD ripping program with nice auto lookup features
- [Microsoft Office web apps](https://snapcraft.io/office365webdesktop) – to connect to MS Office online

We stopped installing any snaps recently. While we trusted the sources for those snaps, we just don’t feel we should add to the growing snap installs on machines.

### Computer Recycling switched, but I still have not

This was an older post, but I've removed the previous conclusion because there have been a lot of improvements since 
Xubuntu 24.04 was first released. As I mentioned earlier in this article, while I use both Xubuntu 24.04.2 and Linux Mint 
XFCE 22.1 at work, my preference at home is to still use Xubuntu 24.04.2.

Handbrake, which I use a lot to compress my media, has better behaviour when queueing a lot of files. While re-developing 
this web site I found I preferred to install hugo via snap. I could have used homebrew, and I did on a Linux Mint machine, only to find it did a lot of things I didn't like (creating a user directory in /home for the application)

Finally, I also found I had less issues with Steam on Xubuntu (using the Debian package straight from Valve). For the 
foreseeable future I'll continue to update Xubuntu on our PXE network server alongside Linux Mint XFCE, so if you're 
ever in our neighbourhood and would like to install either of these great systems feel free to drop in.



