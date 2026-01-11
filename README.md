# postmarketOS-spacewar

postmarketOS for Nothing Phone (1) – spacewar

**postmarketOS-spacewar** provides scripts and images to install **postmarketOS** on the **Nothing Phone (1)**. This project is intended for people who are comfortable with unlocking bootloaders and flashing Android devices only.

This currently ships With the **Phosh Desktop Environment only**.

---

## Requirements

- Nothing Phone (1)
- USB cable (high quality USB-A → USB-C or USB-C → USB-C)
- Linux PC (This is Also Fine to do On Windows or Macos but Linux is Most Recomended)
- git installed

---

## Installation

### 1. Clone the repository

From your home directory:

```sh
cd ~
git clone --depth 1 https://github.com/howtoedittv/postmarketOS-spacewar
cd postmarketOS-spacewar
```

### 2. Get adb and fastboot

> Skip this section if you already have adb and fastboot installed 

Run the provided script:

```sh
chmod +x get-sdk
./get-sdk
```

---

## Unlocking The Bootloader 

> Skip this section if your bootloader is already unlocked.

**note: If you Have a google acount tied to your phone make sure to reset from the phone itself first to avoid being FRP locked later**

1. On your phone, open **Settings**
2. Go to **About phone**
3. Tap **Build number** repeatedly until it says you are a developer
4. Go back to **Settings**
5. Open **Developer options**
6. Enable:
   - **OEM unlocking**
   - **USB debugging**
7. Connect your phone to the PC via USB
8. When prompted to trust the PC, press **Allow**

On your PC, run:

```sh
adb reboot bootloader
fastboot flashing unlock
```

**WARNING:** This will factory reset your phone and destroy all data.

After unlocking, complete the Android setup again and re-enable **Developer options** and **USB debugging**.

---

## Flashing Instructions
**note: If you Have a google acount tied to your phone make sure to reset from the phone itself first to avoid being FRP locked later**

1. Plug your Nothing Phone (1) into your PC
2. Initialize ADB and confirm the device is detected:

```sh
adb devices
```

3. Reboot to bootloader:

```sh
adb reboot bootloader
```

4. Check fastboot detection:

```sh
fastboot devices
```

5. Erase required partitions:

```sh
fastboot erase boot
fastboot erase vendor_boot
fastboot erase dtbo
```

6. Run Your Chosen Image download script Corresponding To Your Preferred Desktop Environment:
```sh
chmod +x get-<your desired dektop environment>
./get-<your desired dektop environment>
```

7. Flash postmarketOS images:
```sh
fastboot flash boot boot.img
fastboot flash userdata userdata.img
```

8. Reboot:

```sh
fastboot reboot
```

You should now boot into **postmarketOS** on your Nothing Phone (1).

---

## Restore Instructions

> This restore process is **only for LineageOS** at the moment.

1. from your current directoy. run:

```sh
cd ~/postmarketOS-spacewar
chmod +x restore
./restore
```

2. After it finishes, a new directory called `lin` will appear cd into it:

```sh
cd lin
```

3. Power off your phone
4. Power it back on while holding **Power + Volume Up**
5. When the Nothing logo appears:
   - Release **Power**
   - Keep holding **Volume Down** until you enter the bootloader

6. On your PC, verify fastboot:

```sh
fastboot devices
```

7. Erase partitions:

```sh
fastboot erase vendor_boot
fastboot erase boot
fastboot erase userdata
```

8. Flash LineageOS images:

```sh
fastboot flash boot boot.img
fastboot flash vendor_boot vendor_boot.img
fastboot flash dtbo dtbo.img
```

9. Reboot into recovery:

```sh
fastboot reboot recovery
```

10. In Lineage recovery:
    - Select **Factory reset**
    - Select **Format data / factory reset**
    - Select **Format data**

11. Go back To the Main menu using volume keys and power button
12. Select **Advanced**
13. Select **Enable ADB**
14. Go back to the first menu
15. Select **Apply update**
16. Select **Apply from ADB**

17. On your PC, sideload LineageOS:

```sh
adb devices
adb -d sideload lineage-23.0-20260107-nightly-Spacewar-signed.zip
```

18. When asked If You Want to reboot back to recovery, select **yes**
19. When back in the recovery go to enable adb once more
20. Go back to the main menu
21. Go to Apply update/Apply from adb
22. Back On The Pc sideload Magisk to Enable root

```sh
adb devices
adb -d sideload Magisk-v30.6.apk 
```
22. When asked about Signuture verification choose yes/accept
23. when it finishes go back to the Apply update/Apply from ADB section
24. back on the pc flash the mindthegapps file
```sh
adb devices
adb -d sideload MindTheGapps-16.0.0-arm64-20250812_214353.zip 
```
25. When asked about Signuture verification choose yes/accept once more
26. Go back to the main menu
23. Select **Reboot Your system**

You should now be back on **LineageOS with root and gapps**.

---

## Some Notes

- This project supports **Nothing Phone (1) only**
- Current shipped desktop environments are Phosh and Plasma-Mobile
- this Plasma-mobile build is in an experimental state flash at your own risk
- Default password: **7777**
- I am **not responsible** for any damage or data loss

### What Works On The Device:

| Feature     | Status                 |
|------------ |-------------           |
| WiFi        | Working                |
| Mobile Data | Not sure/Untested      |
| Bluetooth   | Not sure/Untested      |
| Calls       | Problematic            |

WiFi note: Detected and working (no need for any manual setup)

Mobile Data: Detected my sim card but i'm currently out of data so couldn't test

Bluetooth note: Detected and should work forgot to test

Calls note: Calls are problematic — you may not hear the other person and they may not hear you. No known fix at this time.

---

## Thanks

Special thanks to **ram9200** on The XDA site for creating the scripts used to generate the images.

XDA thread: https://xdaforums.com/t/linux-postmarketos-for-nothing-phone-1-spacewar.4752989/
more thanks for Veythrix and Nonta72 
and to the PostmarketOS team, Linux Devs and just everyone involved in making this task 

link to script used to genrete the images: https://mega.nz/file/W4onkabC#oXoQG4jybsggVygPG5NqHKSCZCR-ww98yjr0bm6nBQQ

---

## License

MIT License © 2025 barry
