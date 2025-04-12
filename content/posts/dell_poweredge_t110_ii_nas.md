---
date: '2024-06-01T09:38:18-04:00'
draft: false
title: 'Dell PowerEdge T110 II Network Attached Storage (NAS) build'
cover:
    image: img/poweredge_t110.webp
    alt: "Dell PowerEdge T110 II workstation"
    caption: "Dell PowerEdge T110 II workstation"
tags: ["TrueNAS","NAS","Network Attached Storage","Storage","Hardware","Linux","Media","DVD","Blu-Ray","Networking"]
categories: ["Linux","Media","Hardware","Networking"]
---

### Migrating the KODI entertainment system

On May 5th I mentioned that we’re Running out of space on our media center. In the comments of that post I followed up outlining a plan to buy another 8TB drive (for a total of 3 x 8TB drives) in order to do a RAID Z1 (for 16TB of space). But in order to do that I would need to reformat the drives, which means I also needed a plan to back up our media center data. I hinted at that solution in the comments too: 4 x 3TB drives in a RAID Z1 – which would give me 9TB of space (1 x 3TB is the spare), just enough to back up all the data.

At first I was thinking of putting the drives in my old Antec Three Hundred Two Atermiter X79 XEON build (the machine we use for ripping media), but that machine is in heavy use, doubling as a media center in another room, on top of it’s ripping duties. I’ve been watching quite a few NAS build videos lately, and noticed in the comments someone mentioned the Dell PowerEdge T110 II, a Dell workstation with room for 4 x 3 .5″ drives. The Working Centre’s Computer Recycling Project just happened to have a T110 II with a Pentium G620 processor. The project has been running a sale on desktop machines and workstations. The project has a base price for 1st gen Core i3’s at $50, the half-off sale means the 1st gen i3’s are going for $25. This G620 is one step down from the i3’s, so I got it for $20. The machine came with 8GB DDR3 (I haven’t checked to see if it’s ECC or not) and a 1TB drive, which I donated back to the project.

### Drives, this could be a problem…

My original plan was to use 2 x 3TB Seagate Constellation drives and 2 x 3TB Seagate Barracuda drives, but one of my 3TB Barracuda drives appears to be completely dead. As an aside, I’ve been wiping lots of drives at the project lately and it’s been a 50/50 split between WD/Seagate drive failures so far. I have a 3TB WD Red, but I’m not sure mixing and matching all these various drives is going to work. My fingers are crossed that what really matters is they’re close in size to each other.

![3D printed slot mounting bracket for the boot SSD](/img/ssd.webp)<figcaption>Fig 1. 3D printed slot mounting bracket for the boot SSD</figcaption>

I also wanted to have a solid state OS/boot drive. The system is pokey enough that it would really benefit from an SSD. My initial plan was to 3D print a riser card that I could attach on the back of the T110 II where the PCI slots are. I had to rethink this because of the large plastic baffle that covers the processor and RAM. The baffle prevents the short SATA power cable from routing nicely to the slots. I’ll use this 3D printed riser in a different system, it’s pretty handy. At the moment I’m printing a 5 1/4 tray with mounting holes for both 2.5 and 3.5 inch drives.

This also brings up the fact that I needed to disconnect the DVD drive in order to accommodate the SSD, but I never planned on using the DVD drive anyway, so it’s not a big deal.

### Operating system

The plan thus far is to put TrueNAS Scale on the system. I have Scale on a machine at work and so far it’s been very reliable. I still need to wait on the SSD mount and dig up my WD Red to test and see if this is going to work as expected or whether I need to pick up another Constellation or two. Sadly, The Computer Recycling Project doesn’t have a lot of large drives, and most of the big drives the project has (2TB) have failed. I have a few other sources I can pick drives up from, and I’ll provide more details if it ends up I have to buy other drives.

![Two stacks of Seagate Hard Drives](/img/hard_drives.webp)<figcaption>Fig 2. 3TB Seagate Hard Drives</figcaption>

### Not the ultimate plan, this is just an intermediate step

Neither the media center upgrade, nor this side backup project are my ultimate storage plan. These are small steps towards a larger capacity NAS. We need a NAS for our media center, but we also need storage for future YouTube videos, and some storage for synchronizing our cell phones (neither of us rely on Google Drive).