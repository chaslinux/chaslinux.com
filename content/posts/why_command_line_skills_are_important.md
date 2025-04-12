---
date: '2025-01-16T06:41:34-04:00'
draft: false
title: 'Why command line skills are important - Troubleshooting...'
cover:
    image: img/flatpak.webp
    alt: "The flatpak command"
    caption: "Running the flatpak command in a terminal window"
tags: ["Linux","Xubuntu","Linux Mint","Shell Scripting","Troubleshooting","Command Line", "CLI"]
categories: ["Linux"]
---

### Introduction

Recently I was checking out Youtube videos about a Linux-related program, and I came across a comment in one of the videos that I’ve seen before (I’m paraphrasing this to not identify the video or commenter):

> *random comment on a Linux video:* "Those commands don’t work. In Windows, you don’t have to write a book to install something. I’m going back to Windows.”

The comment isn't a question, but a statement: `Linux is difficult, Windows is easier.`

Comments like this are not helpful because they lack context. They lack context because the comment didn't include any information other than "those commands don't work." Was the commenter using the same Linux distribution? Was the commenter using the same version of the distribution? Did they spell the commands correctly? Were the commands typed in the proper case (upper case and lower case matter)? What was the error? Too many people give up early because they think their experience with something else is easier, but is it better?

> For many years, I hated anything to do with cooking. Why would I want to learn to cook, when I could just buy something and microwave it? Cooking took too much time, and things often didn’t turn out - even following a recipe exactly.

This sort of parallel's the commenter's post in the sense that when I made an effort to do something, it never worked out for me. Then I met my wife, and she cooked for me, and I loved the food. I began to realize how much I missed home-cooked food. I started learning basic kitchen skills from videos. I started realizing some of the mistakes I was making. I was sure I was doing everything exactly as recipes perscribed, but I realized I wasn't. Temperature was wrong, because stoves vary. Time was wrong, because of the same issue. Ingredients weren't exactly the same, etc.

Slowly, I started learning more and more kitchen skills. To be clear, I wasn't inspired enough to be a chef (expert), but learning to cook made the process easier, and it felt a lot less like a chore. As a bonus, the quality of food I consumed got better.

I was just thinking of another example. The simple act of launching a program, Audacity comes to mind since it works on both Windows and Linux. In both Linux and Windows you can create a shortcut on the desktop to click or double click to launch. This involves moving the mouse close enough to the icon then clicking on it. To launch audacity from a terminal in Xubuntu Linux, hold down the windows key and press T to launch a terminal session… start typing the letters aud, then press the TAB key to complete the filename. Hit enter and audacity launches (unless you have several other programs, like audacious…, etc., in which you just have to press TAB again to see which others begin with aud).

But more than this… there’s another advantage to launching programs from the command line, sometimes you’ll see error messages you wouldn’t see launching the program graphically.

Recently I installed a program named planner on Xubuntu 22.04. Planner launched normally when I clicked through the menus and launched the icon. Nothing seemed out of place. But I then decided to launch it from the command line and noticed a message:

```shell
Failed to load module "atk-bridge"
```

Planner was working, but clearly something wasn’t 100%. There were several reddit, and other site posts that suggested trying things that didn’t work, but buried among those was the suggestion to install an “adaptor” program. In Xubuntu this turned out to be: libatk-adaptor.

A bit more digging and this seems to be related to letting planner, a program that uses some older technology, work with newer software.

Yes, planner worked without needing to install this extra piece of software. But installing the software was simple:

```shell
sudo apt install libatk-adaptor
```

The next time I launched planner from the command line, no warnings, no issues. The lesson, sometimes the command line can give you more information about an error/issue. If a program is failing to launch from the graphical user interface, try opening a terminal (``Windows key + T`` in Xubuntu) and running the command. If you’re not sure what the actual command name is right click on the item in the menu and select the ``Edit Launcher`` option. A new window will open up. In the new window the name of the command will be in the command section.

![Mate Calc launcher information in Xubuntu Linux](/img/mate-calc.webp)<figcaption>Fig 1. Mate Calc launcher information in Xubuntu Linux</figcapture>

### Shortcuts make the difference

In pre-Windows days, one of the most popular applications was Wordperfect for DOS. Wordperfect for DOS came with a template that fit around the function keys on a keyboard. That template contained “hot keys” for popular functions in Wordperfect. The fact that hot keys persist today in applications is a testament to the effectiveness of using hot keys.

It’s the same on the command line in Linux. Hot keys and shortcuts really make life simpler. I almost never move the mouse up to the menu, click on it, then click Terminal Emulator. It’s far easier for me just to hold down the ``Windows key`` on the keyboard and press ``T``. 

Tricks like filename completion (using the ``TAB`` key) really save a lot of time once you get used to using them. I’ve also discovered new commands, and remembered commands I used to use thanks to using TAB completion. TAB completion works like this: You start to type the first few letters of a command then press the ``TAB`` key, if nothing happens, then likely there is another command that begins with those first few letters. If you press the TAB key a second time it will display all the commands that begin with those first few letters. If there is no other command that starts with those few letters pressing TAB once will complete the whole command name. For example:

On the Linux Mint XFCE 21.3 system I’m on now if I type the letter ``f`` in a terminal and press the ``TAB`` key, nothing happens. If I press the TAB key a second time I’m prompted (y/n) if I want to see the 134 commands that begin with f.

![Display 134 possibilities](/img/f_tab.webp)<figcapture>Fig 2. F + Tab - display 134 possibilities (y/n)</figcapture>

If I then type ``ff`` and press ``TAB`` nothing happens. But if I press ``TAB`` a second time I see 4 commands displayed (ffmpeg, ffmpegthumbnailer, ffplay, and ffprobe).

![FF + TAB results](/img/ff_tab.webp)<figcapture>Fig 3. FF + TAB results</figcapture>

Similarly, if I type ``ffp`` and press ``TAB``, still nothing happens. This is because there are two programs installed on my system that begin with ffp (ffplay and ffprobe). The moment there’s a different letter TAB will complete the filename. So when I typed ``ffpl`` and pressed ``TAB``, TAB completion finished off the command adding the ay. This might seem like a lot of effort for two letters, and in this case it is, but some commands are a lot longer to type out, and TAB completion comes in really handy when it comes to those commands.

![ffplay and ffprobe results](/img/ffplay.webp)<figcapture>Fig 4. FFP + TAB results</figcapture>

The command uncompress is a good example of a command where you can save time by typing ``unc`` then pressing ``TAB`` to complete the ompress part of the command.

Combined with graphical user interface shortcut keys, command line shortcuts are really handy.

Another great command line shortcut is to use the ``up/down arrow keys``. These keys cycle up/down through your command history. If you’ve typed something particularly long and need to repeat it, pressing the UP arrow a few times is often quicker than typing out the whole command. Typing the word history in a terminal will let you look at the last 200 commands you’ve typed in the terminal. These are the commands the UP/DOWN arrow keys will cycle through.

![history](/img/history.webp)<figcapture>Fig 5. History results (using up/down arrow keys)</figcapture>

### How do you know what shortcut keys do what?

Many Linux distributions have graphical user shortcut keys stored within a keyboard program. In Linux Mint XFCE if you open the “whisker” (XFCE) menu and type ``keyboard`` into the menu, then click the keyboard program it will bring up a window/program with 3 tabs (behaviour, Application Shortcuts, Layout). Clicking on the ``Application Shortcuts`` tab reveals some of the shortcuts that can be used within Linux Mint XFCE. The “Super” key refers to the “Windows” key on some keyboards. Pressing ``Super + P`` on Linux Mint XFCE displays the Display program, letting you control things like your monitor’s resolution. This is a lot quicker than clicking the Whisker menu searching the menu for the Display program, then launching it. Most of the shortcuts can be changed within the keyboard program, so you can make key combinations that make more sense to you… just be sure to pick combinations that are not already being used by another shortcut.

![Keyboard shortcuts](/img/keyboard_shortcuts.webp)<figcapture>Fig 6. Keyboard/Application shortcuts</figcapture>

### Ditching the ALT key

There is another key we have to talk about, the ALT key. The ALT key is special is most Linux distributions. If you’ve ever tried using the Unity game engine, or another program that makes heavy use of the ALT key, you might have been met with some frustration, as some Linux distributions, like Linux Mint XFCE/Xubuntu use the ALT key for Accessibility options. But it’s not mapped under the Accessibility, nor the keyboard program. Instead look to the Window Manager Tweaks program. Type Window Manager Tweaks in the whisker menu in Linux Mint XFCE/Xubuntu and then launch the program. The Window Manager Tweaks has 6 tabs across the top. Select the Accessibility tab. In this tab the key used to grab and move windows is set to the ALT key. If you play to develop games under Linux using the Unity game engine, or another engine that makes heavy use of the ALT key, change this setting. What do you lose by changing this? The ability to move windows that are too big for your screen. If you’re screen resolution limited, using something like a 1366×768 display, you might want to keep/change the setting as holding ALT and click dragging a window will let you move it to where you can see any buttons at the bottom. 

![Window Manager Tweaks](/img/window_manager_tweaks.webp)<figcapture>Fig 8. Changing the ALT key behaviour</figcapture>

### But the terminal is a scary place...

It’s really not scary. Start by learning a few basic commands like ls, cd. Learning something new takes time. Painters don’t become a master the first time they pick up a paintbrush. Learning to ride a bike, or drive a car takes a bit of practice. But once you learn some of the shortcuts, using the terminal makes some tasks a whole lot easier than clicking around. My favourite task to do in a terminal is to update my Xubuntu and Linux Mint XFCE systems. To do this I hold ``CTRL + ALT + T`` to bring up a terminal, and in that terminal I type:

```shell
sudo apt update && sudo apt upgrade -y
```

When I’m typing this in the terminal I’m really typing sudo apt upd (+TAB) && sudo apt upg (+TAB) -y. Ignore the brackets and +, I’m hitting the TAB key in those spots to save myself 7 keystrokes (ate and rade). I could click on the Whisker menu and type upd, then click the Update Manager program, but the update manager program takes time as it needs to update the cache/list of available updates. There’s no delay like this on the command line as the first command, update, does that for us as the two commands are running. The && after the initial update allows us to run the second program after the first is done.

Life isn’t all perfect on the command line as this example falls down a bit in that thanks to Linux distributions branching out to use other methods of installing (like snap and flatpak), means extra steps if you want to update everything. (We’d have to add something like && flatpak update to the end of the command if we wanted to do more on a Linux Mint system). But the time savings is there, and in my experience learning shortcut keys really makes life a lot simpler.