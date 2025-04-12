---
date: '2023-11-02T09:28:49-04:00'
draft: false
title: 'Updating Discord on Xubuntu Linux'
tags: ["Gaming","Linux","Xubuntu"]
categories: ["Gaming","Linux","Communication"]
---

### Great, and a pain

Discord is one of those programs I love to hate. I like Discord because it’s a good way for people to connect with me about Computer Recycling, and I find it really handy for connecting with people about Game Development and Game Jams. But the process for updating Discord on Linux isn’t good. Normally, I update most software on my system by opening a terminal (Windows Key + T) and typing:

```shell
sudo apt update && sudo apt upgrade -y
```

This is really two commands: sudo apt update, which updates information about what updates are available from online sources, and sudo apt upgrade, which does the actually upgrading. The -y at the end is just to automate the process of pressing Y to say “yes, I want to upgrade.” The && in the middle processes the second command after the first, without needing a separate command/line to do it.

Discord doesn’t do this. Whenever Discord “finds” an update it prompts the user to download the new .deb package, but it doesn’t do any updating on its own. On top of this, if you double click the Discord .deb package to open it with the Software Centre, it won’t update it.

To “upgrade” Discord, I first remove it (which doesn’t remove the settings), then I add it again from the newly updated package. From the terminal:

```shell
sudo apt remove discord -y
cd ~/Downloads
sudo dpkg -i discord-0.0.33.deb
```

Of course, discord-0.0.33.deb would be replaced with whatever version was just downloaded. The next time Discord is launched, it does a bit of updating and then starts working again… until the next Discord update.

I believe there is a more sane way of updating Discord via snaps, and snap refresh, but I’m not sure if it gets updated as often as Discord gets updated. For now, this method works, but it’s not exactly convenient.

I would be remiss if I didn't mention a comment left by [@flyinsquirrel](https://flyingsquirrel.ca) noting that there is an Ubuntu/Xubuntu snap for Discord:

> FWIW, the discord snap seems to check for updates and installs them itself on launch. I’m not sure the snap itself gets updated, but it does its own 
> self-update inside its container.

I've been using the snap since Darcy mentioned it, and it's been a much better method for updating. To install Discord using snap under an Ubuntu variant (Linux Mint does not ship with Snap enabled by default, they prefer flatpak), type:

```shell
sudo snap install discord
```

### Debian packages appear in the software centre, but don't automatically update

Software installed through the Software program on Xubuntu normally gets updates when updates are available in the software repositories. But if you install a "Debian package" (.deb file) either using the Software program, or by command line using ''dpkg -i <filename.deb>'' the program will not get automatic updates. 

The reason the Debian package doesn't get updates is because it didn't come from the "online repositories" software installed through the Software program normally came from -- it came from a download that was done manually through a web browser. Thus, in order to update any software installed through a .deb package you first have to uninstall the package using ''sudo apt remove <packagename>'' or through the graphical Software program, then install the new version using either dpkg or the Software program.