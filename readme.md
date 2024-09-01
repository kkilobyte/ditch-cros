# kkilobyte/ditch-cros - A guide to ditching Chrome OS on your Chrome OS device
## Why?
Well for starters, Chrome OS is a bad operating system, since Google wants to push AI and push virtualizing everything from Android apps and Linux programs in a VM. The only "usable" configuration for Chrome OS on 4 GB Celeron machines is to disable "Play Store" in the Settings, (aka Android or ArcVM), and make sure the Linux developer enviroment (aka Crostini) is also disabled, but that only leaves you with a web browser unless you enable Developer Mode which adds a 30 second wait with a beep (or you can press Ctrl+D on boot) and use Chromebrew, which is kind of a pain in the ass and slow, along with taking up a lot of extra storage.

Solution? Ditch ChromeOS. How? Keep reading.

## Picture Evidence
| <img src="/img/alan-fullrom-alpine-kde.jpg" alt="Alpine Edge KDE on a HP Chromebook 11 G6 EE (alan) using Full ROM" width="400"/> | <img src="/img/phaser360-shimboot-debian12-gnome.jpg" alt="Debian 12 Gnome on a Lenovo 300e Chromebook Flip Gen 2 (phaser360) using Shimboot" width="400"/> |  
| ----- | ----- |
| Alpine Edge KDE on a HP Chromebook 11 G6 EE (alan) using Full ROM | Debian 12 Gnome on a Lenovo 300e Chromebook Flip Gen 2 (phaser360) using Shimboot |

| <img src="/img/vortininja-and-fleex-fullrom-arch-kde.jpg" alt="Arch KDE on a HP Chromebook x360 11 G3 EE (vortininja) and Dell Chromebook 3100 (fleex) using Full ROM" length="400"/>|
| ----- |
| Arch KDE on a HP Chromebook x360 11 G3 EE (vortininja) and Dell Chromebook 3100 (fleex) using Full ROM |

# How?
## Method 1: Best Method (FullROM)
The best experience for any OS is using FullROM. This brings Coreboot+EDK2 but comes with some issues like not being able to use Chrome OS at all unless the stock firmware is restored, and is the only way to run Windows with proper drivers. The follow guide is for Cr50 Chromebooks with the "Cr50 (Battery)" WP method, use [MrChromebox's device table](https://docs.mrchromebox.tech/docs/supported-devices.html) to find your WP method.

1. Backup ALL data using external media or a cloud service.
2. Make sure FWMP is disabled and you are unenrolled. If you are enrolled, you can use SH1mmer's "deprovision" payload to unenroll on Chrome OS v110 and older, you can use SH1mmer's "Cryptosmite" payload to unenroll on Chrome OS v118 and older, you can use "OlyBmmer" to unenroll Chrome OS v124 and older when it releases, and you can use "icarus" to unenroll Chrome OS v130 and older when it releases. If you are not using a business device, FWMP should already be disabled.
3. Enter developer mode by pressing `esc+⟳+⏻ ` and then press `ctrl+d`. You MUST be using the internal keyboard.
4. When your Chromebook says "OS Verification is turned off", press `ctrl+d` again.
5. When Chrome OS boots to "Welcome to your Chromebook", open the Quick Settings menu in the bottom right and click Wi-Fi, and connect to your Wi-Fi.
6. Go back to Quick Settings, and click `⏻ `, if a menu shows up, click "Shut down".
7. If your WP method is "CR50 (battery)", unplug all devices such as USB drives or chargers, open the *back* of the Chromebook using a screwdriver, and pry it off gently, and carefully disconnect the battery.
8. Set the back of the Chromebook on a table, and set your Chromebook on top of the back, but don't click it in or screw it in.
9. Connect a charger.
10. Boot ChromeOS, make sure to press `ctrl+d` on the OS verify screen.
11. Now press `ctrl+alt+🠞` (if you don't have a 🠞 key, press `ctrl+alt+⟳ ` instead).
12. Now type in `chronos` and press `enter`.
13. Now type in `cd; curl -LOk https://mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh`.
14. Your Chromebook might have to reboot, if you are prompted at a `y/n` prompt, press `y` and then `enter`, and wait.
15. Wait for it to reboot, and repeat steps 11 and 12, but this time run `cd; sudo bash firmware-util.sh`.
16. Look for the "Install/Update UEFI (Full ROM) Firmware" option, this is usually option 2.
17. Type in the number for UEFI, in my case it is 2.
18. You may be asked to insert a USB for backup, follow the steps on the screen.
19. Wait for the Chromebook to flash, do NOT use or touch the device during this process.
20. Once it finishes without error, if you already have a Linux/Windows USB, press `enter` and then `r` and then `enter` and skip to step 22, otherwise press `ctrl+alt+🠜`, make sure you have another computer to flash a Linux/Windows USB, or login to ChromeOS to flash a Linux USB using [this guide](https://runtimeterror.dev/burn-an-iso-to-usb-with-the-chromebook-recovery-utility) but with something OTHER than Ubuntu, I recommend [Ultramarine Linux](https://ultramarine-linux.org/).
21. Open Quick Settings, click ⏻  and then Reboot or press `⟳+⏻ `.
22. Your Chromebook can take 30 seconds to 2 minutes to load, wait until you see a bunny rabbit.
23. Press `esc` when you see the bunny rabbit, press `🠟` and then `enter`, and then click on your USB drive.
24. Follow [Chrultrabook's guide](https://docs.chrultrabook.com/docs/installing/installing-linux.html) to install Linux or follow [Coolstar's guide](https://coolstar.org/chromebook/windows-install.html) to install Windows.
25. Hooray!
26. Bonus:
- Linux Audio: [weirdtreething/chromebook-linux-audio](https://github.com/weirdtreething/chromebook-linux-audio)
- Linux keymaps: [weirdtreething/cros-keyboard-map](https://github.com/weirdtreething/cros-keyboard-map)

## Method 2: Easiest Method (AltFw & RW_Legacy)
AltFw is the payload that brings Coreboot+EDK2 UEFI to Chromebooks that aren't EOL and aren't Apollolake and older. 
RW_Legacy is the payload that brings Coreboot_SeaBIOS to Chromebooks that are Apollolake and older. 
EOL Chromebooks do not support either. Windows is ***NOT*** supported and you ***will*** run into issues. You can get a usable experience with AltFw or RW_Legacy but it's not the best.

1. Back up all data using external media or a cloud service like Google Drive. 
2. Make sure FWMP is off and you are unenrolled, follow Step 2 of Method 1: FullROM to unenroll.
3. Enable Developer Mode by by pressing `esc+⟳+⏻ ` and then press `ctrl+d`. You MUST be using the internal keyboard.
4. When your Chromebook says "OS Verification is turned off", press `ctrl+d` again.
5. When Chrome OS boots to "Welcome to your Chromebook", open the Quick Settings menu in the bottom right and click Wi-Fi, and connect to your Wi-Fi.
6. Now press `ctrl+alt+🠞` (if you don't have a 🠞 key, press `ctrl+alt+⟳ ` instead).
7. Now type in `chronos` and press `enter`.
8. Now type in `cd; curl -LOk https://mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh`.
9. Look for the "Install/Update RW_LEGACY Firmware" option, this is usually option 1.
10. Type in the number for RW_LEGACY, in my case it is 1.
11. If you already have a Linux USB, press `enter`, then `r`, and `enter`, and skip to step 14.
12. Otherwise, press `ctrl+alt+🠜`, make sure you have another computer to flash a Linux/Windows USB, or login to ChromeOS to flash a Linux USB using [this guide](https://runtimeterror.dev/burn-an-iso-to-usb-with-the-chromebook-recovery-utility) but with something OTHER than Ubuntu, I recommend [Ultramarine Linux](https://ultramarine-linux.org/).
13. Open Quick Settings, click ⏻  and then Reboot or press `⟳+⏻ `.
14. On the OS verify screen, press `ctrl+l` (L) and then `1`, and then press `esc` when you see the bunny rabbit, press `🠟` and then `enter`, and then click on your USB drive.
15. Follow [Chrultrabook's guide](https://docs.chrultrabook.com/docs/installing/installing-linux.html) to install Linux or follow [Coolstar's guide](https://coolstar.org/chromebook/windows-install.html) to install Windows.
16. Hooray!
17. Bonus:
- Linux Audio: [weirdtreething/chromebook-linux-audio](https://github.com/weirdtreething/chromebook-linux-audio)
- Linux keymaps: [weirdtreething/cros-keyboard-map](https://github.com/weirdtreething/cros-keyboard-map)

## Method 3: Shim
wip

## Method 4: 

# Issues
## General
1. No Ubuntu support. (Fuck Canonical and Ubuntu anyways.)
2. Requires driver fuckery on all OSes, and unsupported OSes will have issues.
3. No ARM support EXCEPT with method 4.
4. Paid Windows driver, (support CoolStar anyways).
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
9. Backlight is *currently* broken on AMD Cezanne devices.
## RW_Legacy
EVERY AltFw issue (except AltFw issue #7) PLUS
1. Broken suspend (at least on `snappy`).
2. BIOS-only / no UEFI.
## Shim
1. Relies on a leaked RMA shim - thus 90% of Chromebooks aren't supported at all.
2. Relies on a glorified chroot.
3. The RMA shim is never updated including the Linux kernel, on `octopus` Chromebooks you get Linux 4.14, on `dedede` Chromebooks you get Linux 5.1, on `reks` and `kefka` you get a Linux kernel too old to run X11!
4. The kernel has a bad configuration (since normal RMA shims aren't meant for normal desktop Linux,) meaning you get no audio (on boards like `nissa` and `dedede`) and no suspend or swap on all boards.
5. Broken GPU acceleration half the time. (For example: X11 on my `meep`, `cret`, `phaser360`, and `fleex`, or Gnome Wayland.)
6. Requires a key combo and a few key inputs to boot.
7. Requires manual building for Linux distros that are not Debian 12 Stable (in Shimboot) or Chrome OS Flex v109 and Arch Linux (in TerraOS).
8. No Windows support AT ALL. Even if you tried, the RMA shim runs the ***Linux kernel*** while Windows runs the ***NT kernel***, and even if you got NT in the shim, you wouldn't be able to "chroot" or whatever.
11. `grunt` Chromebooks on X11 has a weird screen drawing issue where you have to constantly switch in and out of a TTY to render every single new frame.
12. On newui boards like `dedede` and `nissa`, they will have their *shim keys rolled*, meaning all the old shims with old keys will never boot, and the new shims with new keys now have rootfs verification, meaning shim-based Linux enviroments like TerraOS and Shimboot will *NOT* work unless the verification is bypassed and new shims are found.
##
