---
date: '2024-08-15T08:49:02-04:00'
draft: false
title: 'Transitioning our KODI media centre'
cover:
    image: img/our_media_centre.webp
    alt: "Left - our media centre"
    caption: "Left - our media centre running KODI on Xubuntu"
tags: ["KODI","Media Centre","Media","DVD","Blu-Ray","Hardware","Linux","Computer Refurbishing","TFF","TrueNAS","XBMC","Xubuntu"]
categories: ["Hardware","Linux","Media"]
---

### Moving more to a low-power solution

Several months back I replaced the motherboard in the KODI media centre PC that sits in our living room. For many years our media centre has been rocking a Gigabyte motherboard with a second generation Core i7-2600 CPU. The Core i7-2600 came out in Q4 of 2010, making it almost 14 years old at the time I’m writing this. Still, it’s not a bad CPU. For several years it was the system I was compressing our movie collection on as the A8-5600K 4 core APU that was in my workstation (at the time) had about half the performance of the i7-2600. But about six months ago I replaced the CPU and motherboard with a still old, but more modern solution, a MSI motherboard and an Intel Core i3-7100.

The Core i3-7100, despite being 7th generation, still doesn’t quite have the multi-core performance of the i7-2600, at least in synthetic benchmarks, but it’s only about 19% less, and manages that on only 51W of power compared to 95W for the i7-2600. Sadly the motherboard and CPU combination did not come with a backplate, so the setup looks a bit jank. I’ve since bought another motherboard (ASUS), but it needs a bit of testing before I go replacing the MSI board.

### RAM Upgrade

When I bought the MSI motherboard, I bought it thinking I had DDR4 RAM kicking around the apartment. I did, but it was only a mismatched pair of 4GB sticks of RAM (8GB total).

![The old RAM in our KODI media centre](/img/mismatched_ddr4_8gb.webp)<figcaption>Fig 1. The old mismatched RAM in our KODI media centre</figcaption>

Last weekend I picked up a couple of T-Force DDR4 Delta RGB sticks of RAM (2 x 8GB) to up the RAM to 16GB. Initially I thought about picking up 32GB, but we’ve been on vacation, so prioritizing what we’re spending on, I picked up the 16GB kit with the knowledge that the 4 slots on the ASUS board would let me move to 32GB by buying another 16GB kit in a few weeks. The T-Force RAM was on sale for $45CDN, not bad considering 2 x 8GB GSKill DDR3 sticks cost $189CDN new back in 2013.

RGB was not the reason I bought the T-Force RAM. While there were 16GB kits slightly less expensive ($5 less), the T-Force RAM had a higher clock speed than either of the other kits on sale.

![T-Force 16GB (8GB x 2) DDR4 kit](/img/t_force_16gb_ddr4.webp)<figcaption>Fig 2. T-Force 16GB (8GB x 2) DDR4 kit - the new RAM</figcaption>

### Simplifying, and storage

At one time our living room was packed with devices and media. Connected to the computer and television was a 5.1 surround sound Sony receiver, and the media centre stand was packed with DVDs, Blu-rays, and other physical media, plus several other devices.

As my wife and I age, we find ourselves wanting thinking about the fact that when we next move, we don’t want to have to lug around large surround sound systems, or look at clutter. Lately we’ve been purging, rather than adding things to our living space.

I’ve also noticed we need more drive storage. Currently our media centre has a 500GB Seagate boot SSD, and 2 x 8TB Seagate Ironwolf hard drives. The drives are not in a RAID configuration, but the second drive is a backup for the first. Sunday, at 2pm in the morning, a cron job runs rsync to synchronize changes from the first drive to the second. While we have 2 x 8TB drives, we’re really only using 8TB. 4TB drives are really the sweet spot then it comes to buying new drives, a 4TB (CMR) Ironwolf Pro is currently only $133, but this isn’t nearly enough storage. And to be clear, it’s a Pro drive, vs the non-pro 8TB for $245 (currently). Ideally we would mirror the 8TB drives, but this would mean shelling out well over $500 for 2 drives. I expect that within the next several months the cost of drive storage will go down as both spinning rust and solid state drives continue to get bigger, so I’m loathe to buy 2 drives at once.

We also need more storage for things like our phones and cameras. Having big drives isn’t just about our media centre anymore, which made me rethink our living room.

![Side view of new RAM](/img/new_ddr4_side_view.webp)<figcaption>Fig 3. Side view of the media centre with the new RAM</figcaption>

While having a PC with glowing RAM is cool, I’ve been thinking our media centre PC should really transition into a TrueNAS server. Transitioning to TrueNAS would mean that I could do a RAID Z1 configuration with 3 drives, where two act as 16GB with one drive as parity. This would give us a bit more space for awhile. I’m still not convinced it’s enough, but it’s enough for now. This PC would then get tucked away in a less visible area.

In the living room we would use the Tiny Form Factor Lenovo PC pictured on the second glass layer in the first photo. This PC would replace our current KODI media centre and would use an NFS-mounted share (from the hidden TrueNAS server) for the media. I’ve tested NFS shares in the past and they’re plenty fast. And while this seems like we’re complicating things by adding a machine, since this machine is already being used for another purpose, we’re simply re-purposing it, and unifying our backup/media storage on the server.

### Future upgrades

More 8TB drives are the biggest hurdle at this point. The Corsair Spec01 case only has space for 4 drives, so if this ever evolves, it will mean a case upgrade. Sadly, case manufacturers don’t really seem to be manufacturing cases with 3 1/2 inch drive support anymore. Even worse, almost no one makes a case with a 5 1/4 inch drive bay, it’s all mostly old stock. Things like my 3 bay Blu-ray ripping (I’m using a Antec Three Hundred Two case) workstation, are becoming less and less possible without using old stock.

Another 16GB kit would be the next upgrade after adding more drives. The final couple of bits in our media centre puzzle would be a sound bar and switching out our old 42″ Samsung TV (which is several inches thick). The television is 1080p and has been a great TV, so there’s no need to switch it out. I’m really not that enamoured with 4K, and last year I bought a 4k monitor for my workstation, so if I ever feel the need to watch a 4k movie, I just need to go to another room. The switch would be more about mounting the television to the wall, which isn’t something I want to do with this old TV, and would be a lot more likely when we move – maybe a couple of years. It’s the least priority on our list – and ranks lower than buying a nice carpet for the living room.

![Closeup of our media centre](/img/spec01.webp)<figcaption>Fig 4. Closeup of our old media centre</figcaption>

Instead of having a big chonky media centre, I prefer the small Tiny Form Factor PCs in our living room. I’ve always been a fan of the “modern living room” look, but getting that way with all the junk we’ve collected over the years is hard. For now, our KODI media centre is still a media centre, but once I’ve added at least one more drive then I’m going to switch the system to a TrueNAS server.

I haven’t decided yet if I’m going to switch to the ASUS board, as there may be some clearance issues with the Corsair H10 cooler and the size of the built-in backplate on the ASUS board, but I expect it will work. If not, I might be on the hunt for a new case too.

> We've since swapped the big case for a Tiny Form Factor PC (the same as can be seen to the right of the title image). The TFF PC runs Xubuntu and KODI with shares mounted from our TrueNAS server.
