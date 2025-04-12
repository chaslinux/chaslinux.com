---
date: '2024-05-30T15:52:51-04:00'
draft: false
title: 'Reboot to the BIOS from Linux'
cover:
    image: img/BIOS.webp
    alt: "The BIOS from an 8th generation ThinkPad"
    caption: "8th generation (2018) ThinkPad BIOS"
---

### On systemd-based distributions it’s possible to boot to the BIOS from Linux

Have you ever found yourself working on a computer that’s just so blindingly fast that you just cannot mash the key you need to get into the BIOS fast enough? It might be possible to reboot from your Linux system into the BIOS of your computer.

Not all systems support this feature. On the one system we tested this on which didn’t boot to the BIOS the error message mentioned something about the EFI partition. But I was able to successfully run the command on a couple of systems, a 4th gen and 8th gen system.

The command to run is:

```shell
sudo systemctl reboot --firmware-setup
```

![Booting to the BIOS via command line on Linux Mint 22.1](/img/firmware_setup.webp)<figcaption>Fig. 1 - Booting to the BIOS via command line on Linux Mint 22.1</figcaption>

Be sure to properly close any open documents before running this command as it will reboot the computer and then force the “firmware”/BIOS to start up.
