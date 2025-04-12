---
date: '2023-07-07T18:54:33-04:00'
draft: false
title: 'Fasteroids - An Asteroids-like game for Linux and Windows'
cover:
    image: img/fasteroids-game.webp
    alt: "Fasteroids for Linux and Windows"
    caption: "Fasteroids, my Asteroids-like game for Linux and Windows"
tags: ["Game Development","Gamedev","Asteroids","Linux","Windows","SHMUP","Xubuntu","Linux Mint"]
categories: ["Game Development","Gaming"]
---

### Reviving an old project
Today I realized that, since redoing this web site, I still haven’t added any information about the game I made back in 2017-2020. Recently I revived Fasteroids, and made some changes to both simplify the game, but also with the idea that the game should be able to scale to 4k in the near future.

Before I ramble on more, you can download Fasteroids for Linux or Windows from:

(https://chaslinux.itch.io/fasteroids)

> **Note:** I've since squashed some bugs from version 2.39, and removed this old version. Use version 2.40.
> This is a repost from the old web site. While I haven't worked on Fasteroids in the past few weeks, it's still
> on my radar.

Version 2.37 of Fasteroids is an old version I released back in 2020. The latest version of Fasteroids is 2.39. Version 2.37 of Fasteroids is dramatically different from 2.39. Version 2.37 targeted one resolution 1024×768. All menus and visual elements were made to fit that screen size. Version 2.37 also only worked with *buntu Linux distributions up to 20.04. If you upgraded to *buntu 22.04 you were out of luck running Fasteroids 2.37 as a library that was in 20.04 isn’t the same version as in 22.04.

The latest version of Fasteroids I released this morning is 2.39. This new version drops the resolution of the game down to 640×360. More on the reason for the drop in resolution below (future upgrade). Another *BIG* difference is 2.39 for Linux is now an AppImage. This means that anyone using a Linux distribution that can run FUSE/AppImages should be able to run Fasteroids. This latest version is also compiled rather than using GameMaker’s VM runner, meaning less overhead, and theoretically better performance.

640×360 is one of the resolutions in the 16:9 aspect ratio. The idea is that I’ll scale graphics up to other 16:9 resolutions. At this point I’m thinking about scaling the game to the following resolutions: 1280×720 (SD), 1366×768 (WXGA), 1600×900 (HD+), 1920×1080 (FHD), 2560×1440 (WQHD), and 3840×2160 (4K).

While 2.39 is limited to 640×360 I’m not far off writing the code to switch to other resolutions. This is likely going to also require the Asteroids, the UFOs, the main ship, and the bonus buff’s all be redrawn. It’s been a few years since I created the original artwork (GIMP and Aseprite). Things may look a little blurry/jank until I get some more drawing as sprite creation practice in again.

I’m using a few methods to track work:

- The Fasteroids itch.io devlog: (https://chaslinux.itch.io/fasteroids/devlog)
- Trello: (https://trello.com/b/z67tqsLC/fasteroids)
- Google Docs – this one is for my own notes when I’m not at home

If you’re on Xubuntu (or another) Linux, you might need to set the AppImage to be executable. Right click on the Fasteroids-2.39.AppImage, select Properties, switch to the Permissions tab, then check the check box that says “Allow this file to run as a Program.”

Or, in a terminal, change to the directory where Fasteroids-2.39.AppImage is located and type:

```shell
chmod ugo+x Fasteroids-2.39.AppImage
```

This should add the execute bit to the AppImage so when you next open it up it runs. For Windows there is both an Installer and a Zip file containing an EXE that can be run in place.

> One *bug* I noticed with Xubuntu Linux is that it does not seem to display AppImage icons correctly. If you download 
> the Fasteroids AppImage you'll see that it looks like every other AppImage on Xubuntu, a silver box with a gear. 
> Linux Mint XFCE seems to display the icon correctly. I'm not sure what they have implemented that the Xubuntu project
> hasn't, but I hope a fix is in the future.

![AppImage icons show on Linux Mint](/img/appimages_show_on_Linux_mint.webp)<figcation>Fig 1. AppImage icons show on Linux Mint XFCE</figcaption>

If you enjoy the game please reach out to me on Mastodon: [@chaslinux@techhub.social](https://techhub.social/@chaslinux).


