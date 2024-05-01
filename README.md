# redmi2pi
Mobian distro for klipper 3d printing firmware on redmi 2 wt88047.
Includes kiauh, klipper 3d printer firmware, moonraker api, mainsail webui and klipperscreen.
numpy is also preinstalled for resonance compensation analysis.
All credits goes to postmarketos.org mobian.org and debian.org which made this project possible.

Introduction
The image is 6.4GB and will fit an 8G variant just fine, however it is much better to use a class 10 sdcard with larger capacity for long term use since we are going to upload macros, gcodes and other stuff to the device, heck you can even turn it into a music player, download torrents or watch movies on the tiny screen while you print but that is beyond the scope of this document. (booooo!!!!). Wifi connectivity is working using klipperscreen, however, polkit authentication is disabled for NetworkManager at the moment. The phone orientation is landscape with the micro usb on the right side of the phone. This distro is safe but you are most welcome to check everything out.

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
