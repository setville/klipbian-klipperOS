# klipbian-klipperOS

![redmi2pi-klipperOS_small](https://github.com/setville/redmi2pi-klipperOS/assets/168615479/5c24a2ae-8f96-4369-ad7d-7c4667ee7b0e)

Debian distro for klipper 3d printing firmware on redmi 2 wt88047.
Includes kiauh, klipper 3d printer firmware, moonraker api, mainsail webui and klipperscreen.
All credits goes to postmarketos.org mobian.org and debian.org kiauh klipper moonraker mainsail klipperscreen devs and the entire 3d printing community which made this project possible.

The image is based on debian Trixie/Sid and is 6.4GB. It will fit an 8G variant just fine, however it is much better to use a class 10 sdcard with larger capacity for long term use since we are going to upload macros, gcodes and other stuff to the device, heck you can even turn it into a music player, download torrents or watch movies on the tiny screen while you print but that is beyond the scope of this document. (booooo!!!!). Wifi connectivity is working using klipperscreen, however, polkit authentication is disabled for NetworkManager at the moment. The phone orientation is landscape with the micro usb on the right side of the phone. This distro is safe but you are most welcome to check everything out.

## Sources
- Kernel Source: https://github.com/msm8916-mainline/linux
- lk2nd Source: https://github.com/msm8916-mainline/lk2nd
- rootfs source: Official Debian Trixie/Sid Repo

>DISCLAIMER
- I am not responsible for bricked phones, battery explosions, burnt houses, 3d printer nozzle dives, broken heatbreaks, burned tmc drivers, spaghetti prints or thermonuclear war... Please do some research if you have any concerns about doing this to your device. YOU are choosing to make these modifications, and if you point the finger at me for messing up your device, I will laugh at you. (common phone flashing mod disclaimer twisted a bit to fit 3d printing stuff) 

Requirements:
1. redmi 2 phone with UNLOCKED BOOTLOADER and TWRP INSTALLED.
2. ADB and fastboot installed download zip from https://dl.google.com/android/repository/platform-tools-latest-windows.zip
3. Micro usb data cable.
4. files downloaded from this repo (lk2nd.img, boot.img and rootfs.img)

Prep work:
1. https://wiki.postmarketos.org/wiki/Xiaomi_Redmi_2_(xiaomi-wt88047)#Installation
2. https://wiki.postmarketos.org/wiki/Xiaomi_Redmi_2_(xiaomi-wt88047)#How_to_enter_flash_mode
3. https://wiki.lineageos.org/adb_fastboot_guide#On_Windows

>WARNING!!! Be sure to have a backup of your phone's firmware and a full nandroid backup with twrp so you wont have to reflash lineageos everytime things don't work.
- After downloading the zip file, unpack it and open a command prompt or powershell terminal in the folder. make sure you have the path of platform tools included in yout Environment variables.(refer to Prep work #3)

Flashing procedure (built in emmc)
1. Put phone in fastboot mode and flash lk2nd.img using the commands "fastboot erase boot" followed by "fastboot flash boot lk2nd.img" without quotes.
2. reboot phone in lk2nd fastboot mode (refer to prep work #2) or issue a "fastboot reboot"
3. flash the rootfs.img using the command "fastboot flash userdata rootfs.img" without quotes.
4. flash boot.img using the command "fastboot flash boot boot.img" without quotes.

Flashing procedure (built in sd card)
1. flash rootfs.img to sd card using balena etcher in windows or dd in linux.
2. Put phone in fastboot mode and flash lk2nd.img using the commands "fastboot erase boot" followed by "fastboot flash boot lk2nd.img" without quotes.
3. reboot phone in lk2nd fastboot mode (refer to prep work #2) or issue a "fastboot reboot"
4. flash boot.img using the command "fastboot flash boot boot.img" without quotes.
5. Turn the phone off and plug in sdcard
6. Turn on the phone

First boot
1. Resize the partition using resize2fs (built in emmc)
   - sudo resize2fs /dev/mmcblk0p30
   - enter password 1234

2 Resize the partition using resize2fs (sdcard)
   - sudo resize2fs /dev/mmcblk1
   - enter password 1234

3. Reboot
   - sudo reboot
   - enter password 1234
   
5. You can also change the default password which is 123456 for both root account and mobian account
   - sudo passwd mobian
   - type password 1234
   - type your own password on the fields provided. mind the prompt
   - sudo passwd root
   - type password 1234
   - type your own password on the fields provided. mind the prompt
   
At this point the klipperscreen ui should show up, from there you can connect to your wifi and access the phone via ssh and enjoy your self built sonic pad for less than a quarter of the price. 

USB
- We only have one usb port to play with so be gentle with it. a usb hub is essential if you want to use extra usb ports for a pico adxl for instance or even a multiboard setup. 

BATTERY/POWER SUPPLY

>WARNING!!! UNPACKING MOBILE PHONE BATTERIES IS DANGEROUS, A SMALL PUNCTURE WOULD CAUSE THE BATTERY TO EXPLODE/COMBUST VIOLENTLY, IF YOU ARE UNSURE OF WHAT YOU ARE DOING, DO NOT UNPACK THESE BATTERIES WILLY NILLY LEST YOU BURN YOUR HOUSE DOWN!

- The default battery is fine for supplying power for short term prints but it's advisable to remove the battery pouch and solder a buck converter to the battery bms, set the buck output to 4 volts and power it directly from the printer psu. i did a rough estimate of power consumption and current draw rarely reaches 400mA so an LM2596 module should do just fine. in my case i used a mini360 clone and tapped it to my other buck with 12V output, not advisable but it works for me.

![BatteryMod_small](https://github.com/setville/redmi2pi-klipperOS/assets/168615479/9244633e-c4f7-492a-9eb8-3f63d427bbda)

