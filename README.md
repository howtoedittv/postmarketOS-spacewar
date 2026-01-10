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

### 2. Get adb and fastboot (Only needed if You Dont Have adb and fastboot installed) 

Run the provided script:

```sh
./get-sdk
```

---

## Unlocking The Bootloader 

> Skip this section if your bootloader is already unlocked.

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
fastboot erase vendor_boot
fastboot erase dtbo
```

6. Flash postmarketOS images:

```sh
cd ~/postmarketOS-spacewar/des/
xz -d <<your desired dektop environment>.tar.gz.xz
tar -xvf <<your desired dektop environment>.tar.gz
cd ~/postmarketOS-spacewar/des/<your desired dektop environment>
fastboot flash boot boot.img
fastboot flash userdata userdata.img
```

7. Reboot:

```sh
fastboot reboot
```

You should now boot into **postmarketOS** on your Nothing Phone (1).

---

## Restore Instructions

> This restore process is **only for LineageOS** at the moment.

1. From the project directory, run:

```sh
cd ~/postmarketOS-spacewar
./restore
```

2. After it finishes, a new directory called `lin` will appear:

```sh
cd lin
```

3. Power off the phone
4. Power it back on while holding **Power + Volume Up**
5. When the Nothing logo appears:
   - Release **Power**
   - Keep holding **Volume Up** until you enter the bootloader

6. On your PC, verify fastboot:

```sh
fastboot devices
```

7. Erase partitions:

```sh
fastboot erase vendor_boot
fastboot erase userdata
```

8. Flash LineageOS images:

```sh
cd ~/postmarketOS-spacewar/lin
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
    - Confirm

11. Go back using volume keys and power button
12. Select **Advanced**
13. Enable **ADB**
14. Go back to the first menu
15. Go to apply update
16. Go to apply update via adb

17. On your PC, sideload LineageOS:

```sh
adb devices
adb -d sideload lin.zip
```

15. When asked to reboot back to recovery, select **No**
16. Select **Reboot**

You should now be back on **LineageOS**.

---

## Some Notes

- This project supports **Nothing Phone (1) only**
- Current shipped desktop environments are Phosh and Plasma Mobile
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

Bluetooth note: Detected and should work couldn't test

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
