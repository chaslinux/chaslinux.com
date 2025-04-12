---
date: '2025-04-08T07:49:27-04:00'
draft: false
title: 'Using Logitech unifying devices with Linux'
cover:
    image: img/logitech_unifying_devices.webp
    alt: "Logitech keyboard, mouse, and dongle"
    caption: "Logitech K400r keyboard, M525 mouse, and unifying dongle"
tags: ["Linux","Xubuntu","Linux Mint","Hardware","Logitech","Unifying", "Keyboard", "Dongle","Mouse","Pairing"]
categories: ["Linux","Hardware"]
---

### Logitech unifying, but needs configuration

Logitech's **unifying** system is nice for a few reasons:

- Any device with the Logitech unifying symbol should work with a unifying dongle.
- Up to 6 devices can attach to one unifying dongle.
- There are plenty of Logitech devices that are part of the unifying ecosystem.

If you buy a new Logitech wireless keyboard direct from a retailer, chances are you can just plug the dongle into your computer, turn on your wireless keyboard, and work. But if you buy Logitech devices used, and/or they don't come with the unifying dongle, a little work might be needed to get the device paired with the dongle.

### Unifying device paired with another device

If you're device isn't automatically being recognized, you may need to pair your device to the unifying dongle using software. In Ubuntu, Linux Mint, and other Debian-derivatives the software to use is called *solaar* **note the double aa in the program name**.

To install solaar in Linux Mint or Xubuntu open a terminal (CTRL + ALT + T) and type:

```bash
sudo apt install solaar
```

Once solaar is installed, find the program in the menu, and run it. At first your unifying dongle may not be recognized. With solaar running, remove the unifying dongle and re-insert it. You should see the Unifying receiver dongle in the solaar window.

![Solaar with a device paired](/img/solaar_unifying_receiver_k750.webp)<figcaption>Fig 1. Solaar - Logitech k750 keyboard paired with unifying device</figcaption>

In the example below the unifying receiver already has a Logitech k750 keyboard paired with it. If you wanted to remove the k750 pairing you would click on the part that says 750, a button will appear in the bottom right of solaar letting you un-pair the device.

To pair a new device click on the Unifying Reciever part in solaar, and click the *Pair new device* button. Solaar with then scan for a device.

![Solaar - pairing a new device](/img/solaar_pair_new_device.webp)<figcaption>Fig 2. Solaar - pair a new device</figcaption>

At this point you may have to turn on and off your keyboard/mouse to allow solaar to detect it. Pairing happens automatically once it sees the device. If it cannot find the device, check the devices' batteries. You may have to restart after the keyboard/mouse is paired, but I found I didn't have to - it just started working once paired.

![Logitech K400 found by solaar](/img/solaar_k400_keyboard_paired.webp)<figcpation>Fig 3. Logitech K400r paired using Solaar</figcaption>

### Solaar displays battery levels

Running under Linux Mint XFCE solaar seems to display the keyboard's battery level (in percentage) in the panel/taskbar. This is a nice life hack that makes it easy to see when you need to change your batteries.
