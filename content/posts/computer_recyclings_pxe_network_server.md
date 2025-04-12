---
date: '2025-04-01T18:24:58-04:00'
draft: false
title: "Computer Recycling's PXE Network Server"
cover:
    image: img/most_recent_linux_installers_pxe.webp
    alt: "The most recent Linux distributions on our PXE network server"
    caption: "A variety of Ubuntu-based distributions"
tags: ["Linux","Computer Refurbishing","Software","Operating System","Ubuntu","Kubuntu","Xubuntu","Linux Mint","Software Tools"]
categories: ["Linux","Operating Systems","Computer Refurbishing"]
---

### PXE network installation

Most Linux distribution web sites describe the process of how to download an **ISO**, and create a bootable USB key. While USB keys are great if you're working on your own computer, when you need to scale up and install across a number of systems there are more efficient ways of deploying Linux. One of those ways is to network boot, and install from a PXE (Preboot Execution Environment) server.

### PXE server history at The Working Centre's Computer Recycling Project

The Working Centre's Computer Recycling Project has deployed Linux via a PXE server since around 2010. The machine we originally used was a custom built machine with 4 drives (all independent, none in a RAID configuration), a Core 2 Duo processor, and a whopping 4GB of RAM. Over the years the machine developed a few hiccups, one of the drives failed (luckily it wasn't a drive that was critically important), some of the scripts we used stopped working with newer (20.04+) versions of Xubuntu Linux, and the host OS stopped getting updates (it was 32bit,a misstep on my part), and UEFI PXE booting was only set up much later.

### Enter the new server

The new PXE server is on server-grade hardware, a 1U rack-mount server with lots of RAM, and a mirrored RAID array. While I originally installed a 64bit of Ubuntu server 22.04, it's since been upgraded to Ubuntu 24.04.2 without any issue. The new server supports both **Legacy BIOS** and **UEFI** PXE network booting, though not all the software on the server will necessarily run on all hardware (for example: our old Debian Live environment we use for some testing, doesn't work on 7th or 8th generation hardware, because that Debian environment is very old -- but we have alternative tools that do).

At the moment the menu is broken down into 3 main menu options:

1. Linux Live Installers
2. Manual Installers (FreeDOS)
3. Utilities and Tools

The old PXE server required staff and volunteers to type in arbitrary names we gave to various distributions in order to boot the option. The new PXE server uses a menu system that accepts arrow key input, making it easier to select any option. The image in the background of the menu changes slightly depending on whether you're booting in UEFI mode, or Legacy mode (either UEFI64, UEFI32, or Legacy appear in the bottom right of the image).

![Booting the server in Legacy mode](/img/legacy_main_menu.webp)<figcaption>Fig 1. Legacy PXE boot main menu</figcaption>

A fourth option, autoinstallers, is disabled for now. While the autoinstaller appears to work for Xubuntu Linux, there are some issues with autoinstallation:

- technically it's not Xubuntu, but an Ubuntu kernel with xubuntu-desktop packages.
- we ran into quite a few boot loader issues on several different systems.

### Github scripts

To automate some of the process that used to be automated in the autoinstaller, we actually pull a script from github (that pulls other scripts), and run it after we've completed a live installation. It's certainly less efficient that using the autoinstall method, but it has some advantages:

- Other people and organizations can use the scripts.
- Other people and organizations can contribute to the scripts.
- Whether at work or home, the scripts can be updated/modified.
- Scripts can be quickly modified for other systems.

The main script we currently pull is: (https://github.com/chaslinux/mint-setup)

This script pulls 4 other scripts that do the following functions:

1. Update the operating system, and create a PDF of the hardware specifications on the user's desktop.
2. Update the system and install a bunch of extra software we think the "average computer user" might find handy.
3. Run a CPU benchmark (geekbench6)
4. Run a graphics benchmark (phoronix-test-suite's OpenArena benchmark)

### The current state of the Linux installers

The new PXE server at the Computer Recycling Project currently supports installing the following Linux Distributions:

1. Linux Mint 22.1 XFCE edition
2. Linux Mint 22.1 Cinnamon edition
3. Linux Mint 21.3 XFCE edition (21.3 has an old kernel that can better support Nvidia cards)
4. Xubuntu 24.04.2
5. Xubuntu 22.04
6. Ubuntu 24.04.2 Desktop
7. Kubuntu 24.04.2 Desktop
8. PoPOS 22.04 Desktop (UEFI and Intel only)
9. Ubuntu Server 24.04.2 HWE enabled
10. Ubuntu Server 24.04.2 (non-HWE)
11. Ubuntu Server 22.04

![PoPOS running on an Optiplex 3050](/img/pop_os_from_pxe_installer.webp)<figcaption>Fig 2. The latest addition to our PXE server PoPOS 22.04</figcaption>

### Manual installations

The manual installtion section of the server currently only has one operating system FreeDOS.

### Utilities and Tools

Not only can you install Linux, but you can run a bunch of tools via PXE. On our PXE server we have a bunch of different tools we use for certain situations:

1. Hardware Test (Jammy) - this is a custom Xubuntu 22.04 environment with some extra tools for testing more modern hardware.
2. Debian Live (Jessie) - we keep this to test legacy 32 bit computers, and older 64 bit hardware.
3. Parted Magic 2019_03_17 - this is actually a commercial product based on open source that we bought to wipe SSDs and NVMe drives.
4. Memtest 6.2 (64 bit) - an updated version of Memtest that seems to run in both UEFI and Legacy mode
5. HDAT2 - a very old version of a hard disk repair we used to use.
6. SHREDOS - a custom Linux distribution that runs nwipe, an updated version of dban with some extra features.
7. DBAN - Darik's Boot and Nuke - interactive.
8. DBAN (3 pass autowipe) - automated.
9. Clonezilla - while we haven't used this in awhile it's an updated version of the open source cloning software.

![Tools menu](/img/uefi_tools_menu.webp)<figcaption>Fig 3. Utilities and tools menu</figcaption>

There are a few other tools actually on the server, including a more open source memory test we might eventually move to once more testing is done.

### Gotchas

Our project sees a lot of variety in the hardware we get, this is both a blessing and a curse. In our testing we've found some very bizarre results, network booting is not quite as straightforward as it used to be, thanks mostly to the implementaton of UEFI. UEFI can be vastly different between machines. Not all machines seem to be able to boot all options, despite the fact that their "specifications" meet/exceed the specifications for the Linux distribution.

> For example: HP mt43 mobile thin clients (roughly 2018) kept doing a network timeout while trying to load any of the Linux Mint, or Xubuntu images, but loaded Ubuntu 24.04.2 just fine. Another laptop with similar specifications network booted every image just fine. 

### Evolving

As we run into various issues we're evolving both our server and processes. We may completely automate our installations again some day, but having switched to Linux Mint there's an extra obstacle as we seen to be one of the few organizations deploying Mint via PXE server. Also, I love the fact that others have contributed to our scripts. We've been blessed to have people who have worked on the Tor project contributed to our scripts, and former Canonical staff also contribute to our scripts. The world is a better place when we work together!