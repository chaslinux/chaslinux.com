---
date: '2023-07-26T11:57:28-04:00'
draft: false
title: 'First experience trying to learn Unity on Xubuntu Linux'
tags: ["Game Development", "Gamedev","Unity","Xubuntu","Linux","Programming"]
categories: ["Game Development","Linux","Programming"]
---

> After this experience, and some back and forth with GameMaker, the GameMaker team switched the licensing back to a one time fee (except for console exports),
> and they released a beta version of the engine for Ubuntu-based systems. The team continues to update this beta along with the normal code. Since I previously
> had experience with GameMaker I've decided to stick with it. I've been really thrilled with it as bugs I've run into have been fixed a short while after
> I've reported them, and the community have been great helping me solve issues.


### The king of game engines

Unity is considered the big kahuna of game engines. It is often cited as the best engine to learn if your end goal is to work in the game industry. Unity is cross-platform, meaning it can run on different operating systems. It can also compile programs for more than a dozen other platforms the engine itself doesn’t run on.

I have very little experience with the Unity game engine. I bought a few online tutorials, and a book about a year ago, but when I started reading I found most of the documentation was extremely user-interface heavy, and didn’t get into coding. Four chapters into the book I’d bought and I’d yet to write a single line of code. It was a frustrating experience compared to GameMaker, where I was writing code within the first 10 minutes of watching a video. But because Unity is used so much for mobile development I thought I’d give it another shot.

### Initial problems / conflicts with Xubuntu key-mapping

When I first tried the Unity game engine I discovered both Xubuntu Linux and Unity bump heads over the use of the ALT key. Normally, most key bindings can be reassigned in the “keyboards” program in Xubuntu, but in this case the ALT key keybinding was assigned in the “window manager tweaks” program.

1. Open the Window Manager Tweaks program
2. Click the Accessibility tab
3. Change the “Key used to grab and move windows:” from the ALT key to one of the other options, or set it to None.

If you leave this key assigned to ALT, when you start to use Unity’s built-in editor to adjust 3D objects you’re going to run into issues trying to adjust those objects – Unity needs the ALT key (as do other engines).

You can’t just install Unity hub

Installing Unity is not difficult, but the default experience will not be the same as what you see in tutorials. If you have a bit of command-line experience in Linux, or can just copy and paste, you won’t have much trouble getting the Unity hub installed. Follow the instructions here:

(https://docs.unity3d.com/hub/manual/InstallHub.html#install-hub-linux)

Once Unity hub is installed you have to agree to their license, set up an account, and install the Unity editor. Note: the Unity editor is not the same as Visual Studio Code. The Unity editor is the main interface you’ll see working with Unity. It consists of 4 main windows: Hierarchy, the Scene/Game window, the inspector and the project/console window.

Visual Studio Code comes into the scene when you create a script within Unity… but Visual Studio Code doesn’t get automatically installed in Unity hub. By default, I found Unity opened Mousepad, the default text editor in Xubuntu, when I first tried creating a script. Mousepad knows about C#, but doesn’t offer the level of support for C# that VS Code does. I installed VS Code by downloading and double-clicking on the .deb package here:

(https://code.visualstudio.com/download)

I then installed the required .NET SDK by following the steps here:

(https://learn.microsoft.com/en-ca/dotnet/core/install/linux-ubuntu-2204)

Yousuf Azad Sami has a nice brief article on connecting all these parts. Once VS Code is installed, Unity still needs to know about VS Code. Check our Yousuf’s article here:

(https://medium.com/@sami.yousuf.azad/set-up-visual-studio-code-for-unity-in-linux-69b7f4352e0b)

But even with VS Code installed I found the experience didn’t quite match what I was seeing as I was following a tutorial. VS Code let me do some command-completion, but generally didn’t offer as many suggestions (drop downs) as I was seeing in the tutorial. These seemed to be Unity-specific. There may be an add-on VS Code needs to know about on Linux that it knows when installed on Windows.

For experience developers this missing feature (drop down suggestions) might be annoying, but for someone like me, someone new to learning Unity, it feels like a really important feature. I opened VS Code and clicked on the Extensions, then searched for unity. There was a Unity debugger extension that looked official, but it’s been depreciated. The closest thing I could find to the feature was the Unity Code Snippets add on by Kleber Silva, but it didn’t appear to be an official Unity plug-in – so use at your own risk.

### Slowness

I have to mention the Godot game engine here because installing and using Godot is 1000x faster than using Unity. I installed Unity on a couple of Xubuntu machines: 

An ASUS desktop featuring a Core i7-4770 @ 3.9GHz (4 cores, 8 threads) CPU with 16GB DDR3 RAM.
A custom workstaion with a XEON XEON E5-2690v2 (10 core, 20 threads) CPU, with 64GB of DDR3 RAM and an NVMe drive.

Unity felt sluggish when I tried compiling my program on my XEON workstation. I cannot imagine trying to develop a game on a machine that’s less powerful than either of these machines. To be fair, there is a wait when you click “play” on Gamemaker, but it’s a lot more clear on Gamemaker that the engine is busy. On Unity I couldn’t tell whether it ran into an issue with the code, or whether it was just delayed running the game. A few times I clicked play to run the game, nothing seemed to happen for a bit. I clicked play again, and then the game ran, or spat out an error message. The delay was just too much. At least with Gamemaker I could see an error in the inspector window. And Godot, well, that engine just runs like the wind.

### The results

First, I want to give a shout out to Game Maker’s Toolkit for their excellent Unity Tutorial for Complete Beginners, this was one of the first Unity videos I’ve watched where I felt like I was really learning the engine. Although it’s been a very long time since I’ve been in school, watching this video felt like I was connecting with the teaching style of the teacher. You can see the GMT video here:

(https://www.youtube.com/watch?v=XtQMytORBmM&t=1502s)

I spent quite a bit of time creating my own sprites for the game in Aseprite. Aseprite is a sprite creation program available for Linux through Steam. There was an old version floating around the Internet that was (legally) free, but Aseprite was inexpensive enough that I just bought it outright. The tutorial is only 45 minutes long, but I only managed to get roughly 25 minutes into the video last night.

My version of the game doesn’t look anywhere as smooth as the tutorial, and my bird rotates when it collides with the stalactites/stalagmites in my game. My C# code isn’t any different than the Tutorial, but my stalactites have multiple hit boxes, which might be part of the issue. 

I plan on working completely through the tutorial in this evening, but I’m not sure I’ll continue with Unity as I really don’t like the huge delay when running the game within Unity.

Gamemaker has a Linux version of the engine, but it comes with the warning that it may corrupt your projects. I like a lot of things about Gamemaker, but I suspect that in the end I’m going to end up spending much more time in the future learning Godot, as the performance and stability on Linux is top notch. Other than the aforementioned issue with the ALT key and Xubuntu, Godot works pretty flawlessly in Xubuntu, and it takes seconds to install. That said, I don’t have a lot of experience with Godot, but the brief experience I have makes me think this is the engine to stick with on Linux.

