# kkilobyte/ditch-cros - A guide to ditching Chrome OS on your Chrome OS device
## Table of Contents
- [kkilobyte/ditch-cros](#kkilobyte-ditch-cros---a-guide-to-ditching-chrome-os-on-your-chrome-os-device)
  * [DISCLAIMER!!!](#disclaimer---)
  * [Why remove ChromeOS?](#why-remove-chromeos-)
  * [Why make this guide?](#why-make-this-guide-)
  * [Picture Evidence](#picture-evidence)
- [How?](#how-)
  * [Method 1: FullROM](#method-1--best-method--fullrom-)
  * [Method 2: AltFw & RW_Legacy](#method-2--easiest-method--altfw---rw-legacy-)
  * [Method 3: Submarine](#method-3--submarine)
    + [Using a USB drive or SD card](#using-a-usb-drive-or-sd-card)
    + [Using internal storage](#using-internal-storage)
  * [Method 4: Shim](#method-4--shim)
  * [Method 5: Libreboot](#method-5--libreboot--basically-fullrom-for-two-arm-boards-)
- [Issues](#issues)
  * [NOTICE!](#notice)
  * [General](#general)
  * [Full ROM](#full-rom)
  * [AltFw](#altfw)
  * [RW_Legacy](#rw-legacy)
  * [Submarine](#submarine)
  * [Shim](#shim)
  * [Libreboot](#libreboot)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

## DISCLAIMER!!!
I am ***NOT*** responsible for any damage to devices or if you brick a device, and I'm also ***NOT*** responsible if you get in trouble for unenrollment or theft.
Theft ***IS A CRIME***, I do not encourage it at all, and I mention unenrollment ***ONLY*** for documentation and educational purposes.
### Theft can be prosecuted as either a misdemeanor or a felony under US law.

## Why remove ChromeOS?
Well for starters, Chrome OS is a horrible operating system, since Google wants to push AI and push virtualizing everything from Android apps and Linux programs in a VM. 

The only "usable" configuration for Chrome OS on 4 GB Celeron machines is to disable "Play Store" in the Settings, (aka Android or ArcVM), and make sure the Linux developer enviroment (aka Debian or Crostini) is also disabled, but that only leaves you with a web browser unless you enable Developer Mode which adds a 30 second wait with a beep and use Chromebrew, which is kind of a pain in the ass and slow, along with taking up a lot of extra storage.

Overall it's unoptimized and difficult to use. It's very limiting for powerusers (and sometimes normies) and you are better off using literally anything else. 

## Why make this guide?
There isn't a list of ways to run different operating systems on Chromebooks like here, and most people are unaware of methods like Shimboot or Submarine, and only know of the traditional Full ROM and RW_Legacy, and most people go into public Discords asking for someone to hold their hand as they install a better OS.


## Picture Evidence

<details>
 <summary><b>Click here</b></summary>
| <img src="/img/poc/alan-fullrom-alpine-kde.jpg" alt="Alpine Edge KDE on a HP Chromebook 11 G6 EE (alan) using Full ROM" width="400"/> | <img src="/img/poc/phaser360-shimboot-debian12-gnome.jpg" alt="Debian 12 Gnome on a Lenovo 300e Chromebook Flip Gen 2 (phaser360) using Shimboot" width="400"/> |  
| ----- | ----- |
| Alpine Edge KDE on a HP Chromebook 11 G6 EE (alan) using Full ROM | Debian 12 Gnome on a Lenovo 300e Chromebook Flip Gen 2 (phaser360) using Shimboot |

| <img src="/img/poc/vortininja-and-fleex-fullrom-arch-kde.jpg" alt="Arch KDE on a HP Chromebook x360 11 G3 EE (vortininja) and Dell Chromebook 3100 (fleex) using Full ROM" width="500"/> |
| ----- |
| Arch KDE on a HP Chromebook x360 11 G3 EE (vortininja) and Dell Chromebook 3100 (fleex) using Full ROM |

| <img src="/img/poc/hatch-shimboot-debian12-xfce.jpg" alt="Debian 12 XFCE on a Lenovo IdeaPad Flex 5i Chromebook (akemi) using Shimboot" width="400"/> | <img src="/img/poc/drawcia-shimboot-debian12-gnome.jpg" alt="Debian 12 Gnome on a HP Chromebook 11 G9 EE (drawcia) using Shimboot" width="400">
| ----- | ----- |
| Debian 12 XFCE on a Lenovo IdeaPad Flex 5i Chromebook (akemi) using Shimboot | Debian 12 Gnome on a HP Chromebook 11 G9 EE (drawcia) using Shimboot |

| <img src="/img/poc/vortininja-fullrom-ultramarine-kde.jpg" alt="Ultramarine 40 KDE on a HP Chromebook x360 11 G3 EE (vortininja) using Full ROM" width="400"/> | <img src="/img/poc/meep-fullrom-bootscreen.jpg" alt="Coreboot bootup logo on a HP Chromebook x360 11 G2 EE (meep) using Full ROM" width="400">
| ----- | ----- |
| Ultramarine 40 KDE on a HP Chromebook x360 11 G3 EE (vortininja) using Full ROM | Coreboot bootup logo on a HP Chromebook x360 11 G2 EE (meep) using Full ROM |

| <img src="/img/poc/fleex-shimboot-void-dwm.jpg" alt="Void DWM on a Dell Chromebook 3100 (fleex) using Shimboot" width="500"/> | <img src="/img/poc/barla-fullrom-bootscreen.jpg" alt="HP bootup logo on a modified HP Chromebook 11A G6 EE (barla) using Full ROM" width="500">
| ----- | ----- | 
| Void DWM on a Dell Chromebook 3100 (fleex) using Shimboot | HP bootup logo on a modified HP Chromebook 11A G6 EE (barla) using Full ROM | 

| <img src="/img/poc/craaskbowl-fullrom-bootscreen.jpg" alt="Coreboot boot logo on an Acer Chromebook Spin 511 (craaskbowl) using Full ROM" width="500"/> |
| ----- |
| Coreboot boot logo on an Acer Chromebook Spin 511 (craaskbowl) using Full ROM |

(credits to error404/null/symlink, kelsea/crossystem, kxtzownsu/katelyn, and vk6/ading2210 because i stole half of these from them)
</details>

# How?
## Method 1: Best Method (FullROM)
The best experience for any OS is using FullROM. This brings Coreboot+EDK2 but comes with some issues like not being able to use Chrome OS at all unless the stock firmware is restored, and is the only way to run Windows with proper drivers. The follow guide is for Cr50 Chromebooks with the "Cr50 (Battery)" WP method, use [MrChromebox's device table](https://docs.mrchromebox.tech/docs/supported-devices.html) to find your WP method.

1. Backup ALL data using external media or a cloud service.
2. Make sure FWMP is disabled and you are unenrolled. If you are enrolled, you can use [the unenrollment guide](/unenroll.md). If you are not using a business device, FWMP should already be disabled.
3. Enter developer mode by pressing `esc+⟳+⏻ ` (`esc+refresh+power`) and then press `ctrl+d`. You MUST be using the internal keyboard.
4. When your Chromebook says "OS Verification is turned off", press `ctrl+d` again.
5. When Chrome OS boots to "Welcome to your Chromebook", open the Quick Settings menu in the bottom right and click Wi-Fi, and connect to your Wi-Fi.
6. Go back to Quick Settings, and click `⏻ `, if a menu shows up, click "Shut down".
7. If your WP method is "CR50 (battery)", unplug all devices such as USB drives or chargers, open the *back* of the Chromebook using a screwdriver, and pry it off gently, and carefully disconnect the battery.
8. Set the back of the Chromebook on a table, and set your Chromebook on top of the back, but don't click it in or screw it in.
9. Connect a charger.
10. Boot ChromeOS, make sure to press `ctrl+d` on the OS verify screen.
11. Now press `ctrl+alt+🠞` (above the 2, if you don't have a 🠞 key, press `ctrl+alt+⟳` (refresh, above the 2 or 4) instead).
12. Now type in `chronos` and press `enter`.
13. Now type in `cd; curl -LOk https://mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh`.
14. Your Chromebook might have to reboot, if you are prompted at a `y/n` prompt, press `y` and then `enter`, and wait.
15. Wait for it to reboot, and repeat steps 11 and 12, but this time run `cd; sudo bash firmware-util.sh`.
16. Look for the "Install/Update UEFI (Full ROM) Firmware" option, this is usually option 2.
17. Type in the number for UEFI, in my case it is 2.
18. You may be asked to insert a USB for backup, follow the steps on the screen.
19. Wait for the Chromebook to flash, do NOT use or touch the device during this process.
20. Once it finishes without error, if you already have a Linux/Windows USB, press `enter` and then `r` and then `enter` and skip to step 22, otherwise press `ctrl+alt+🠜` (above the 1), make sure you have another computer to flash a Linux/Windows USB, or login to ChromeOS to flash a Linux USB using [this guide](https://runtimeterror.dev/burn-an-iso-to-usb-with-the-chromebook-recovery-utility) but with something OTHER than Ubuntu, I recommend [Ultramarine Linux](https://ultramarine-linux.org/).
21. Open Quick Settings, click ⏻  (power) and then Reboot or press `⟳+⏻ ` (`refresh+power`).
22. Your Chromebook can take 30 seconds to 2 minutes to load, wait until you see a bunny rabbit.
23. Press `esc` when you see the bunny rabbit, press `🠟` (down arrow) and then `enter`, and then click on your USB drive.
24. Follow [Chrultrabook's guide](https://docs.chrultrabook.com/docs/installing/installing-linux.html) to install Linux or follow [Coolstar's guide](https://coolstar.org/chromebook/windows-install.html) to install Windows.
25. Hooray!
26. Bonus:
- Linux Audio: [weirdtreething/chromebook-linux-audio](https://github.com/weirdtreething/chromebook-linux-audio)
- Linux keymaps: [weirdtreething/cros-keyboard-map](https://github.com/weirdtreething/cros-keyboard-map)
If you are installing Windows, the above is already handled by the guide.

## Method 2: Easiest Method (AltFw & RW_Legacy)
AltFw is the payload that brings Coreboot+EDK2 UEFI to Chromebooks that are Geminilake and newer. 
RW_Legacy is the payload that brings Coreboot_SeaBIOS to Chromebooks that are Apollolake and older. 
EOL Chromebooks do not support either. Stoneyridge Chromebooks may not work with either. Windows is ***NOT*** supported and you ***will*** run into issues. You can get a usable experience with AltFw or RW_Legacy but it's not the best. You do not choose if you get AltFw or RW_Legacy.

1. Back up all data using external media or a cloud service like Google Drive. 
2. Make sure FWMP is disabled and you are unenrolled. If you are enrolled, you can use [the unenrollment guide](/unenroll.md). If you are not using a business device, FWMP should already be disabled.
3. Enable Developer Mode by by pressing `esc+⟳+⏻ ` (`esc+refresh+power`) and then press `ctrl+d`. You MUST be using the internal keyboard.
4. When your Chromebook says "OS Verification is turned off", press `ctrl+d` again.
5. When Chrome OS boots to "Welcome to your Chromebook", open the Quick Settings menu in the bottom right and click Wi-Fi, and connect to your Wi-Fi.
6. Now press `ctrl+alt+🠞` (above the 2, if you don't have a 🠞 key, press `ctrl+alt+⟳ ` (refresh, above the 2 or 4) instead).
7. Now type in `chronos` and press `enter`.
8. Now type in `cd; curl -LOk https://mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh`.
9. Look for the "Install/Update RW_LEGACY Firmware" option, this is usually option 1.
10. Type in the number for RW_LEGACY, in my case it is 1.
11. If you already have a Linux USB, press `enter`, then `r`, and `enter`, and skip to step 14.
12. Otherwise, press `ctrl+alt+🠜` (above the 1), make sure you have another computer to flash a Linux/Windows USB, or login to ChromeOS to flash a Linux USB using [this guide](https://runtimeterror.dev/burn-an-iso-to-usb-with-the-chromebook-recovery-utility) but with something OTHER than Ubuntu, I recommend [Ultramarine Linux](https://ultramarine-linux.org/).
13. Open Quick Settings, click ⏻  (power) and then Reboot or press `⟳+⏻ ` (`refresh+power`).
14. On the OS verify screen, press `ctrl+l` (L) and then `1`, and then press `esc` when you see the bunny rabbit, press `🠟` (down arrow) and then `enter`, and then click on your USB drive.
15. Follow [Chrultrabook's guide](https://docs.chrultrabook.com/docs/installing/installing-linux.html) to install Linux or follow [Coolstar's guide](https://coolstar.org/chromebook/windows-install.html) to install Windows.
16. Hooray!
17. Bonus:
- Linux Audio: [weirdtreething/chromebook-linux-audio](https://github.com/weirdtreething/chromebook-linux-audio)
- Linux keymaps: [weirdtreething/cros-keyboard-map](https://github.com/weirdtreething/cros-keyboard-map)

## Method 3: Submarine
1. Back up all data using external media or a cloud service like Google Drive. 
2. Make sure FWMP is disabled and you are unenrolled. If you are enrolled, you can use [the unenrollment guide](/unenroll.md). If you are not using a business or enterprise device, FWMP should already be disabled. 
3. Enable Developer Mode by by pressing `esc+⟳+⏻ ` (`esc+refresh+power`) and then press `ctrl+d`. You MUST be using the internal keyboard.
4. When your Chromebook says "OS Verification is turned off", press `ctrl+d` again.
5. When Chrome OS boots to "Welcome to your Chromebook", open the Quick Settings menu in the bottom right and click Wi-Fi, and connect to your Wi-Fi.
6. Continue with ChromeOS setup and login.
7. Press `ctrl+🔍+esc` and look at CPU, if it says AMD or Intel, download [this](https://nightly.link/FyraLabs/submarine/workflows/build/main/submarine-x86_64.zip), if it says Rockchip, Samsung Exynos, MediaTek, download [this instead](https://nightly.link/FyraLabs/submarine/workflows/build/main/submarine-arm64.zip), and extract the file you downloaded to `My Files/Downloads`
8. Now press `ctrl+alt+🠞` (above the 2, if you don't have a 🠞 key, press `ctrl+alt+⟳ ` (refresh, above the 2 or 4) instead).
9. Type in `chronos` and press enter, and then run `sudo enable_dev_usb_boot`.

### Using a USB drive or SD card
10. Plug in your external storage device (without the data you backed up) and run `sudo lsblk` and look for your drive.
12. Run `cd; sudo dd if=MyFiles/Downloads/submarine-<arch>.kpart of=/dev/<storage device> bs=16M status=progress oflag=direct`.
13. Take out your USB drive, run `sudo reboot` or press `⟳+⏻ `, plug in the device you flashed in on the white screen and press Ctrl+U.
14. If all goes well, you should soon see the Submarine boot menu.
15. You should be able to install Linux via the boot menu off of a USB drive, to install Linux Mint (Debian edition), follow [this guide](https://developer.fyralabs.com/submarine/guide_lmde), for Debian, follow [this guide](https://developer.fyralabs.com/submarine/guide_debian), and for Arch, follow [this guide](https://developer.fyralabs.com/submarine/guide_arch).
16. Hooray!
17. Bonus:
- Linux Audio: [weirdtreething/chromebook-linux-audio](https://github.com/weirdtreething/chromebook-linux-audio)
- Linux keymaps: [weirdtreething/cros-keyboard-map](https://github.com/weirdtreething/cros-keyboard-map)

### Using internal storage
10. Start by creating a 16 MB EXT4 partition using your favorite partitioning tool.
11. Run `cgpt add -i <partition number> -t kernel -P 15 -T 1 -S 1 /dev/mmcblk0`
12. Run `cd; sudo dd if=MyFiles/Downloads/submarine-<arch>.kpart of=/dev/mmcblk0p<partition> bs=16M status=progress oflag=direct`.
13. You should be able to install Linux via the boot menu off of a USB drive, to install Linux Mint (Debian edition), follow [this guide](https://developer.fyralabs.com/submarine/guide_lmde), for Debian, follow [this guide](https://developer.fyralabs.com/submarine/guide_debian), and for Arch, follow [this guide](https://developer.fyralabs.com/submarine/guide_arch).
14. Hooray!
15. Bonus:
- Linux Audio: [weirdtreething/chromebook-linux-audio](https://github.com/weirdtreething/chromebook-linux-audio)
- Linux keymaps: [weirdtreething/cros-keyboard-map](https://github.com/weirdtreething/cros-keyboard-map)

## Method 4: Shim
Shim-based Linux booting uses the default Coreboot+Depthcharge firmware that Google ships on all Chromebooks, however it doesn't run as decent as ChromeOS. For starters, Developer mode must be on (however it does not matter if FWMP is on), and you must boot into recovery mode (the same screen that you use to reinstall ChromeOS). All thanks to a tool for repair shops and schools.

1. Decide on rather you want Shimboot (Debian) or TerraOS (Arch). Shimboot is better maintained and TerraOS's systemd is outdated, and Shimboot is known to work better on ARM (`jacuzzi`) Chromebooks.
2. Figure out your [device board](/device-identify.md#board-name).
3. If you want Shimboot, get the latest build for your board from [ading2210/shimboot/releases](https://github.com/ading2210/shimboot/releases) or [dl.darkn.bio/shimboot](https://dl.darkn.bio/Shimboot). If you want you TerraOS, get the latest build for your board from [files.mercurywork.shop/r58playz/terraos/arch-images/](http://files.mercurywork.shop/r58playz/terraos/arch-images/).
3a. If your board does not show, you will have to manually build using a personal device. [/r58playz/terraos](https://github.com/r58playz/terraos) | [/ading2210/shimboot](https://github.com/ading2210/shimboot)
3b. You can grab raw unmodified RMA shims from [dl.darkn.bio/sh1mmer/raw](https://dl.darkn.bio/SH1mmer/Raw).
4. Once you obtain a Shimboot/TerraOS shim for your device, flash it to a USB drive. If you are using Windows/MacOS/ChromeOS to flash, use [this guide](https://runtimeterror.dev/burn-an-iso-to-usb-with-the-chromebook-recovery-utility) to flash. If you are using Linux, run `lsblk`, find your USB drive, find your Linux shim, and run `sudo dd if=<linux shim> of=/dev/<usb drive> oflag=direct status=progress bs=16M`.
5. If you are using TerraOS, run `sudo growpart /dev/<usb drive> 4` and `sudo resize2fs /dev/<usb drive>4` you might need to install `cloud-utils-growpart` and `e2fsprogs`.
6. Back up ALL data using external media or a cloud service.
7. Enable Developer Mode by by pressing `esc+⟳+⏻ ` and then press `ctrl+d`. You MUST be using the internal keyboard.
8. There might be mysterious black text in the top left corner, ignore this and press `esc+⟳+⏻ ` again and insert your Linux shim USB.
9. On Shimboot, press `3` and then `enter`, on TerraOS, press `->` (right arrow) and then `enter`, and then `🠟` (down arrow) twice, and then `enter`.
10. You should be greeted with a login page. On Shimboot, put `user` as the username and password, on TerraOS put `terraos` as the username and password.
11. On Shimboot, open a terminal with `ctrl+alt+t` and then run `sudo expand_rootfs`. TerraOS users may skip this step.

### You are now in a Xfce enviroment on your USB drive, if you want to flash to your eMMC/internal storage and replace chromeOS, continue with steps 12 to 16, otherwise skip to 17.

12. You can use the computer you flashed to put the Shimboot/TerraOS image onto `/home/user/` (on Shimboot) or `/home/terraos` (on TerraOS) or you can download the Linux shim image inside of Xfce.
13. Boot back into Xfce (if you need to), open a terminal, and run `lsblk`, find the option the has mmcblk, and check if it has `0` or `1`.
14. Now run `sudo dd if=<shim image> of=/dev/mmblk<num> bs=16M status=progress oflag=direct`, and then `sudo reboot`.
15. Repeat step 5 on TerraOS but with your `mmcblk<num>` instead of `<usb>`.
16. Boot back into the bootloader, on Shimboot press `1` and then `enter`, on TerraOS press `->` (right arrow) and then `enter`.
17. Login with `user` for user/pass on Shimboot, login with `terraos` for user/pass on TerraOS.
18. On Shimboot, repeat step 11.
19. Make a new user. Open a terminal with `ctrl+alt+t` and run `sudo adduser <your username here>`, and then run `sudo adduser <username> sudo`.
20. Press `⏻ ` (power) and then click log out. Login as your new user, open a terminal with `ctrl+alt+t`, and run `sudo deluser user` or `sudo deluser terraos`.

### You are now in a Xfce enviroment on your eMMC, congrats. Run the following to get a proper experience.

21. Bonus:
- Linux Audio: [weirdtreething/chromebook-linux-audio](https://github.com/weirdtreething/chromebook-linux-audio)
- Linux keymaps: [weirdtreething/cros-keyboard-map](https://github.com/weirdtreething/cros-keyboard-map)

# UNFINISHED GUIDE

## Method 5: Libreboot (basically FullROM for two ARM boards)
Libreboot, a Coreboot distro, has [*official* Chromebook support](https://libreboot.org/docs/install/chromebooks.html) but only for "nyan" and "gru" Chrome devices.

1. Back up all data using a cloud service or external media.
2. Make sure FWMP is disabled and you are unenrolled. If you are enrolled, you can use [the unenrollment guide](/unenroll.md). If you are not using a business device, FWMP should already be disabled.
3. Enable Developer Mode by by pressing `esc+⟳+⏻ ` (`esc+refresh+power`) and then press `ctrl+d`. You MUST be using the internal keyboard.
4. When your Chromebook says "OS Verification is turned off", press `ctrl+d` again.
5. Connect to Wi-Fi from Quick Settings in the bottom right.
6. Now press `ctrl+alt+🠞` (above the 2, if you don't have a 🠞 key, press `ctrl+alt+⟳ ` (refresh, above the 2 or 4) instead).
7. Enter `chronos` and then press `enter`.
8. Run `sudo crossystem hwid`. Keep note of this.
9. On most Libreboot-supported devices, you have the "[WP Screw](https://docs.mrchromebox.tech/docs/firmware/wp/disabling.html#removing-the-write-protection-screw)" method to disable hardware write protection. This guide assumes you have that method.
10. Open the back of the Chromebook, disconnect the battery, and look for "`WP SCREW`". Once you find it, remove it, and power the device back on.
11. Login to ChromeOS.
12. Now press `ctrl+alt+🠞` (above the 2, if you don't have a 🠞 key, press `ctrl+alt+⟳ ` (refresh, above the 2 or 4) instead).
13. Run the following:
`sudo flashrom -p host --wp-status
sudo flashrom -p host --wp-disable
sudo flashrom -p host --wp-range 0x0,0x0`
14. Run the following:
`cd ~/MyFiles/Downloads
sudo flashrom -p host -r depthcharge.rom
sudo flashrom -p host -v depthcharge.rom`
15. Make sure you have an installation media.
[Arch Linux ARM](https://libreboot.org/docs/uboot/uboot-archlinux.html) on `gru bob` and other RK3399 Chromebooks works.
[Debian 12](https://libreboot.org/docs/uboot/uboot-debian-bookworm.html) on `gru kevin` works.
[Debian has a DebianOn guide](https://wiki.debian.org/InstallingDebianOn/Asus/C201) for `veyron speedy`, however other RK3288 based Chromebooks should work too.
Follow [this guide](https://runtimeterror.dev/burn-an-iso-to-usb-with-the-chromebook-recovery-utility) to flash using ChromeOS.
16. Back up `depthcharge.rom` to a cloud service or external media.
17. 

# Issues
## NOTICE!
General hardware issues like the numerous hardware bugs `celes` has or the very poor quality control of `kohaku` causing the deteriorating trackpad grounding or the faulty backlight circuit, still apply REGARDLESS the firmware. This will persist from either ChromeOS or Linux or Windows or WHATEVER. Do not blame hardware bugs on the custom firmware.
## General
1. No Ubuntu support. (Fuck Canonical and Ubuntu anyways.)
2. Requires driver fuckery on all OSes, and unsupported OSes will have issues.
3. No ARM support EXCEPT with Submarine, Shimboot, and Libreboot
4. Paid Windows audio driver, (on non-EOL and non-Stoneyridge Chromebooks, support CoolStar anyways).
5. Sometimes the Chromebook will turn itself back on (like when the charger is plugged in or taken out) in BOTH Linux and Windows.
6. DisplayPort and VGA output via the DVI port doesn't work in Windows on `stumpy`.
## Full ROM
1. No Chrome or Chromium OS support, (you will run into driver issues like with audio or the trackpad).
2. Requires WP to be OFF
3. Requires an unenrolled device.
## AltFw
1. No touchscreen (at least not on `octopus`).
2. No Windows support. (You will run into driver issues, like with the touchscreen or trackpad.)
3. Requires a key combo to boot. (Workaround exists but requires WP to be OFF to change GBB flags.)
4. Requires an unenrolled device.
5. AltFw payload list works but does not display correctly on Intel Geminilake devices. Just press "1" on the `ctrl+l` (L) menu.
6. Not available for EOL devices.
7. UEFI-only / no BIOS/CSM.
8. Lots of AMD Stoneyridge devices do not currently have functional AltFw.
9. Backlight is broken on AMD Cezanne devices.
10. Menus such as the boot splash, EDK2 UEFI settings, EFI shell, or GRUB are stretched and look kinda weird.
## RW_Legacy
EVERY AltFw issue (except AltFw issue #7) PLUS
1. Broken suspend (at least on `snappy`).
2. BIOS-only / no UEFI.
3. Everything before GPU drivers load, such as Windows Boot Loader, Ventoy, GRUB, or verbose boot only shows in a small 800x600 box in the top left portion of the screen, at least on `snappy`.
4. Too minimal, no TUI's, you only get a CLI to select a number that corresponds to your boot device, similar to Shimboot.
## Submarine
1. Requires an unenrolled device.
2. No Windows *at all*.
3. Screen doesn't initialize on some MT8192 Chromebooks.
4. Touchscreen might not work for some.
5. Requires key combo on boot (if you use the Ctrl+U method).
## Shim
1. Relies on a leaked RMA shim - thus 90% of Chromebooks aren't supported at all.
2. Relies on a glorified chroot.
3. The RMA shim is never updated including the Linux kernel, on `octopus` Chromebooks you get Linux 4.14, on `dedede` Chromebooks you get Linux 5.1, on `reks` and `kefka` you get a Linux kernel too old to run X11!
4. The kernel has a bad configuration (since normal RMA shims aren't meant for normal desktop Linux,) meaning you get no audio (on boards like `nissa` and `dedede`) and no suspend or swap on all boards.
5. Broken GPU acceleration half the time. (For example: X11 on my `meep`, `cret`, `phaser360`, and `fleex`, or Gnome Wayland.)
6. Requires a key combo and a few key inputs to boot.
7. Requires manual building for Linux distros that are not Debian 12 Stable (in Shimboot) or Chrome OS Flex v109 and Arch Linux (in TerraOS).
8. No Windows *at all*.
11. `grunt` Chromebooks on X11 has a weird screen drawing issue where you have to constantly switch in and out of a TTY to render every single new frame.
12. On newui boards like `dedede` and `nissa`, they will have their *shim keys rolled*, meaning all the old shims with old keys will never boot, and the new shims with new keys now have rootfs verification, meaning shim-based Linux enviroments like TerraOS and Shimboot will *NOT* work unless the verification is bypassed and new shims are found.
13. Shimboot's selector is kinda ugly and very minimal. No TUI business, just a CLI to select the number that corresponds to your boot device.
14. Updating Arch in TerraOS using `pacman -Syu` will cause Arch to break. A workaround is to use `yay -Syu` or `paru -Syu` instead. 
15. You will have to manually wait for systemd to compile for Arch from the AUR on TerraOS.
## Libreboot
1. Only supported on "`nyan`" and "`gru`" boards. Both of these boards are not found on [cros.tech](https://cros.tech) or [chromiumdash](https://chromiumdash.appspot.com), however devices that are referenced to, such as [`gru kevin`](https://cros.tech/device/kevin/) exists on cros.tech, however without a board name.
2. Requires WP to be OFF.
3. Must be unenrolled.
4. Horrible Linux distro support.
5. No Windows *at all* afaik.
6. Pretty mediocore install guide (FROM Libre themselves!!!)
7. I can't find a download.
