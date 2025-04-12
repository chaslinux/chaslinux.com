---
date: '2023-03-20T19:45:38-04:00'
draft: false
title: 'Handbrake performance on more than 6 cores'
cover:
    image: img/encoding.webp
    alt: "Core usage encoding Blu-Ray quality files"
    caption: "Core usage encoding Blu-Ray quality files"
tags: ["Handbrake","Encoding","FFMpeg","Video Encoding","Hardware","Software","Linux"]
categories: ["Linux","Media","Software"]
---

### Diminishing returns after 6 cores, but not for all media

Handbrake is a video transcoder. It’s normally used to convert and compress video from a format into a more compressed format. Handbrake comes in a command line version, handbrake-cli, and a graphical version, handbrake. I’ve seen it mentioned several times that Handbrake is best at 6 cores or less, after that the encoding returns are diminishing. I thought this was the case with some of my experimentation, but it seems the answer is more complicated – it depends.

In this reddit thread (https://www.reddit.com/r/Amd/comments/6t0x77/do_you_know_that_handbrake_can_only_use_up_to_6/) someone by the nickname Jussi_Helle-aho comments that it depends on the media and format being converted to. Jussi suggests the limitation isn’t handbrake, but the h264 format. I’m not sure this second part is true, but the first might be. In my experimentation with my E5-1650v0 (6 core, 12 thread) and E5-2690v2 (10 core, 20 thread) I found that handbrake did tend to max out (90%+) all of my E5-1650v0 cores on DVD content, whereas my E5-2690v2 cores sat around 75-80% during the encoding process.

However, if I started encoding Blu-ray content, even using x264 as an end format, all cores ramped up to between the high 80’s and mid 90’s. I set up a conky to monitor all my cores originally to try and diagnose some issues running Grim Dawn, a Windows-based ARPG that I run under Proton through Steam. The game works fine at the beginning, but as things ramp up and the game progresses, it crawls on my 10 core 20 thread system. This is a bit concerning since I have an NVMe drive, 10 cores and 20 threads, 64GB of RAM, and, a 4GB Radeon R9 380 graphics card. My system is significantly better than the minimum recommendation, and just fits the recommended settings with the CPU’s top clock at the recommended setting.

Running idle, the cores run at 1.20-1.50GHz. Running Handbrake on Blu-ray content, all the cores and threads shoot up to 3.29GHz with between 90-95% usage. At the end of the encoding process, cores drop back down to between 1.20 and 1.50GHz. DVD encoding is slightly different, cores eventually shoot up to 3.29 GHz, but tend to sit at 3.24-3.27 GHz for a bit, and only average 82% usage.

I haven’t experimented yet with different codecs. VP9 seems interesting, but whether Handbrake supports it I’ve yet to investigate. GPU encoding is all the rage, but I remember reading some articles and thinking there were drawbacks to GPU encoding given my process, and it seemed more difficult to implement in Xubuntu Linux. Still, these are worth looking into as I’ve mostly switched to webp for images (vs jpeg/png) and been pretty happy with the result.

Is it worth going out and buying an inexpensive X79/X99 CPU and motherboard combination over new technology? I don’t think so. If you already have an X79/X99 motherboard or CPU the answer might be yes depending on the processor. Newer technology tends to have instruction sets more beneficial to compression. Newer processors also tend to have higher clock speeds per core, which translates into more performance per core. I’m not sure how a processor like the Ryzen 5 5500, which was just over $115CDN last week, would fare against a $60-$80 18 core, 36 thread XEON, but I’ve been tempted to upgrade our media centre with an X99 board and processor, and my own system with a Ryzen CPU and motherboard. 