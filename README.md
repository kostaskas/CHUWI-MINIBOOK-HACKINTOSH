# CHUWI Minibook Hackintosh

EFI files for hackintosh on the CHUWI Minibook, works on Catalina and Mojave with initial support for Big Sur.
If you see anything that could be added or changed don't hesitate to make a pull request.

![Catalina with working Graphics Acceleration](/images/Catalina.jpeg)

## *CRITICAL ISSUE WARNING*
## The Fan does not work on its own and requires a special patch. Please use EFI release version 0.1.0 or higher to enable automatic Fan operation. 

##  Basic Usage

1. Create a bootable Mojave or Catalina bootable USB using this [tutorial](https://internet-install.gitbook.io/macos-internet-install/) OR this [tutorial](https://www.olarila.com/topic/6278-new-vanilla-olarila-images/)(arguably easier but must register) but use my CLOVER folder at the point where you should configure CLOVER bootloader
2. Boot from this usb then install Mojave/Catalina on a free partition of your drive ( please note...must be installed to ssd as macos does not detect emmc )
3. During first boot, after installing the OS, mount your EFI partition and place the CLOVER folder alongside other OSes bootloader
4. Reboot and change BIOS bootloader order to have clover bootloader as first entry
5. Open your config.plist and generate a new serial number [Tutorial here](https://hackintosher.com/forums/thread/generate-your-own-hackintosh-serial-number-board-serial-number-uuid-mlb-rom-in-clover.306/)
6. Install additionals drivers
7. Reboot and enjoy !


## Changing the display orientation

To correct the screen orientation within macOS download the [Display Rotation Menu](https://www.magesw.com/displayrotation/) app and set the view to portrait flipped OR press and hold down cmd+opt (Windows+alt) and open System Preferences...keep holding down those two buttons and click on Displays then the rotation option will appear so set it to 270 degrees for the fixed layout


## Enabling HiDPI mode

to enable HiDPI mode ( adds 960 x 600 ) enter the following command in terminal post-installation then reboot:

sudo defaults write /Library/Preferences/com.apple.windowserver.plist DisplayResolutionEnabled -bool true


## Setting resolutions over 1080p
- Method 1
1. flash modified bios *warning-possibility of windows serial key being deleted so proceed with caution* (format usb stick to fat 32, copy files inside of folder to root of drive then reboot)
2. enter bios using f7(fn + 7) then go to chipset -> system agent -> graphics configuration -> dvmt pre-allocated and change to 64mb
3. either delete config.plist and rename config4k.plist to config.plist OR select config4k at clover boot screen under options

- Method 2
1. load clover and select "start uefi shell 64" 
2. enter the command "setup_var_3 0x894 0x2" (without the quotations) hit enter then type exit
3. either delete config.plist and rename config4k.plist to config.plist OR select config4k at clover boot screen under options

### Additional drivers

[Wifi dongle driver](https://github.com/chris1111/Wireless-USB-Adapter-Clover)

[Wifi dongle driver(older adapters)](https://github.com/chris1111/Wireless-Ralink-Panel-Utility)

[Latest AutoBuild of Intel WiFi Driver & HeliPort App](https://github.com/1hbb/OpenIntelWireless-Factory/releases)

[Latest AutoBuild of OpenCore (You will need to merge our release into one provided at this link if you want to use this. Will not boot otherwise)](https://github.com/williambj1/OpenCore-Factory/releases)



## What works

- Graphic Acceleration
- Bluetooth (Improved Reliability)
- Brightness
- Audio (Fixed audio after sleep)
- Power Management
- Battery 
- USB
- Keyboard
- Camera
- Sleep / Wake ( lid, timed & manual sleep seem to function fine but button appears to be problematic even though power awake works)
- FAN now operates automatically on Cold/Warm boot and after sleep.
- TrackPoint 
- HDMI / Type-C
- Windows boot from OpenCore
- TouchScreen / Stylus (double click doesnt work and non-functional on mojave)
- Internal Wi-Fi (use the heliport app to join networks just like the built in wireless and check "load at login" to autostart it if u would like...if u want to connect to your home internet automatically then u will need to edit the info.plist of the itlwm.kext with your ssid and password)
- FileVault Supported

## Planned/In Progress Fixes

- Accelerometer (likely will not have full support but may allow for a triggered rotate when keyboard flipped)
- Auto shut off of Keyboard when flipped into tablet mode
- Additional resolutions on internal monitor (may not be possible, so don't get your hopes up yet)
- Native Brightness Key Activation
- Native Sleep Button support

## What doesn't work

- Fingerprint Sensor
- Card Reader
- Emmc
- Accelerometer
- Additional Resolutions other than default

## Other Operating Systems

OS ( Version ) ( Issues )
- [Android](https://www.android-x86.org/)    ( Android-x86 9.0-rc1 )                   ( cast screen, auto rotate broken )
- [Chrome - Brunch Method & Tools](https://github.com/sebanc/brunch) ( v80+ ) ( none & preferred method. Dual boot works best when installed to alternate drive such as EMMC or SD card, Installation on same SSD is challenging and requires chromeOS to be installed first before Windows or macOS )
- [Chrome - Chromify Method & Tools](https://github.com/imperador/chromefy) ( v80+ ) ( none & works well with dual boot and installed on same SSD )
- [Linux](https://manjaro.org/)                   ( Manjaro-cinnamon-18.0.4-stable-x86_64 ) ( none )
- [Ubuntu](https://ubuntu.com/)                  ( 20.04 LTS )                             ( none )

## Using Other Operating Systems with OpenCore
Windows: Should be installed and booted from the OpenCore menu. OpenCore will automatically show Windows in the menu with no additional effort. 

Linux: Ubuntu is the only flavor tested. Requires special steps for OpenCore to show Linux in the boot menu:
  1. Install macOS & optionally Windows first before attempting to install Linux, period, full stop. (This is important)
  2. Shrink drive and create a new partition for your Ubuntu install. If using macOS to partition you must choose partition and DO-NOT add a volume to your APFS partion. (Won't work if you don't do this right)
  3. Create Ubuntu boot disk
  4. Insert Installer into USB port and restart computer. Enter UEFI and select OpenCore from the boot menu.
  5. You will see the Ubuntu installer USB show in the boot menu. Select the Ubuntu installer to begin installation.
  6. Follow all installation prompts and when asked if you want to install Ubuntu alongside Windows or completely erase the drive; instead select "something else"
  7. Change Nothing else except the following: Select the partition you want to use for Linux and then click "change", format as Ext4 and set mount point as "/".
  8. Confirm and then continue with the install as normal.
  9. Reboot once install has completed and Ubuntu should show in the OpenCore boot menu.
  * If you restore a partition after installing Ubuntu you may loose the ability to boot Ubuntu from the OpenCore menu which may result in needing to reinstall Ubuntu

chromeOS: I recommend installing to a Ultra High Speed SD card especially if using the "Brunch" method of installation. Once installed to the SD card it will show up in the OpenCore boot menu.

## Credits
Special thanks to my Minibook bro [@Balopez](https://github.com/balopez83/One-Mix-3-Hackintosh) for all of his assistance and [@Lazd](https://github.com/lazd/VoodooI2CGoodix) for the touchscreen driver <br>
[All users from the GPD Discord]() especially [@azkali](https://github.com/Azkali/GPD-P2-MAX-Hackintosh) <br>
[Fewt's Hackintosh guide](https://fewt.gitbook.io/laptopguide/) <br>
[CHUWI for making the great Minibook](https://www.chuwi.com/cn/) <br>
