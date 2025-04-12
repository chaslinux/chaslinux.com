---
date: '2024-05-31T11:47:15-04:00'
draft: false
title: 'Prince of Persia for Linux'
cover:
    image: img/sdlpop.webp
    alt: "SDLPoP - open-source port of the DOS game Prince of Persia"
    caption: "SDLPoP - open-source port of the DOS game Prince of Persia"
tags: ["Gaming","Linux","SDLPoP","Prince of Persia","DOS","Retro","Retro Gaming","Classic Gaming"]
categories: ["Gaming","Linux","Software"]
---

### Prince of Persia - a classic game for DOS

When I first ran Prince of Persia on PC-DOS I remember thinking, “finally, a DOS game that rivals the fun I had on Commodore 64 games.” I was never very good at the game (and that continues today), but it’s a classic game.

The original DOS version has a port for Linux which you can find on github here:

(https://github.com/NagyD/SDLPoP?tab=readme-ov-file)

### The simplest method to install SDLPoP on Ubuntu/Xubuntu Linux

If you’re on Xubuntu, or another Ubuntu-variant, there is a snap for the game (called sdlpop). To install the snap simply open a terminal and type:

```shell
sudo snap install sdlpop
```

Snap may take a minute to install all the necessary files, but once it does you can find SDLpop in the Xubuntu whisker menu. But I recommend launching it from the terminal, as you can launch it with options. If you type:

```shell
sdlpop full
```

SDLpop will launch in full screen mode.

![SDLPoP - playing the open source port of Prince of Persia](/img/sdlpop_action.webp)<figcaption>Fig 1. Playing SDLPoP on Xubuntu Linux</figcaption>

SDLpop is more than a clone of Prince of Persia, it’s been expanded on to include more options than the DOS version had. If you compile the code yourself you can also modify SDLPoP.ini. While the file exists in the snap version of SDLpop it can’t be modified because the snap format prevents this (for security reasons).

I couldn’t find SDLpop in flathub, so it doesn’t appear to be available as a flatpak (which means it isn't as simple install for Linux Mint or Debian users).

### Compiling SDLPoP

If you want a bit more control over SDLPoP there’s a configuration file SDLPoP.ini that can be modified in the compiled version. Sadly this file cannot be modified in the snap version of SDLPoP (for security reasons snap won’t let you modify snapped files — in general). I found compiling SDLPoP was not that difficult.

First clone the git repository (make sure you have git installed of course – ``sudo apt install git -y``):

```shell
git clone https://github.com/NagyD/SDLPoP
```

SDLPoP needs a the libsdl2-image-dev library before you can compile SDLPoP. I also always recommend installing build-essential as it covers building quite a bit of software.

```shell
sudo apt install libsdl2-image-dev build-essential -y
```

With these installed change into the cloned repository directory and then the src directory, then make and sudo make install. (If you later want to uninstall you can run sudo make uninstall in the same directory).

```shell
cd SDLPoP/src/
make
sudo make install
```

After you run SDLPoP you should be able to find SDLPoP by clicking on the Xubuntu whisker menu in the top left and typing sdl.

When SDLPoP is first run you’ll notice it defaults to a pretty small size 640×400 (16:10 aspect ratio). There are a couple of things you can do to make it larger. The first thing, which works both in the snap and compiled version is to press ESC to bring up the SDLPoP menu, use the keyboard arrow keys to navigate to Visuals, then turn on the full screen mode. This will put SDLPoP in full screen mode.

![Options screen for SDLPoP](/img/sdlpop_options.webp)<figcaption>Fig 2. SDLPoP options screen</figcaption>

The second thing you can do, which only works in the compiled version, is to modify the SDLPoP.ini file. Unlike a lot of software I’ve compiled, SDLPoP doesn’t move itself into /usr/share, or a system folder. When you compile SDLPoP it compiles in place, meaning that the binary (prince) is made in the SDLPoP directory you pulled from github. For example, on my system it went to:

```shell
/home/chaslinux/Code/SDLPoP
```

I like to put all my github projects in a directory off my home directory called Code (/home/chaslinux/Code). If you just clone the repository into your home directory it would be something like /home/chaslinux/SDLPoP.

You can just change into the SDLPoP directory and modify the SDLPoP.ini file:

```shell
cd SDLPoP
mousepad SDLPoP.ini
```

On Linux Mint replace mousepad (above) with xed, the editor used in Linux Mint Cinnamon and XFCE. Because the file is stored within your own home folder you won’t need elevated sudo privileges to edit the configuration file. Mousepad is the default text editor in Xubuntu. If you’re using another distribution like Ubuntu you might have to use another editor like xed, gedit, vi, or nano.

Under the General section of the file modify the lines:

```shell
pop_window_width = default
pop_window_height = default
```

You’ll want to use something that’s one of the 16:10 aspect ratio resolutions to make sure SDLPoP scales correctly (looks right). I’m on a fairly large screen so I chose 1680 x 1050.

```shell
pop_window_width = 1680
pop_window_height = 1050
```

![Running SDLPoP at 1680x1050](/img/sdlpop_1680x1050.webp)<figcaption>Fig 3. Running SDLPoP in a window at 1680x1050</figcaption>

There are a number of other options that can be changed in this SDLPoP.ini file. Some of those options can also be passed on the command line if you launch SDLPoP in a terminal. The command to run SDLPoP is prince (as in Prince of Persia), but the executable file is located outside of the normal PATH the BASH shell understands. So if you just try to run prince from your home directory you might get a:

```shell
prince: command not found
```

To make prince findable to your BASH shell you’ll have to add the path to the prince binary to your .bashrc file. As I mentioned earlier, in my case the path is /home/chaslinux/Code/SDLPoP. The .bashrc file is located in your home directory:

```shell
cd ~
nano .bashrc
```

At the end of my .bashrc I added the line:

```shell
PATH=$PATH:/home/chaslinux/Code/SDLPoP
```

Note the $ after the second PATH, and the colon before the path to the prince executable. In the example above replace ``chaslinux`` with your username. You don’t need to put the executable at the end of the path as everything in the SDLPoP directory will be added to the BASH PATH. Now close the initial terminal and open a new terminal, prince should now be executable from your home folder. Typing:

```shell
prince full
```

Launches SDLPoP in full screen mode.

I hope this helps someone, and that more people learn about some of the fun old school games we used to play, that are also available on Linux.

