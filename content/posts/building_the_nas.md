---
date: '2024-09-25T08:17:57-04:00'
draft: false
title: 'Building the NAS - hardware hiccups'
cover:
    image: img/building_the_nas.webp
    alt: "Unpacking the NAS case"
    caption: "Fractal Design Define R5 - our NAS case"
tags: ["TrueNAS","NAS","Network Attached Storage","Storage","Hardware","Linux","Media","DVD","Blu-Ray","Networking"]
categories: ["Linux","Media","Hardware","Networking","Computer Refurbishing"]
---

### Most of the hardware is assembled

The past few weeks have been extremely busy, so I knew last night would probably be the only time I would get this week to work on the NAS. I’m glad I started building the NAS last night as it took much longer than anticipated. I finally finished the build at 10pm last night (and it’s still not quite complete).

![Intel Core i3 7100 CPU close-up](/img/intel_core_i3_7100.webp)<figcapture>Fig 1. I used an Intel Core i3-7100 CPU for lower power consumption</figcapture>

### Using parts of our old KODI media centre

Part of the reason the build took so long was that I needed to use several parts from our existing KODI media centre. My wife and I are trying to make our space look less cluttered. And while the Corsair Spec 02 case our existing media centre was in really wasn’t a big eyesore, we’ve been loving the look of Tiny Form Factor PCs. Lately, the Computer Recycling Project has seen a number of TFF PCs come in, with decent specifications too (7th gen Dell Optiplex 3050s). One of these looks a whole lot better under a television than the Spec 02 machine. Because the NAS is only 4 drives, I could have built it in the SPEC 02 case, but there were several reasons why I didn’t:

- The motherboard in that build didn’t have a back plate, and while this doesn’t affect the performance, have that much more open space allows for a lot more dust to settle in the system.
- There’s not much space for drives, and in that cramped space the 4 drives would likely heat up much quicker.
- I have more media than space, even with the new drives I’m not sure the additional space will stay free for very long. Being able to expand in the future (even if I have to copy to dozens of other smaller drives and rebuild) is important.

With that in mind I bought a Fractal Design Refine 5. Cases that support more than 2 x 3.5″ drives are really hard to find. Even at the Computer Recycling Project we rarely see cases with lots of drive space and all the equipment to mount those drives. The Refine 5 wasn’t cheap ($165 CDN), but at least it was on sale when I bought it.

In my last post I mentioned I planned on using another, untested motherboard, an ASUS Prime Z270-A. That motherboard actually came with an Intel Core i7-7700K CPU, but I decided against using that CPU as it draws 40 watts more than the Intel Core i3-7100 in our existing media centre. I also pulled the Corsair 750W power supply, RAM, and the Corsair H100i AIO. Pulling out the power supply and AIO turned out to be more time consuming than expected as everything was a pretty tight fit in the AIO.

### The Fractal Design Refine R5 – good, but far from perfect

I really like the look and design of the Fractal Design Refine 5. It’s a tragedy that case manufacturers are opting to build less functionaly cases with RGB lighting, instead of including actual functionality (additional drives, 5 1/4 inch bays, etc.). Don’t get me wrong, I like RGB lighting, but I’ll take the added functionality over RGB lighting and clear side panels any day.

Here are some things that annoyed me about the Refine 5:

- The manual has great pictures, but little explanation. For the most part things are clear from the pictures, but having never built in a similar case things like the fan control connection were not as clear as could have been.
- Some things are out of order (optional steps). If you’re planning on building in this case with an AIO, remove the top panels BEFORE you put the motherboard in. It took me nearly 20 minutes to pinch those clips that have to be pinched in order to remove the top back panel. If the case was still empty this wouldn’t have been an issue. Some sort of forewarning, like “if you’re planning to use an AIO, remove the top panel(s) first)” would have been really helpful.
- A couple of spaces are tight. In order to put the 8 pin power connector through the top left I had to separate the connector into it’s 2 x 4pin parts and put them through the channeling, then reconnect them before attaching the connector to the motherboard. A bit more routing space would have been handy. Also, the fan connector on the back, and for my AIO, both use a SATA power connector which is pretty wide and difficult to keep flat against the back plane.
- My Corsair PSU has additional cables for molex, so I had to route them under the drive bays. I guess this case is really better if you have a modular power supply with separate cables. There was enough space to route/hide everything, but if I add more drives I’ll be changing power supplies.
- No USB-C. While I don’t use this much, it would have been nice to have on the Refine 5, or at least all USB 3.0.

### But there are good things about the Refine R5

There are some things I really appreciated about the case:

- Lots of space for drives, and well laid out. There’s actually even more space for drives using optional components, but I have no plans to go that crazy.
- I LOVE the trays Fractal Design chose. These trays proved really helpful as one of my Seagate Ironwolf 8TB drives (ST8000VN002) was not like the others (ST8000VN004). That first drive has fewer mounting holes on both the sides and bottom. Being able to adjust where the drive is mounted in the tray made it possible to reasonably mount the drive as I wanted in the case.
- The channeling is among the best in cases I’ve built in, with the exception of routing the 8 pin power cable I mentioned earlier. 
- Construction, it’s just a quality case.

### Things still to do

I didn’t get to everything last night. It was almost 10pm when I finally booted the system for the first time to a successful POST. The POST showed all 32GB of RAM, which was my main concern at 10pm. I didn’t get the chance to connect all the hard drives as it was too late in the evening. Part of the reason I didn’t connect them up was the fact that all the SATA data cables I had on hand were different, and I wanted some consistency. Luckily, there’s Computer Recycling, and cables are cheap ($0.50/each). I also didn’t put the Gigabyte GTX970 4GB video card in the system. When I tested for POST I used the ASUS Prime’s onboard video, which appeared to work just fine. I know the GTX970 works, as it was the card we used in our KODI media centre.

![The card that didn't make it into the case](/img/gtx_970_4gb.webp)<figcapture>Fig 2. Gigabyte GTX970 4GB video card</figcapture>

This evening my better half and I have some work to do, but I’m hoping to finally connect up the drives and install TrueNAS. I’m still torn whether to put the GTX970 in the build or not, it means more draw on the 750W power supply, but I believe software like [Jellyfin](https://jellyfin.org/) benefit from the 970.