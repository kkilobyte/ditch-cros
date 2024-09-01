# kkilobyte/ditch-cros - A guide to ditching Chrome OS on your Chrome OS device
## Why?
Well for starters, Chrome OS is a bad operating system, since Google wants to push AI and push virtualizing everything from Android apps and Linux programs in a VM. The only "usable" configuration for Chrome OS on 4 GB Celeron machines is to disable "Play Store" in the Settings, (aka Android or ArcVM), and make sure the Linux developer enviroment (aka Crostini) is also disabled, but that only leaves you with a web browser unless you enable Developer Mode which adds a 30 second wait with a beep (or you can press Ctrl+D on boot) and use Chromebrew, which is kind of a pain in the ass. 

Solution? Ditch ChromeOS. How? Keep reading.

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
AltFw is the payload that brings Coreboot+EDK2 UEFI to Chromebooks that aren't EOL and aren't Apollolake and older. RW_Legacy is the payload that brings Coreboot_SeaBIOS to Chromebooks that are Apollolake and older. EOL Chromebooks do not support either. Windows is ***NOT*** supported and you ***will*** run into issues.

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


# Issues
## General
1. no ubuntu support (fuck ubuntu)
## Full ROM
1. no chrome or chromium OS support (including flex/fydeOS/brunch)
2. requires WP off
3. requires unenrollment
## AltFw
1. no touchscreen
2. no windows support (broken touchpad and touchscreen)
3. requires key combo on boot
4. requires unenrollment
5. broken on grunt
6. not available for EOL
7. UEFI-only / no BIOS/CSM 
## RW_Legacy
Same as AltFw BUT ALSO
1. broken suspend (at least on `snappy`)
2. BIOS-only / no UEFI
## Shim
1. no suspend (shim kernel restrictions)
2. forced to use an old insecure kernel (linux kernel 4.14 on `octopus`)
3. no swap (shim kernel restrictions)
4. no audio (depends on board, `octopus` has working audio)
5. no x11/wayland (on older boards like `kefka` or `reks`)
6. broken gpu accel at times (for example: x11 on `octopus` or gnome wayland)
7. requires key combo and key inputs to boot
8. requires manual building for everything but debian (in shimboot) or chromeOS and arch (in terraOS)
9. no windows
10. requires a leaked shim
11. weird screen drawing issue on `grunt` where you have to open a tty to draw the next frame in x11
