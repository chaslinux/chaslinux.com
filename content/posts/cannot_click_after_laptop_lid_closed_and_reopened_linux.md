---
date: '2024-05-28T12:14:43-04:00'
draft: false
title: 'Cannot click after laptop lid closed and re-opened - Xubuntu Linux'
cover:
    image: img/xubuntu.webp
    alt: "A modified version of Xubuntu"
    caption: "Xubuntu Linux + plank"
tags: ["Hardware","Linux","Computer Refurbishing","Xubuntu"]
categories: ["Linux","Hardware"]
---

### The problem is power management (workaround)

You’ve installed Xubuntu 22.04 on your laptop and things are going smoothly… Then you close the lid on your laptop and discover when you open it back up again that when you move the mouse it moves, but you cannot right or left click for some reason? The issue appears to be with power management.

The work around we found that appears to fix this is to edit the file:

```shell
sudo vi /etc/UPower/UPower.conf
```

In this file there’s a line that says:

```shell
IgnoreLid=false
```

Change this to:

```shell
IgnoreLid=true
```

Make sure you spell true with a small “t,” if you use a capital for True, it won’t be recognized. Try restarting and now you should be able to open and close the lid without the mouse locking the left and right click.
