---
date: '2025-01-23T11:26:33-04:00'
draft: false
title: 'Lessons learned encoding media under linux'
cover:
    image: img/handbrake.webp
    alt: "Handbrake video encoding software running under Xubuntu Linux"
    caption: "Handbrake running under Xubuntu Linux"
tags: ["1080p","4k","Blu-Ray","DVD","Encoding","Hardware","Linux","Media","Handbrake","Xubuntu","Linux Mint","FPS"]
categories: ["Media","Linux"]
---

### Hardware and Linux Distribution Differences

This post covers a bunch of areas of media decoding and encoding that I’ve discovered over a number of years using Debian-based distributions like Xubuntu, and Linux Mint. Primarily I’ll cover some of the differences between Xubuntu and Linux Mint, how various hardware (CPUs and graphics cards) encode video, and some of the “gotchas” when it comes to different methods as they apply to Handbrake (software) and MakeMKV.

### First – straight up numbers

I’m going to blather on about various topics so I thought I’d start by getting straight to the point with CPU vs GPU encoding. This is strictly using Handbrake under either Linux Mint, or Xubuntu. The version of Handbrake varies slightly on a couple of results, but most results are using Handbrake 1.7.2. There are 4 potential Handbrake “presets.” I’ve modified each of these “presets” to include all subtitles in the video. The same video and presets were copied to a key and used on each system. I wanted to test a large variety of old and slightly newer systems. I don’t have access to the latest hardware, so you won’t see any NVidia RTX 4090 cards, or 14th gen Intel systems, but I did manage to spend a bit of time with a 12th gen Intel system.

| Manufacturer | Model | FPS | OS | Handbrake | Notes | Hardware Date |
| :------: | :------: | :------: | :------: | :------: | :------: | :------: |
| NVidia | Quadro P1000 | 883.40149 | Xubuntu 24.04 | 1.7.2 | 4GB Video Card + NVenc | 02/2017 |
| Intel | i5-12400 | 776.363831 | Linux Mint 22 | 1.7.2 | Quicksync | 01/2022 |
| NVidia | Quadro M4000 | 655.209595 | Xubuntu 24.04 | 1.7.2 | 8GB Video Card + NVenc | 06/2015 |
| Intel | i5-12400 | 479.023224 | Linux Mint 22 | 1.7.2 | Fast 1080p preset (CPU only) | 01/2022 |
| Nvidia | GTX 1050Ti |	468.287628	| Xubuntu 24.04 | 1.8.2 | 4GB Video Card + NVenc | n/a |		
| Intel	| i7-7700K | 457.851044 | Xubuntu 24.04 | 1.7.2	| Quicksync | 01/2017 |
| AMD | RX5500 | 331.553558	| Ubuntu 24.04.1 | 1.7.2 | 8GB Video Card + VCN | 04/2018 |
| Intel | i7-4770 | 329.963104 | Xubuntu 24.04 | 1.7.2 | Quicksync | 06/2013 |
| Intel	| i7-7700K	| 302.826874 | Xubuntu 24.04 | 1.7.2 | Fast 1080p preset (CPU only) | 01/2017 |
| AMD |	Ryzen 7 2700X |	297.94632 |	Ubuntu 24.04.1 | 1.7.2 | Fast 1080p preset (CPU only) |	04/2018 |
| Intel | XEON E5-2690 V2 |	257.048859 | Xubuntu 24.04 | 1.8.2 | Fast 1080p preset (CPU only) |	09/2013 |
| Intel | i7-4770 |	227.501648 | Xubuntu 24.04 | 1.7.2 | Fast 1080p preset (CPU only) | 06/2013 |
| Intel | i5-7500T | 222.97403 | Linux Mint 22 | 1.7.2 | Dell Optiplex 3050 TFF w/ QuickSync | 01/2017 |
| Intel | XEON E3-1245 V3 |	220.609741 | Linux Mint 22 | 1.7.2 | Fast 1080p preset (CPU only) |	06/2013 |
| Intel	| i5-4590 |	214.610916 | Linux Mint 22 | 1.7.2 | Quicksync | 05/2014 |
| Intel	| i5-557R |	212.791763 | Xubuntu 24.04 | 1.7.2 | iMac 16,2 Quicksync |	05/2015 |
| Intel	| i7-2600K | 209.560608 | Linux Mint 22 | 1.7.2 | Quicksync | 01/2011 |
| Intel	| i7-2600K | 190.158112 | Linux Mint 22 | 1.7.2 | Fast 1080p preset | 01/2011 |
| Intel	| i5-4590 |	180.338837 | Linux Mint 22 | 1.7.2 | Fast 1080p preset (CPU only) |	05/2014 |
| Intel	| i5-557R |	177.168747 | Xubuntu 24.04 | 1.7.2 | iMac 16,2 Fast 1080p preset (CPU only) | 05/2015 |
| Intel	| i5-7500T | 173.715698 | Linux Mint 22 | 1.7.2 | Dell Optiplex 3050 TFF Fast 1080p preset (CPU only) |	01/2017 |
| Intel	| i5-3470 |	162.972992 | Linux Mint 22 | 1.7.2 | Fast 1080p preset (CPU only) |	06/2012 |
| Intel	| i5-3470 |	157.530548 | Linux Mint 22 | 1.7.2 | Quicksync | 06/2012 |
| AMD |	Phenom II X6 1055T | 131.942596 | Linux Mint 22 | 1.7.2 | Fast 1080p preset (CPU only) | 05/2010 |
| Intel | Pentium G4560 | 120.576569 | Xubuntu 24.04 | 1.7.2 |	Fast 1080p preset (CPU only) |	01/2017 |
| Nvidia | GTX 960 | 113.656097 | Xubuntu 24.04	| 1.8.2 | 2GB Video Card + NVenc | 01/2015 |
| AMD |	A10-7800 | 103.614662 |	Linux Mint 21.3	| 1.7.2 | Fast 1080p preset (CPU only) | 07/2014 |
| AMD |	A10-6700 | 99.39901 | Linux Mint 22	| 1.7.2	| Fast 1080p preset (CPU only) | 06/2013 |
| AMD |	Athlon II X4 645 |	91.306389 |	Linux Mint 22 |	1.7.2 |	Fast 1080p preset (CPU only) | 08/2010 |

The presets are Fast 1080p 30 FPS H.264 which uses raw CPU encoding, Quicksync H.265 1080p which uses special “quicksync” instructions found on most Intel processors since the 2nd gen i-Series processors (note: not all Intel processors support this – see the top 7th gen Pentium G4560 which failed when we tried), NVENC H.265 1080p which is supported by most newer NVidia cards (and some pretty old ones), and VCN 1080p H.265 1080p encoding.

The original video was an encrypted DVD that was turned into a MKV along with all subtitles using MakeMKV.

The clear winner of the encoding battle was won by the NVidia Quadro P1000 4GB video card. The P1000 is remarkably a small, thin card that requires no power outside of the PCIe slot it fits in. It has 4 x mini-Display Port outputs for up to 4 monitors. The system it was running on is none other than the dual-monitor workstation I frequently use at The Working Centre’s Computer Recycling Project. The project has run Xubuntu Linux since a bit before 2010, only recently moving more towards Linux Mint. There are some advantages to using Xubuntu over Linux Mint that do not have to do with encoding numbers, but I’ll get to those further down. This winning result was using the Nvidia NVENC preset. I’ve run into issues with this preset which I’ll also explain further down. For now the important take-away is that this 2017 4GB graphics card will give you a better encoding result than a 2022 CPU with Quicksync enabled. There’s an asterisk here that I’ll explain after the next result.

The Intel Core i5-12400 CPU with the Quicksync preset enabled comes in second with a bit less than 100 FPS under the Quadro P1000. This might not seem like much, but if you’re encoding a lot of video, it could be significant. And this is where NVenc fell down for me. NVenc was fine for encoding 1 video at a time, but if I queued videos in Handbrake, like you would for something like a season of television shows, NVenc didn’t seem to activate. I’m not sure if this was a bug. I also cannot say if this was true for Quicksync as I only tried queuing videos on the Fast 1080p preset (it worked) and NVenc.

The third top result is also an interesting result. The Nvidia Quadro M4000 is an 8GB video card from 2015. What makes this result interesting is the fact that the card is an 8GB card, less memory than our top result 4GB card. This result suggests encoding isn’t so much about RAM as it is the improved technology of the newer 2017 card.

What isn’t in these top 3 results, the 10 core 20 thread Intel XEON E2690 v2 CPU, nor the Ryzen 7 2700X 8 core 16 thread CPU. In fact both of these ranked lower than a 4th generation Intel Core i7-4770 with Quicksync. The E2690 V2 doesn’t support Quicksync, and the Ryzen 7 2700X just can’t keep up to quicksync. There is a result showing the Ryzen 7 2700X above the i7-4770, but this was the AMD RX 5500 graphics card with VCN enabled using the VCN preset. It also lagged behind our top performers.

The takeaway from these top encoders are: if you’re on an older system and looking for a cheap way to encode a few videos, buy a Quadro P1000 video card. The P1000 is easy on your computer’s resources (low powered card). Don’t look on Amazon for these cards as Amazon sellers have them on for $200+. Ebay is probably the best bet with these cards sometimes going for around $100CDN – it’s not super cheap, but compared to buying a complete 12th gen desktop it is.

If you’ve got money to burn I would argue a desktop with an Intel Core i5-12400 is the better choice despite the 100 FPS less as you always have the option to add a newer NVidia card for even better performance.

Generally speaking, the newer the technology, the better, but this is not always true, as this chart suggests. Even with quicksync enabled, our Tiny Form Factor Dell Optiplex 3050s with their 7th generation Intel Core i5-7500T CPUs could not beat the 4th generation i7-4770 without quicksync enabled … so what’s going on here? Quit simply the i5-7500T CPU is really designed for the embedded, low-power draw market. At a TDP of 35W the i5-7500T is a decent CPU, but it just cannot compete with the i7-4770 desktop processor which has a TDP of around 85W and higher base and max turbo frequencies. With quicksync enabled the i7-4770 (non-K) is more than 100 FPS better than the i5-7500T for video encoding. Does this make the i5-7500T a bad processor, not at all, it’s just not as good as the older i7 for this particular task.

![Video encoding results for various hardware](/img/encoding_numbers.webp)<figcaption>Fig. 1 - Video encoding results for various hardware</figcaption>

### Handbrake – Xubuntu vs Linux Mint

Using Handbrake under Xubuntu was a more pleasant experience than using it under Linux Mint. When queuing multiple files, Handbrake under Linux Mint returns you to a top-level directory. This means if you have videos stored under ~/Videos, you have to drill down to that directory, or whatever sub-directory under this that the episode is stored in. For example ~/Videos/Night_Court. Each time you add a file to a queue Handbrake returns you to a top level directory where you have to drill down to ~/Videos/Night_Court to get the second, then again for the third file, and so on. Handbrake under Xubuntu returns you to the directory the last queued file was in, so if you’re queuing multiple files you simply choose the next file and add it to the queue. This is not only time saving, but hand-stress saving. 

### Summary

Newer is not necessarily better, especially if you’re on a tight budget. If you have lots of cash, and plan on doing lots of video encoding then a modern Intel-based system with a modern NVidia GPU is probably going to be your best bet. While we didn’t have any Nvidia GPUs newer than the 2017 P1000 to test with, I’ve spoken with a few people with more modern NVidia GPUs that swear they’re awesome for video encoding. The performance of older cards varies. If you’re interested in picking up a used NVidia card check the wikipedia web page on NVENC as the table explains quite a bit about the actual graphics processors that support NVENC. I’ll reiterate, just because something is newer, doesn’t mean it’s better. Take the NVidia GT1030 2GB video card for example. Checking [Techpowerup](https://www.techpowerup.com/gpu-specs/geforce-gt-1030.c2954), the GT1030 uses a GP108 graphics core, which the wikipedia NVENC web page shows has no NVENC encoders available for. In our results the i7-4770 (non-K) with quicksync enabled beat out the i7-7700K without quicksync enabled, so just because something is old doesn’t mean it’s bad… with quicksync enabled the newer i7-7700K is more than 100 FPS faster, so this choice comes down to economics and the availability of similar hardware where you are.

When encoding multiple files be prepared either to not get NVENC performance, or to individually add each file (babysit your computer). I prefer to batch everything and let the CPU encode everything at once. I have to imaging this is something that will be fixed in a later version of handbrake.

Whether it’s the (.deb debian) repository of Handbrake vs the flatpak Handbrake, or just differences between Xubuntu and Linux Mint, Handbrake worked better under Xubuntu for queuing multiple files. It was simply less work, and less strain on the hands. I previously mentioned switching my home desktop to Linux Mint, that didn’t last long after I discovered this Handbrake issue. My home workstation is back running Xubuntu and will likely stay that way for the foreseeable future.

Sadly I didn’t have access to a lot of newer hardware, it would have been really nice to run the same tests on a modern Intel graphics card, or newer NVidia graphics card. I’ll continue to update this list as I have access to more hardware. I have more to say about encoding 1080p vs 4k, but that’s for a different post.
