---
date: '2024-05-05T16:09:17-04:00'
draft: false
title: 'Adding a laser printer as a shared network printer in Xubuntu Linux'
cover:
    image: img/hp_lj_1320_fp.webp
    alt: "HP LaserJet 1320 laser printer close up"
    caption: "HP LaserJet 1320 laser printer close up"
tags: ["Computer Refurbishing","Hardware","Printing","Networking","Linux","Xubuntu","HP","Laser Printer"]
categories: ["Hardware","Networking","Media"]
---

### Switching printers at home

Other than running out of toner, there was nothing wrong with the HP Laserjet P1102w printer we have at home. The printer printed cleanly, was compact, and was connected to our wireless network, so any machine on our network could print to it. In fact, I was planning on buying more toner this evening after we did our usual scouring of thrift shops. I thought there was a small chance I might find the right HP 85A toner at one of the stores we planned to go to. I did find some other toner at one of the thrift shops, and the $5.95 price tag wasn’t bad, but it was for a different model in the same line of printers. But this was actually after spotting an even better deal, an HP Laserjet 1320 duplex printer for a whopping $10.95.

I’m familiar with the HP Laserjet 1320 as this is the printer we use at several places at work. I’m normally not a fan of HP printers, despite the fact our previous printer was also an HP Laserjet. HP printers tend to be a pain to configure in Linux, and they do nasty things with toner on newer models. But, being very familiar with this printer, I knew it would be a great printer if it worked.

### Testing the HP Laserjet 1320

The printer was pretty dirty on top. I opened the top part to check for toner, it was there. I wasn’t about to buy the printer without checking for issues like streaking, or empty toner. The power cable looked like it had been through a rain storm, but the printer had both it and a USB cabled plugged into the back of it. I turned off the power switch on the right-hand side, plugged the printer into the test station at the thrift shop, then powered the printer on. After the printer ran through it’s brief startup routine I held the green button on the top to start a test print. To my surprise/delight, a crisp looking test page printed, without any toner spots or issue.

### Perks / issues

The big draw of the HP Laserjet 1320, at least for me, is it’s ability to do duplex (double-sided) printing. The printer is automatically recognized by Xubuntu, and print quality is decent. While the printer tray normally holds around 120 sheets, there’s an optional tray available to hold up to 250 sheets (HP P2015 sheet feeder with tray). The extra tray ads about 3 inches to the printer height, but if you print a lot, it might be a good idea. In our family use case, 120 pages is more than enough.

![HP Laserjet 1320](/img/hp_lj_1320-scaled.webp)<figcaption>Fig 1. HP LaserJet 1320 laser printer</figcaption>

While new HP-branded (HP 49A) toner for this printer is expensive: $176.99 CA, it’s capable of a yield of 2,500 pages. Lots of off-branded toners exist at reasonable prices ($29 – $50) on Amazon.

### First steps

The first step is to make sure the printer is available locally on the machine it’s connected to. In Xubuntu you can click the whisker menu in the top left (or just press the Windows key on the keyboard to open the menu) and type printers into the menu. You should see a program you can click to open up a list of locally connected printers.

### Sharing the printer

Sharing a printer that’s connected and working on a Xubuntu Linux system is a whole lot easier than you might expect. 

In the web browser on the computer the printer is connected to type: (http://localhost:631)

Next, click the *Administration* tab at the top of the OpenPrinting CUPS web site that opens. At this point you will be prompted to enter a username and password, this is the same as the user account you’ve set up.

Once on the Administration page it’s simply a matter of clicking the *Advanced > Share Printers* connected to this system and clicking the *Change Settings* button below.

![OpenPrinting CUPS web administration](/img/localhost631.webp)<figcaption>Fig 2. OpenPrinting CUPS administration screen</figcaption>

That’s it! Provided the printer is already working connected to your networked Xubuntu desktop, it will now be available to other computers on your network, including systems running Windows.
