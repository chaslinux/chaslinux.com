---
date: '2023-12-20T16:18:57-04:00'
draft: false
title: '[Fix] OBS Studio records static desktop image, no movement'
cover:
    image: img/frozen_obs_studio.webp
    alt: "OBS Studio is not really recording"
    caption: "Xubuntu - OBS Studio is not really recording"
tags: ["Hardware","Xubuntu","Linux Mint", "NVidia","OBS","Recording","Media"]
---

### OBS is awesome!

Open Broadcasting Software, also known as OBS Studio, is an awesome piece of free and open source software that lets you capture audio and video from a wide variety of sources: screen capture, webcam, audio capture from the system, from an external source, from static images, slide shows, etc.

It’s been awhile since I’ve used OBS to capture the desktop of one of the systems at work, an ASUS M51AC desktop with an i7-4770 CPU, 16GB of RAM, and a 256GB SSD. I installed OBS 30.0.1 and started to record a video of the desktop, using the webcam microphone for audio. After a bit of tweaking, adjusting Xubuntu’s microphone sensitivity, I managed to get audio recording correctly so audio levels did not “clip” (go into the red) in OBS.

Thinking I was done I recorded a video, only to find out later OBS had only captured a static image, and none of the adjustments I made to the desktop. At first I thought it might be due to the fact that I was recording 2k display, and also driving a second 1080p display. When I lowered the 2k display capture to 1080p it still refused to capture any of the desktop movement.

The solution turned out to be adding a graphics card. I was trying to capture the display using onboard video. While the M51AC’s onboard graphics is enough to drive the 2k and the 1080p displays, it’s not enough to capture the display correctly.

While I’m not a big fan of NVidia cards, I find their drivers tend to crash in Xubuntu and require removing and reinstalling, I put an NVidia Quadro P1000 (4GB) card into the M51AC. After installing the card I loaded up [Timeshift](https://github.com/teejee2008/timeshift) and created a restore point.

If you haven’t used Timeshift yet, it’s a simple point and click program that lets you create a system restore point. You can exclude your home directory so you’re not time shifting your entire Steam library (not backing up /home is the default behaviour).

The next task was to install the proprietary nvidia drivers. In Ubuntu/Xubuntu (or Linux Mint) this is pretty simple, just click on the whisker menu, type the word *Drivers*, open the driver program (make sure you’re connected to the Internet first or the driver program won’t be able to query the Internet to see what drivers are available). Install the “Proprietary, Tested” driver.

Reboot for the new graphics driver to take effect.

After installing the driver OBS Studio correctly recorded the 2k desktop.

In the case where the driver borks things, timeshift has a command-line version (that gets installed with timeshift) where you can timeshift the computer back to the open source driver.