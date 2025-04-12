---
date: '2025-01-17T12:13:40-04:00'
draft: false
title: 'How to play Jazz Jackrabbit on Linux'
cover:
    image: img/openjazz_titlescreen.webp
    alt: "OpenJazz title screen"
    caption: "OpenJazz is a Linux front end to Jazz Jackrabbit"
tags: ["Gaming","Linux","Software","Steam","Xubuntu","Linux Mint"]
categories: ["Gaming","Linux"]
---

### Jazz Jackrabbit – an introduction

Back in 1994 the World Wide Web (WWW) was just starting to catch on, mostly via a dial-up connection. Bulletin Board Systems (BBS) were starting to be on the way out, but at the time I was running a bulletin board for a local computer club. One of the attractions of bulletin board systems (besides online games/aka doors, message boards, and chatting) were the extensive “shareware” software collections. If you weren’t going to a computer store to buy software, you were probably calling a bulletin board to download shareware or freeware software. Shareware software became known as “try before you buy” software. In most cases software was fully functional, but limited in some way (for example: a game where you could play the first few levels, but if you wanted more, you had to send the shareware author money for the rest of the software).

One of the really popular games you could download from a bulletin board was the shareware version of Epic MegaGames’ Jazz Jackrabbit. Jazz was similar to the commercial game Sonic the Hedgehog in the sense that the idea was to speed through the level as fast as possible. In Jazz Jackrabbit you’re Jazz, a Jackrabbit who must speed through levels in order to rescue Eva Earlong, your girlfriend, from the evil turtle Devan Shell. On the way you blast through other enemies, pick up various weapons, and pass by game save points.

Jazz was pretty graphical for the time and had a fair amount of polish.

### OpenJazz

OpenJazz was started on the 23rd of August, 2005, by Alister Thomson. Others later ported the projects to other operating systems and platforms. OpenJazz isn’t playable on it’s own, it needs either the shareware files or full files from Jazz Jackrabbit. It’s important to note that OpenJazz only works with Jazz Jackrabbit 1 files, files from Jazz Jackrabbit 2 will not work with OpenJazz. Additionally, I found some files, like the Holiday Hare shareware files resulted in the title screen looking a bit glitchy (this went away when I pressed ESC and started playing the game).

OpenJazz has some issues, but these are mostly due to the fact that games back then didn’t autoscale to the current resolution. When I installed OpenJazz and launched it with Holiday Hare it launched at a very low 320×200 resolution. Thankfully the resolution can be adjusted in game, but adjusting the resolution doesn’t necessarily adjust all screens (the storyline screens for example stayed at the lowest resolution). There are work-arounds – I lowered the display resolution of one of my monitors to better match the game.

OpenJazz also lets you run the game with a number of “switches.”:

```shell
OpenJazz -f ~/PATH_TO_JAZZ_FILES
```

The -f switch runs Openjazz in full screen mode. When running OpenJazz you have to specify the path to where the extracted Jazz Jackrabbit files are. OpenJazz can also take the following other switches:

- \-window : start in windowed mode
- \-m : start with muted audio
- \-s : scale the window by a factor (1 to 4)
- \-w, \-l : directly load a specific world/level
- \-q : no logging
- \-verbose : log much more than the default logging
- \-v : display the version of OpenJazz (and when it was built)
- \-h : display help for OpenJazz

I was not able to jump to a specific level using the -l switch, but when I tried I was using the Holiday Hare pack. I expect using something like the files from the full paid edition of Jazz Jackrabbit would have worked.

### Installing OpenJazz on Xubuntu and Linux Mint

OpenJazz is in the software repositories for Xubuntu 24.04.1. I also checked Linux Mint 22 and found the same openjazz package in Linux Mint 22. To install OpenJazz open a terminal (CTRL + ALT + T) and type:

```shell
sudo apt install openjazz
```

Note that when you install the OpenJazz software package everything has to be lowercase as the software package is named in lowercase and Linux is “case sensitive.” Sadly, the actual executable is a mix of upper and lowercase letters: OpenJazz, so when starting the game you have to capitalize both the O and J. Funny enough though you can read the manual (man page) by typing the lowercase name after man: 

```shell
man openjazz
```

### Starting the game 

As mentioned earlier, in order to play Jazz Jackrabbit, you either need the original game files, or one of the shareware files. I found the Holiday Hare files and extracted them to my \~/Downloads directory. (If you’re unfamiliar with Linux command line shortcuts, the tilde (~) symbol refers to your home directory. In my case /home/chaslinux. So \~/Downloads refers to a full path of /home/chaslinux/Downloads). The extracted directory was called Jazz95. In order for me to run the Holiday Hare files using OpenJazz, the full command was:

```shell
OpenJazz ~/Downloads/Jazz95
```

Alternatively I could have typed the full path:

```shell
OpenJazz /home/chaslinux/Downloads/Jazz95
```

Learning a bit about command line commands saves a lot of typing and makes life a lot simpler.

### Retro-rewind

Jazz Jackrabbit is one of a number of “classic” games that are playable under Linux (albeit with a bit of effort). Among other classic games within apt repositories are Tyrian (opentyrian), Doom (various), Paradroid (freedroid), and Puzzle Bobble (as frozenbubble). I’m sure there are many more I’ve missed, and this excludes a lot of classic commercial games that are still selling via platforms like Steam. I picked up one of my favourite games of all time Heroes of Might and Magic III via Steam, and it’s fully playable under Linux via Proton… but that’s for another post.
