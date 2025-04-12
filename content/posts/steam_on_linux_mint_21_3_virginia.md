---
date: '2025-03-13T09:19:00-04:00'
draft: false
title: 'Steam On Linux Mint 21.3 (Virginia)'
cover:
    image: img/mint-xfce-running-steam-flatpak.webp
    alt: "Steam flatpak running on Linux Mint"
    caption: "The flatpak version of Steam running on Linux Mint XFCE"
tags: ["Gaming","Linux Mint","Linux","Refurbishing","Steam"]
categories: ["Gaming","Linux","Hardware"]
---

### Debian package over flatpak, but get it from Steam

Moving from Xubuntu to Linux Mint XFCE was not as seemless as I’d hoped it would be. The last time I gave Linux Mint serious consideration was over 13 years ago when the Computer Recycling Project at The Working Centre was looking for a replacement for Ubuntu 10.04 (the next version would include the Unity desktop which wouldn’t run on a lot of our laptops at the time).

I remember thinking at the time that Xubuntu looked slicker, and had a better update program than Xubuntu. But Xubuntu seemed to run better on a wider range of hardware than Linux Mint, and there were some issues I can’t recall, that were show stoppers for us at the time.

One of the things I consider to be a show stopper is if Steam doesn’t work. I’m sad to say that Linux Mint 21.3 has Steam issues. These issues are resolvable, but since Linux Mint is often touted as a “new user-friendly” Linux distribution, I’d expect the issues to be solved in a major release like Virginia (21.3).

### What Steam Issues?

While Linux Mint supports flatpak, there seem to be ample web sites that suggest that flatpaks pose security problems. Common advice seems to be use a Debian package first, and only use flatpak’s when:

- You need a later version of a program
- The software isn’t in the distribution’s software repository

I installed the Steam flatpak to see how it performed. On my desktop workstation it performed admirably. I had no problem installing Steam, and was able to play Path of Exile with decent performance (R7 2700X CPU and an RX5500 video card). While I never paid attention on Xubuntu to how many FPS I got (because it was smooth), I didn’t notice a difference with the flatpak on Mint.

But, I decided to follow the common advice and install Steam from the software repositories, only to discover there were missing libraries. This prompted me to uninstall, and pick up the Debian package directly from Steam/Valve.

The Valve Steam Debian package seemed to work fine initially. I installed Clicker Heroes, an IDLE RPG that needs to be installed via Proton. It worked without issue. But when I went to play Path of Exile, performance was noticeably bad – it felt like I was running on a system with low-end integrated graphics.

A bit more digging and I discovered that the problem was likely due to the fact that Linux Mint 21.3 (Virginia) uses a fairly old kernel (5.15.0-112) out of the box, a kernel that doesn’t appear to properly support the RX5500.

Linux Mint actually makes installing a new kernel fairly simple:

1. Open the Update Manager
2. Click View > Linux Kernels
3. Click through the notification that warns about wireless and other potential issues installing a new kernel
4. Pick the kernel you want and click install
5. Reboot and pray


This fixed my issue with Path of Exile performance on the Valve version of Steam.

But this method has 2 problems: First, it’s not really that newbie-friendly as it involves several steps. Second, it can’t be scripted easily.