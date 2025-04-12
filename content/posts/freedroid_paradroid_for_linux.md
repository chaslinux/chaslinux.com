---
date: '2024-05-31T11:20:47-04:00'
draft: false
title: 'Freedroid - Paradroid (C64) for Linux'
cover:
    image: img/freedroid.webp
    alt: "Freedroid is an open source version of Paradroid, a popular game for the Commodore 64"
    caption: "Freedroid"
tags: ["Gaming","Linux","Freedroid","Paradroid","C64","Commodore 64","Retro","Retro Gaming","Classic Gaming"]
categories: ["Gaming","Linux","Software"]
---

### Paradroid, has a version for Linux

Growing up in the Commodore 64 era, I’m particularly fond of the games of that age. Games in that era tended to be simpler, but sometimes within that simplicity were some really neat concepts. Paradroid was one of those games that was particularly unique and interesting.

There’s a really good look-back at Paradroid on the LemonTube64 Youtube channel here:

(https://youtu.be/kkEBccMEhXs)

Freedroid “classic” is a port of the game to Linux. The website for Freedroid classic might be a bit confusing when you first arrive because the same developers also worked on an isometric 3D-like game they called FreedroidRPG. The web site for both is:

(https://www.freedroid.org)

Currently there is no mention of Freedroid classic on the landing page for FreedroidRPG, but if you go to the Download page, it’s mentioned about half-way down.

### Installation of freedroid classic is easy

To install Freedroid classic on Xubuntu Linux simply open a terminal (``Windows + T key``) and type:

```shell
sudo apt update
sudo apt install freedroid
```

If you then open the Xubuntu whisker menu in the top left and type freedroid you should find the game… but if you run the game from the terminal you can also add “switches” to do things like make the window larger, launch in full screen mode, launch with no sound, launch with debugging turned on, etc.

### Gameplay

In Freedroid classic you start as a 001 droid, the lowest of the low in the droid pool. In the game you’re on a massive ship that’s full of droids that are more powerful than your starting droid. To win the game you have to destroy all the droids on all levels. Sounds simple enough, but the game has a few twists.

As a 001 droid you’re relatively weak. It takes several shots to destroy robots with larger numbers. But don’t fret, you possess an “influence device” (a helmet) that lets you try to take over other droids if you hold down the fire key when you crash into them. Be aware that droids who crash into you weaken your shields. If too many droids crash into you, or you’re fired upon by a sufficiently powerful droid, it’s game over.

When you crash into another droid with the influence device activated a mini-game opens up. At the start of the mini game you have a few seconds to pick a side you want to be on (various colours, generally one light, one darker). Depending on the side there are routed wires that go to the center. The idea is to pick the correct set of wires so that your colour is dominant.

![320 robot trying to take over a 420](/img/freedroid_takeover.webp)<figcaption>Fig 1. Freedroid - 320 robot trying to take over a 420</figcaption>

Things that affect the mini (wire) game:

- As a low level robot you have fewer wires you can use
- Some of the wires fork, both to your advantage and disadvantage
- Time counts down quickly as you choose which wires to take
- Once you pick a wire, you cannot unpick it

The first couple of times you try the game things are a bit confusing, in part because you first have to pick a side, but then as you get used to how the mini-game works. At the end of the countdown if more wires are your colour, you win and take over the robot. If more wires are in the opposing robots colour, you lose. If the center turns black, it’s a stalemate and you both go again.

In addition to other droids there are consoles you can check out, shield-restoring squares (at the cost of game score), and transfer areas that you can use to go to another level. Be careful not to jump to the highest levels right away. The higher the droid number, the more likely they are to fire, and the stronger they tend to be (both shield and firepower wise).

![The ship elevator](/img/freedroid_moving_levels.webp)<figcaption>Fig 2. Freedroid - taking the elevator</figcaption>

Freedroid is an awesome port of this wonderful game. If you enjoy old school games, or just have old hardware and want to try something different, give Freedroid Classic a try.

### Be the best robot you can

As a 001 your weapon sucks, but as you take over more powerful robots your weapon's power gets stronger, but the most fun lies in trying to take over stronger robots. You can choose to try to shoot more powerful robots, but they might get you before you get them. And yes, I managed to take over the 420!

![Freedroid - Now a 420 robot](/img/freedroid_420.webp)<figcaption>Fig 3. Freedroid - I took over the 420</figcaption>