---
date: '2023-05-30T20:25:37-04:00'
draft: false
title: '[Fix] Vikings - Wolves of Midgard crashing after kalypso startup screen'
cover:
    image: img/vikings_new_character.webp
    alt: "Vikings, Wolves of Midgard - new Warrior Character"
    caption: "Vikings, Wolves of Midgard - new Warrior Character"
tags: ["Gaming","Linux","Software","Steam","Xubuntu","Linux Mint"]
categories: ["Gaming","Linux"]
---

### Vikings – Wolves of Midgard (crashes after the Kalypso video)

Vikings – Wolves of Midgard is a linear action role playing game (ARPG) that lets you go back and repeat quests several times until you’re overpowered. Recently I’ve tried a number of role playing games only to find they were lacking in graphics, the controls were too jank, or they just required obscene amounts of time to make any progress. I like Vikings – Wolves of Midgard, because I find that despite the fact that the story is almost aways the same, you can complete quests over and over again until you’re overpowered. The controls are not bad, especially compared to some of the games I’ve played lately. Best of all it runs natively under Linux.

The one big problem I’ve had with the game lately is that the game completely crashes right after the Kalypso introduction video, with no chance to play the game.

### A solution for Xubuntu Linux

I found that if you moved the 3 Kalypso video files to another folder, the screen temporarily goes white, then the game loads. For me these files were located:

```shell
/home/chaslinux/.steam/debian-installation/steamapps/common/Vikings - Wolves of Midgard/vikings_Data/StreamingAssets/videos/
```

On your system replace chaslinux with whatever your login username is, so if you log in with a user name of peterm it would be:

```shell
/home/peterm/.steam/debian-installation/steamapps/common/Vikings - Wolves of Midgard/vikings_Data/StreamingAssets/videos/
```

In the videos folder I simply created a folder called temp and I moved logo_kalypso.mpv, logo_kalypso.ogv, and logo_kalypso.webm to the newly created temp folder.

After doing this the game launched and I was able to play.

![Inventory screen - Vikings, Wolves of Midgard](/img/vikings_character_inventory.webp)<figcaption>Fig 1. Vikings, Wolves of Midgard - inventory</figcaption>