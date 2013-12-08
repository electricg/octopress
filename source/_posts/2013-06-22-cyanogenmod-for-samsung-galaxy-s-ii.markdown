---
layout: post
title: "CyanogenMod for Samsung Galaxy S II"
date: 2013-06-22 15:15:00 +0000
comments: true
categories:	
---
This guide is for installing CyanogenMod 10.1 on Samsung Galaxy S II using Mac OS X (10.8.4 at the time of writing).


## Get the files

* [CyanogenMod 10.1](http://wiki.cyanogenmod.org/w/I9100_Info) I use the **Nightly** version.
* [ClockworkMod Recovery](http://cmw.cmfs.me/c1/recovery/GT-I9100_JB_ClockworkMod-Recovery_6.0.2.9.tar) This is the link to the latest version, but I used the [5.5.0.4 version](http://cmw.cmfs.me/c1/recovery/recovery-clockwork-5.5.0.4-galaxys2.tar).
* [Google Apps](http://goo.im/gapps) I used the [20121212 version](http://goo.im/gapps/gapps-jb-20121212-signed.zip).
* [Heimdall Suite](http://cmw.cmfs.me/common/heimdall_v1.4rc1_mac.zip) for Mac OS X. This is the link to the latest version, but I used the [1.3.2 version](https://github.com/downloads/Benjamin-Dobell/Heimdall/heimdall-suite-1.3.2-mac.dmg).
* [Official stock firmware](http://samsung-updates.com/device/?id=GT-I9100) As I live in the UK, I went for the [CPW version](http://samsung-updates.com/region/?region=CPW) and at the time of writing I used [this version](http://hotfile.com/dl/225705527/e74f79b/CPW-I9100XWLSW-20130529181159.zip.html).


## Installation

1. Fully charge the device.
* Place the CyanogenMod rom and the Google Apps .zip files on the root of the SD card and on the root of the phone storage.
* Install Heimdall Suite as a normal application and follow the instructions.
* Extract the *zImage* file from the ClockworkMod zip.
* Open a terminal on the computer and navigate to the directory containing *zImage* (do not close the terminal for the moment).
* Power off the Galaxy S II and connect the USB adapter to the computer but not to the Galaxy S II.
* Now boot the Galaxy S II into download mode by holding down **Volume Down**, **Home** & **Power**. Accept the disclaimer. After this insert the USB cable into the device.
* From the previously open computer terminal run the following command:

  	sudo heimdall flash --kernel zImage --no-reboot

* A blue transfer bar will appear on the device showing the recovery being transferred.
* Manually reboot the phone into ClockworkMod Recovery mode by holding **Volume Up**, **Home**, & **Power**.
* Use the physical volume buttons to move up and down and the power button to confirm your selection. 
* Select **backup and restore** to create a backup of the current installation on the device.
* Select the option to **wipe data/factory reset**.
* Select **install zip from sdcard**.
* Select **choose zip from sdcard**.
* Select the CyanogenMod file you placed on the sdcard. You will then need to then confirm that you do wish to flash this file.
* If for some reason it's not possible to install from the sdcard, select the **choose zip from internal sdcard** option to select the files from the internal memory.
* Repeat the **install**, **choose** and **select** procedure for the Google Apps file.
* Return back to the main menu, and select the **reboot system now** option.
* The device should now boot into CyanogenMod.


## Go back to the Stock Official Firmware

1. Unzip the Official Stock Firmware
* Open a terminal on the computer and navigate to the directory containing the extracted files (do not close the terminal for the moment).
* Power off the Galaxy S II and connect the USB adapter to the computer but not to the Galaxy S II.
* Now boot the Galaxy S II into download mode by holding down **Volume Down**, **Home** & **Power**. Accept the disclaimer. After this insert the USB cable into the device.
* From the previously open computer terminal run the following command:

		sudo heimdall flash --factoryfs factoryfs.img --cache cache.img --hidden hidden.img --modem modem.bin --kernel zImage --param param.lfs --primary-boot boot.bin --secondary-boot Sbl.bin

* A blue transfer bar will appear on the device showing the recovery being transferred.
* Reboot the phone.


## Sources
* [CyanogenMod Wiki](http://wiki.cyanogenmod.org/w/I9100_Info)
* [everydaylht.com](http://everydaylht.com/howtos/android/heimdall/) "Use Heimdall to Install Kernels, Recoveries, ROMs on your Samsung Android Device"