 # Unenrollment for Chrome OS Devices
Useful for ditching ChromeOS and using Full ROM, AltFw, or RW_Legacy methods.
Remember! You can always use the Shim method for Linux without unenrollment!

## Why?
Every method except the Shim method requires FWMP to be missing as Developer Mode is required, but FWMP blocks Developer Mode. Thus we need to remove FWMP. 

## What Kernver and ChromeOS version do I have?
To verify your kernver and your ChromeOS version, you need to first boot ChromeOS and then press `alt+v`, you will find a number followed by other numbers, only the first 2 or 3 numbers matter, such as `94`, `110` or `127`. Take note of this number and find the method related. If it is `120` or higher, you should check your kernver. Press `esc+⟳+⏻ ` (`esc+refresh+power`), and then `tab`. 

Now, you just scroll down with your eyes until you find `tpm_ver`, and then look to the right of that to find `tpm_kernver`, and your kernver will be the last number to the right of kernver, this means `tpm_kernver=0x00010004` is kernver 4 or kv4.

# How?
## ChromeOS v101 and below - SHroot
Pretty cool universal USB-less unenrollment exploit that requires you to have a Chromebook that hasn't been touched in years. It exploits a bash shell and root escalation method in Crosh that has been long patched, but still very neat and very easy.

1. Login to your Chromebook.
2. Open Crosh with `ctrl+alt+t`. If it says `crosh is blocked`, use SH1mmer.
3. Paste the following in:

`set_cellular_ppp \';dbus-send${IFS}--system${IFS}--print-reply${IFS}--dest=org.chromium.SessionManager${IFS}/org/chromium/SessionManager${IFS}org.chromium.SessionManagerInterface.ClearForcedReEnrollmentVpd;exit;\'`

Just like this \
<img src="/img/tutorial/crosh-rootesc.png" width="1000">

5. Press `enter`.
6. Back up all data to an external media (like a USB flash drive) or a cloud service (like Google Drive).
7. Press `esc+⟳+⏻ ` (`esc+refresh+power`).
8. Press `ctrl+d` and then `enter`.
9. On the scary screen with black text at the top left, press `enter` again.
10. Wait for ChromeOS to boot, and then go through the setup.
11. Now you can set up ChromeOS with a personal Google account and use [Full ROM](/readme.md#method-1-best-method-fullrom) or [AltFw](/readme.md#method-2-easiest-method-altfw--rw_legacy)!

## ChromeOS v110 and below - SH1mmer
The preferred unenrollment method for ChromeOS v110 and below is using SH1mmer's very cool "deprovision" option. This takes ownership of the TPM and erases the FWMP, along with making ChromeOS not check for enrollment by putting a parameter in the RW portion of the VPD.

1. Back up all data to an external storage device or cloud service. You must not use the same storage device as the device you will be using SH1mmer with.
2. If you are using ChromeOS, MacOS, or Windows, download [this extension](https://chromewebstore.google.com/detail/chromebook-recovery-utili/pocpnlppkickgojjlmhdmidojbmbodfm). (Linux users skip this step.) If you only have the Chromebook and this is blocked, try using [Skiovox](https://skiovox.com/skiovox.pdf). If you are using a version where Skiovox is patched, you can't use SH1mmer anyways.
3. [Identify](/device-identify.md) what Chromebook *board* you have.
4. Find and download your *board*'s SH1mmer [here](https://dl.darkn.bio/SH1mmer/Prebuilt/Legacy), if it's missing, good luck, use BadRecovery or CRSH2TTY.
5. Open your "Downloads" folder in the "Files" app, double click on the SH1mmer zip file, and drag the SH1mmer bin file to your Downloads folder.
6. If you are using Linux, skip to step 8, otherwise open a Chrome tab, click on the puzzle icon in the top right, and click on "Chromebook Recovery Utility".

<img src="/img/tutorial/chrome-recovery-extension.png">
7. Click on the ⚙ (settings) icon in the corner and click "Use local image" and the select your SH1mmer bin file.
<img src="/img/tutorial/cru-local-image.png">

8. If you don't use Linux, skip to step 9, otherwise, open a terminal and run `lsblk` and verify what your USB drive is, once you have verified, run `cd ~/Downloads; sudo dd if=<sh1mmer file> of=/dev/sd<usb letter> oflag=direct status=progress bs=16M` and wait. Skip to step 10.
9. Plug in the USB drive that you want to use for SH1mmer, do ***NOT*** use the USB drive with your data if you backed up data to a USB drive.
10. Verify this USB drive doesn't have important data and then wait for it to flash.
11. Once finished, press `esc+⟳+⏻ ` (`esc+refresh+power`) and then `ctrl+d`. Then press `esc+⟳+⏻ ` (`esc+refresh+power`) again and insert the USB.
12. Wait for SH1mmer to load, once you are greeted with a scary menu with lots of options.
<img src="/img/tutorial/sh1mmer.jpg" width="400">

13. Press `d` and then `enter`, this should come with two messages both having "SUCCESS!". Once it says "FINISHED", preform an EC reset by pressing `⟳+⏻ ` (`refresh+power`).
14. You should be greeted at a "OS Verification is off" screen but with no black text in the corner. Press `ctrl+d` whenever you Chromebook turns on and you see this screen. 
15. Setup ChromeOS as normal
16. Now you can set up ChromeOS with a personal Google account and use [Full ROM](/readme.md#method-1-best-method-fullrom) or [AltFw](/readme.md#method-2-easiest-method-altfw--rw_legacy)!
<img src="/img/tutorial/craaskbowl-unroll-google.png" width="400">

## ChromeOS v118 and below - CryptoSmite
The preferred unenrollment method for ChromeOS v118 and below is using SH1mmer's not-as-cool "CryptoSmite" option. This writes a corrupted cryptohome to your data partition, or "stateful", using some random Google account, but this removes FWMP, so you can easily go into Developer Mode with no restrictions.

1. Back up all data to an external storage device or cloud service. You must not use the same storage device as the device you will be using CryptoSmite with.
2. If you are using ChromeOS, MacOS, or Windows, download [this extension](https://chromewebstore.google.com/detail/chromebook-recovery-utili/pocpnlppkickgojjlmhdmidojbmbodfm). (Linux users skip this step.) If you only have the Chromebook and this is blocked, try using [Skiovox](https://skiovox.com/skiovox.pdf). If you are using a version where Skiovox is patched, you can't use CryptoSmite anyways.
3. [Identify](/device-identify.md) what Chromebook *board* you have.
4. Find and download your *board*'s SH1mmer [here](https://dl.darkn.bio/SH1mmer/Prebuilt/Legacy), if it's missing, good luck, use BadRecovery or CRSH2TTY.
5. Open your "Downloads" folder in the "Files" app, double click on the SH1mmer zip file, and drag the SH1mmer bin file to your Downloads folder.
6. If you are using Linux, skip to step 8, otherwise open a Chrome tab, click on the puzzle icon in the top right, and click on "Chromebook Recovery Utility".

<img src="/img/tutorial/chrome-recovery-extension.png">
7. Click on the ⚙ (settings) icon in the corner and click "Use local image" and the select your SH1mmer bin file.
<img src="/img/tutorial/cru-local-image.png">

8. If you don't use Linux skip to step 9, otherwise, open a terminal and run `lsblk` and verify what your USB drive is, once you have verified, run `cd ~/Downloads; sudo dd if=<sh1mmer file> of=/dev/sd<usb letter> oflag=direct status=progress bs=16M` and wait. Skip to step 10.
9. Plug in the USB drive that you want to use for SH1mmer, do ***NOT*** use the USB drive with your data if you backed up data to a USB drive.
10. Verify this USB drive doesn't have important data and then wait for it to flash.
11. Once finished, press `esc+⟳+⏻ ` (`esc+refresh+power`) and then `ctrl+d`. Then press `esc+⟳+⏻ ` (`esc+refresh+power`) again and insert the USB.
12. Wait for SH1mmer to load, once you are greeted with a scary menu with lots of options.
<img src="/img/tutorial/sh1mmer.jpg" width="400">

13. Press `p` and then select "Cryptosmite" with the arrow keys.
14. Wait for ChromeOS to reboot.
15. Connect to internet.
16. Remove the SH1mmer USB from the Chromebook and press `esc+⟳+⏻ ` and then `ctrl+d`.
17. Connect the USB back into the chromebook and press `esc+⟳+⏻ ` again but this time press `h` for `Touch .developer_mode` and then preform an EC reset by pressing `⟳+⏻ ` (`refresh+power`), on the OS verification screen press `ctrl+d`.
18. Wait for ChromeOS to boot.
19. QUICKLY!!! press `ctrl+alt+🠞` (above the 2, if you don't have a 🠞 key, press `ctrl+alt+⟳` (refresh, above the 2 or 4) instead).
20. Now type in `root` and press `enter`.
21. Run `vpd -i RW_VPD -s check_enrollment=0`
22. Now run `cryptohome --action=remove_firmware_management_parameters`. If that shows a bunch of `--action=` text, run `device_management_client --action=remove_firmware_management_parameters` instead.
23. Press `ctrl+alt+🠜` (above the 1), and setup ChromeOS as normal.
24. If you see `Enterprise enrollment`, quickly boot into SH1mmer, open bash, and run `mkfs.ext4 /dev/mmcblk*p1`, and repeat 13 to 23 again. 
25. Congrats! Now you can set up ChromeOS with a personal Google account and use [Full ROM](/readme.md#method-1-best-method-fullrom) or [AltFw](/readme.md#method-2-easiest-method-altfw--rw_legacy)!
<img src="/img/tutorial/craaskbowl-unroll-google.png" width="400">

## ChromeOS v124 and below - BadRecovery (formerly OlyBmmer) <!-- i have no idea how accurate this guide is going to be because i have never used badrecovery before -->
BadRecovery (not to be confused with the iOS exploit) is the preferred unenrollment method for ChromeOS v124 and below. It leverages a vulnerability in recovery images to get arbitrary code execution or to chain to other exploits (such as Cryptosmite).

1. Back up all data to an external storage device or cloud service. You must not use the same storage device as the device you will be using BadRecovery with.
2. If you are using ChromeOS, MacOS, or Windows, download [this extension](https://chromewebstore.google.com/detail/chromebook-recovery-utili/pocpnlppkickgojjlmhdmidojbmbodfm). (Linux users skip this step.) 
3. [Identify](/device-identify.md) what Chromebook *board* you have.
4. Find and download your *board*'s BadRecovery [here](https://dl.darkn.bio/BadRecovery), if it's missing, good luck, use CRSH2TTY or [build BadRecovery yourself](https://github.com/BinBashBanana/badrecovery).
5. Open your "Downloads" folder in the "Files" app, double click on the BadRecovery zip file, and drag the BadRecovery bin file to your Downloads folder.
6. If you are using Linux, skip to step 8, otherwise open a Chrome tab, click on the puzzle icon in the top right, and click on "Chromebook Recovery Utility".

<img src="/img/tutorial/chrome-recovery-extension.png">
7. Click on the ⚙ (settings) icon in the corner and click "Use local image" and the select your BadRecovery bin file.
<img src="/img/tutorial/cru-local-image.png">

8. If you don't use Linux skip to step 9, otherwise, open a terminal and run `lsblk` and verify what your USB drive is, once you have verified, run `cd ~/Downloads; sudo dd if=<badrecovery file> of=/dev/sd<usb letter> oflag=direct status=progress bs=16M` and wait. Skip to step 10.
9. Plug in the USB drive that you want to use for BadRecovery, do ***NOT*** use the USB drive with your data if you backed up data to a USB drive.
10. Verify this USB drive doesn't have important data and then wait for it to flash.
11. Once finished, press `esc+⟳+⏻ ` (`esc+refresh+power`). ONLY IF the image you downloaded has "`dev-only`" in the file name, press `ctrl+d` and then `esc+⟳+⏻ ` (`esc+refresh+power`) again and insert the USB, otherwise just insert the USB normally. You should now be waiting for your Chromebook to recover, wait for it to recover.
12. Once it recovers, you should now be at a weird looking hacker screen that says BadRecovery, just enter developer mode by pressing `esc+⟳+⏻ ` (`esc+refresh+power`) and then `ctrl+d` and `enter`, and then press `ctrl+d` whenever you see a developer mode/OS verification warning.
<img src="/img/tutorial/badrecovery.jpg" width="400">

13. Congrats! Now you can set up ChromeOS with a personal Google account and use [Full ROM](/readme.md#method-1-best-method-fullrom) or [AltFw](/readme.md#method-2-easiest-method-altfw--rw_legacy)!
<img src="/img/tutorial/craaskbowl-unroll-google.png" width="400">

## UNRELEASED!!: ChromeOS v130 and below - icarus
I do not have permission to give out information about icarus.

1. use a proxy or shimboot or crsh2tty or wait until around janurary 1st, 2025

## CRSH2TTY: every single release ever (tested v31 to v128)
CRSH2TTY is a very funny exploit. It's a cool universal USB-less exploit that should not even work at all yet it has been tested on many devices, including new ones like `nissa craaskbowl` or `dedede boten` to extremely old ones like `peppy` or `clapper`. No one is exactly sure how this works, but it requires two 2-second waits and then one 15-hour wait to work.

1. Powerwash using `ctrl+shift+q+q` and then `ctrl+alt+shift+r`. If this doesn't work, press `esc+⟳+⏻ ` (`esc+refresh+power`) and then `ctrl+d`, and then `enter`.
2. Proceed through ChromeOS setup as normal.
3. When it starts to enroll, wait 2 seconds then restart by preforming an EC reset by pressing `⟳+⏻ ` (`refresh+power`).
4. When it starts to enroll again, wait 2 seconds and press the recovery shortcut, `esc+⟳+⏻ ` (`esc+refresh+power`) then `⏻ ` (`power`) to turn it off.
5. Leave it off for ***15 hours*** or more.
6. Once 15 hours is up, turn on the Chromebook. You should be greeted at the `Welcome to your Chromebook` screen, you should already be connected to Wi-Fi, so press `Get started`.
7. On the `Get connected` screen, just press `Next`, you should see `Getting your device ready`, wait on this screen, and then you should see `Choose your Chromebook's setup`. 
9. Hooray!!!
<img src="/img/tutorial/craaskbowl-unroll-google.png" width="400">

# Kernver (kv) to ChromeOS (crOS) table
Please note this can be inaccurate because kernver skipping (aka kernskip) is really common. For example, I own an `octopus phaser360` Chromebook with kernver 1 but on ChromeOS v126 (v126 is kernver 4), and many people got ChromeOS v113 on kernver 1 (v113 is kernver 2).
In the event of a kernskip, you should downgrade to the versions connected to your kernver to be allowed access to more exploits.

| Kernver   | ChromeOS version            | Unenroll method |
|-----------|-----------------------------|---------------|
| 0<sup>1</sup> | any up to v111<sup>3</sup> | SHroot (to v101) or SH1mmer (to v110) |
| 1 | any up to v111<sup>3</sup> | SHroot (to v101) or SH1mmer (to v110) |
| 2<sup>2</sup> | v112 to v119<sup>4</sup>| Cryptosmite (to v118) |
| 3 | v120 to v125<sup>5</sup> | BadRecovery |
| 4 | v126 to v129 | icarus |
| 5 | v130+ | CRSH2TTY |

<sub><sup>Kv0 is usually a factory setting bug<sup>1</sup></sup></sub> \
<sub><sup>On some devices, kv2 is actually crOS v111<sup>2</sup></sup></sub> \
<sub><sup>v110 or lower recommended<sup>3</sup></sup></sub> \
<sub><sup>v118 or lower recommended<sup>4</sup></sup></sub> \
<sub><sup>Some early versions of v120 is kv2, however newer versions are kv3<sup>5</sup></sup></sub> \
<sub><sup>Some early versions of v125 is kv3, however newer versions are kv4<sup>5</sup></sup></sub> \
<sub><sup>v124 or lower recommended<sup>5</sup></sup></sub>
