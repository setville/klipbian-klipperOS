# redmi2pi-klipperOS
Mobian distro for klipper 3d printing firmware on redmi 2 wt88047.
Includes kiauh, klipper 3d printer firmware, moonraker api, mainsail webui and klipperscreen.
numpy is also preinstalled for resonance compensation analysis.
All credits goes to postmarketos.org mobian.org and debian.org which made this project possible.

The image is based on debian bookworm and is 6.4GB. It will fit an 8G variant just fine, however it is much better to use a class 10 sdcard with larger capacity for long term use since we are going to upload macros, gcodes and other stuff to the device, heck you can even turn it into a music player, download torrents or watch movies on the tiny screen while you print but that is beyond the scope of this document. (booooo!!!!). Wifi connectivity is working using klipperscreen, however, polkit authentication is disabled for NetworkManager at the moment. The phone orientation is landscape with the micro usb on the right side of the phone. This distro is safe but you are most welcome to check everything out.

Requirements:
1. redmi 2 phone with UNLOCKED BOOTLOADER and TWRP INSTALLED.
2. ADB and fastboot installed download zip from https://dl.google.com/android/repository/platform-tools-latest-windows.zip
3. Micro usb data cable.
4. files downloaded from this repo (lk2nd.img, boot.img and rootfs.img)

Prep work:
1. https://wiki.postmarketos.org/wiki/Xiaomi_Redmi_2_(xiaomi-wt88047)#Installation
2. https://wiki.postmarketos.org/wiki/Xiaomi_Redmi_2_(xiaomi-wt88047)#How_to_enter_flash_mode
3. https://wiki.lineageos.org/adb_fastboot_guide#On_Windows

Flashing procedure (built in emmc)
1. Put phone in fastboot mode and flash lk2nd.img using the command "fastboot flash boot lk2nd.img" without quotes.
2. reboot phone in lk2nd fastboot mode (refer to prep work #2)
3. flash the rootfs.img using the command "fastboot flash userdata rootfs.img" without quotes.
4. flash boot.img using the command "fastboot flash boot boot.img" without quotes.

Flashing procedure (built in sd card)
1. flash rootfs.img to sd card using balena etcher in windows or dd in linux.
2. Put phone in fastboot mode and flash lk2nd.img using the command "fastboot flash boot lk2nd.img" without quotes.
3. reboot phone in lk2nd fastboot mode (refer to prep work #2)
4. flash boot.img using the command "fastboot flash boot boot.img" without quotes.
5. Turn off phone and plug in sdcard
6. Turn on the phone.

First boot
1. Resize the partition using resize2fs (built in emmc)\n
   1.1 sudo resize2fs /dev/mmcblk0p30\n
   1.2 enter password 123456\n
2 Resize the partition using resize2fs (sdcard)\n
   2.1 sudo resize2fs /dev/mmcblk1p1\n
   2.2 enter password 123456\n
3. Reboot\n
   3.1 sudo reboot\n
   3.2 enter password 123456\n
   
5. You can also change the default password which is 123456 for both root account and mobian account
   5.1 sudo passwd mobian
   5.2 type password 123456
   5.3 type your own password on the fields provided. mind the prompt
   5.4 sudo passwd root
   5.5 type password 123456
   5.6 type your own password on the fields provided. mind the prompt
   
At this point the klipperscreen ui should show up, from there you can connect to your wifi and access the phone via ssh and enjoy your self built sonic pad for less than a quarter of the price. We only have one usb port to play with so be gentle with it. a usb hub is essential if you want to use extra usb ports for a pico adxl for instance or even a multiboard setup. The default battery is fine for supplying power for short term prints but it's advisable to remove the battery pouch and solder a buck converter to the battery bms, set the buck output to 4 volts and power it directly from the printer psu. i did a rough estimate of power consumption and power draw rarely reaches 400mA so a LM2596 module should do just fine. in my case i used a mini360 clone and tapped it to my other buck with 12V output, not advisable but it works for me.
