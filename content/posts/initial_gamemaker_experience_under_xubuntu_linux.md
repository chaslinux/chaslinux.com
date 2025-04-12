---
date: '2023-08-03T13:32:33-04:00'
draft: false
title: 'Initial GameMaker experience under Xubuntu Linux'
cover:
    image: img/gamemaker_under_linux.webp
    alt: "GameMaker running under Xubuntu Linux"
    caption: "Some of the code for Pong in GameMaker running under Xubuntu Linux"
tags: ["Game Development","Gamedev","GameMaker","Linux","Xubuntu","Programming"]
categories: ["Game Development","Linux","Programming"]
---

### Previous GameMaker experience

I bought version 1.4 of the Gamemaker game engine on a Humble Bundle many years ago. At the time Gamemaker ONLY ran under Microsoft Windows. It was possible to export games to Linux (Ubuntu/Debian-specifically), but you couldn’t run the game engine itself under Linux. Version 2.x came along, and I paid to upgrade to 2.x as well.

Some time between when I bought 1.4 and 2.x I started working on my Asteroids-like clone, Fasteroids: (https://chaslinux.itch.io/fasteroids). Many professional developers suggest starting and finishing a project as quickly as you can, then moving on to something else. Of course I didn’t listen and kept adding “features” to Fasteroids, which lead to the game being pretty messed up, and me losing interest.

Then Opera bought YoYo games and turned Gamemaker into a subscription model… this made me swear off Gamemaker, despite the fact that I really enjoyed working in GML. But Opera did one thing that’s made me reconsider, they made a version of the engine that runs under Linux.

### Can you code a game simple in Linux?

Part of my day job involves refurbishing computers with Xubuntu Linux (**Update:** Linux Mint) and promoting them among the community as a less expensive alternative to new or refurbished systems with Microsoft Windows. Asking people to make the leap from Windows to Linux can be a big challenge. The past couple of days I asked myself the question “what would be the best game engine to use in Linux?”

The most obvious answer to the question above, given what I know about Linux, is the Godot game engine. Godot exists in the Xubuntu/Ubuntu software repositories, so it can be installed right from the “software” program in Xubuntu – no extra files needed from the Internet.

I tried Unity, the big kahuna of game engines, a couple of days ago, and despite everything working, the experience wasn’t as good as the brief experience I’ve had with Godot under Linux. This left me wondering, how bad could the Gamemaker beta for Linux client be? Could I actually code a game with it?

I’m happy to say the answer is a definite “Yes!”

### Gamemaker engine for Linux? What engine?

Opera, the company that bought out Yoyo Games, the previous company behind the Gamemaker engine, hasn’t made it obvious where you can download the Linux version. The Windows and MacOS versions of Gamemaker are pretty easy to find, but there’s no obvious links on their web site to the Linux version, which is a shame, because despite their “this could corrupt your game files” warning, I found the engine to be stable enough that when I shut down with a project open, the project was fine when I started up again.

> I have since put many of the steps here into a shell script. The script doesn't download the GameMaker engine Debian package, but it installs all the
> dependencies the engine requires for Xubuntu 24.04.2. You can clone the script from github at: (https://github.com/chaslinux/gamemaker-install)

To download Gamemaker for Linux you’ll first have to satisfy some dependencies, open a terminal and enter the following commands:

```shell
sudo apt update

sudo apt install build-essential openssh-server clang libssl-dev libxrandr-dev libxxf86vm-dev libopenal-dev libgl1-mesa-dev libglu1-mesa-dev zlib1g-dev libcurl4-openssl-dev ffmpeg libfuse2 curl -y
```

The first command updates the online software library. The second command downloads and installs several libraries and programs Gamemaker uses. Now we need to download some Steam-related files needed by Gamemaker. Note: you don’t need a Steam account, these are for Steam support within Gamemaker (Software Development Kit).

```shell
sudo mkdir /opt/steam-runtime/

curl https://repo.steampowered.com/steamrt-images-scout/snapshots/latest-steam-client-general-availability/com.valvesoftware.SteamRuntime.Sdk-amd64,i386-scout-sysroot.tar.gz | sudo tar -xzf - -C /opt/steam-runtime/
```

A great feature of newer versions of Gamemaker is the ability to make AppImages. AppImages are awesome because they can be run on any Linux distribution that supports “fuse.” What this means is you can develop a game on Xubuntu/Ubuntu and run it on Fedora Linux without needing to make any changes to the code. The same AppImage that runs on Ubuntu will run on Fedora Linux.

```shell
wget https://github.com/linuxdeploy/linuxdeploy/releases/download/continuous/linuxdeploy-x86_64.AppImage

sudo install -m 0755 linuxdeploy-x86_64.AppImage /usr/local/bin/linuxdeploy

wget https://github.com/AppImage/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage

sudo install -m 0755 appimagetool-x86_64.AppImage /usr/local/bin/appimagetool
```

Finally, get the .deb (Ubuntu/Debian package) for Gamemaker from: 

(https://gms.yoyogames.com/ReleaseNotes-NuBeta.html)

Click the Ubuntu download and install the .deb file using the software centre. Gamemaker can now be found in the whisker menu under Xubuntu, just open the menu and start typing gamemaker.

This beta version only makes games for Opera’s gx.games. In order to compile for other targets you’ll need to purchase a Creator ($4.99USD/mo), Indie ($9.99USD/mo), or Enterprise license ($79.99/mo). Indie adds exporting to web and mobile (other than gx.games), Enterprise adds exporting to consoles.

### Monthly subscription is not the way to go

> Shortly after I initially wrote this article I contacted the GameMaker team indicating I didn't want to buy month-to-month, but would be happy to buy a year
> worth of GameMaker (I despise monthly subs). Not long after the team switch back to the 1 time payment model... And they granted me a professional license for 
> buying the year sub. This is one of the reasons I've stuck with GameMaker, it seems the team really do care about the community.
> I've kept the post as I initially wrote it, but am adding this to show the team changed the model for the better.

I feel the monthly subscription model Opera has chosen for Gamemaker is not going to attract new developers to Gamemaker. When I bought Gamemaker 1.4, it was 7 months before I started using Gamemaker. Some argue that you’re more likely to use software if you’re paying for it each month, but I’m not convinced, here’s why:

Many years ago I picked up a book something like “Learn MySQL in 24 hours.” I spent the first couple of days going through the first six chapters of the book and then I got stuck, really stuck. I put the book down for approximately 6 months, then picked it up again and wondered “how the heck did I get stuck on that problem…” I’d learned the answer somewhere else, but I needed to step away from MySQL for awhile and come back to it. I can see something like this happening with Gamemaker as it’s sometimes difficult just to bend your head around game design principles.

One of the reasons I promote Free and Open Source Software is that it tends NOT to have a monthly subscription model. 

### Ping pong

When I first started learning Gamemaker years ago I found Sara (ne: Shaun) Spalding’s tutorials really helpful. So when trying out Gamemaker under Xubuntu I wanted a fast way to create a basic game… I chose Sara’s Pong tutorial as a quick (in under 15 minutes) way to test creating a game:

(https://www.youtube.com/watch?v=yjt75sdH9h8)

It took me a bit more than 15 minutes, but not a lot more (25 at most) to complete this tutorial. One of the problems I ran into is when I created resources using a hot key combination, they didn’t automatically get assigned to the appropriate tree structure area. For example, if I created a sprite, or an object, both were at the bottom of the Asset Browser, below Timelines. I needed to drag the sprites and objects up to their appropriate area – something a complete Gamemaker newbie might have missed.

That said, the game worked!

![Pong game made in GameMaker under Linux](/img/pong-game.webp)<figcpation>Fig 1. Pong game made using GameMaker under Linux</figcaption>

### Overall impressions

I really like Gamemaker as an engine. It looks like Opera is doing some good things with Gamemaker… but the monthly subscription is a bit of a show-stopper for me. I’d prefer to buy the engine outright every couple of years rather than pay a monthly subscription. I work full time, and creating games is a hobby for me. I know some people pay monthly subs to play games like Warcraft, but that’s never been my thing. I prefer to just buy something once or twice. I don’t like “yet another thing I have to track every month…”

Gamemaker shows promise under Linux. The engine was stable enough that when I shut down the computer with Gamemaker and my project open, nothing got corrupted.

I expect I will probably transfer my game-making skills to Godot, which is completely free. I’m going to try sticking with Gamemaker for a bit and give some updates as I discover new things about the engine under Xubuntu Linux.