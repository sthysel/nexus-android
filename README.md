# Installing Android 7 (Nougat) on Nexus 7 (2012)

In short you will need to:
- Install necessary android tools on Arch
- Gather the bootloader, android-nougat (7), and google play images.
- Setup Dev mode on device
- Install Team win's boatloader using the ```fastboot``` tool from the android tools repo. 
- Push new Android image file onto device using the ```adb``` tool, this is the Nougat Image
- Push BeansGapps image file device using the ```adb``` tool, this installs google play store.

## Install android tools
From [Android Arch Wiki](https://wiki.archlinux.org/index.php/android) install

```
 $ sudo pacman -S android-tools
 $ sudo pacman -S android-udev
```

## Gather the images

Get everthing together in a convenient directory.

### Bootloader

Gather [Team Win's reovery](https://twrp.me/devices/asusnexus72012wifi.html)
for Asus Nexus 7 2012 Wi-Fi (Grouper) which is the wifi model I have.

### Android nougat image 

Download the [aosp_grouper image](https://www.androidfilehost.com/?fid=889764386195914290). This
seems to be the recommended image at this time. 

### BeansGapps google apps


Download [beansgapps](https://www.androidfilehost.com/?fid=673368273298962437)


## Setup dev-mode on android device

- Click 7 times on build number in Config menu
- Enable USB debug mode

Plug device into Arch laptop, check the allow dialog on the Nexus 7.
Verify that thedevice can connect by:

```
$ adb devices
```


## Install Team Win recovery

Rename the downloaded image to twrp.img


Boot USB connected Nexus 7 to fastboot mode

```
$ adb reboot bootloader
```


Unlock the bootloader

```
$ fastboot oem unlock
```

Flash recovery

```
$ fastboot flash recovery twrp.img
```

Once the image has been copied, be ready to hold the down volume button 
and the start button on the Nexus 7 and boot into recovery.

```
$ fastboot reboot
```




## Push new image onto /sdcard/

```
$ adb push aosp_grouper-7.1.2-ota-eng-20170707.ds.zip /sdcard/
$ adb push BeansGapps-Mini-7.1.x-20170610.zip /sdcard/
```


## Install new image

* Boot into Recovery
* Factory Reset (only needed if you are not already on Android 7 AOSP)
* Install 7.x Grouper OTA-Package 
* Reboot into recovery
* Install Gapps for 7.1.x 
* Wipe dalvik/cache
* Reboot


