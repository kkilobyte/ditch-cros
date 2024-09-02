# Unenrollment for Chrome OS Devices
Useful for ditching ChromeOS and using Full ROM, AltFw, or RW_Legacy methods.
Remember! You can always use the Shim method for Linux without unenrollment!

## Why?
Every method except the Shim method requires FWMP to be missing as Developer Mode is required, but FWMP blocks Developer Mode. Thus we need to remove FWMP. 

## What Kernver and ChromeOS version do I have?
To verify your kernver and your ChromeOS version, you need to first boot ChromeOS and then press `alt+v`, you will find a number followed by other numbers, only the first 2 or 3 numbers matter, such as `94`, `110` or `127`. Take note of this number and find the method related. If it is `120` or higher, you should check your kernver. Press `esc+⟳+⏻ `, and then `tab`. 

On `oldui` boards (with a white background, such as `snappy` or `octopus`), you just scroll down with your eyes until you find `tpm_ver`, and then look to the right of that to find `kernver`, and your kernver will be the last number to the right of kernver, this means `kernver=0x00010004` is kernver 4 or kv4.

On `newui` boards like `nissa` or `dedede`, you have to use the `🠟` key to scroll down to the bottom where you should find kernver

# How?
## ChromeOS v101 and below - Crosh Root Escalation
1. Login to your Chromebook.
2. Open Crosh with `ctrl+alt+t`. If it says `crosh is blocked`, use SH1mmer.
3. Paste the following in:

`set_cellular_ppp \';dbus-send${IFS}--system${IFS}--print-reply${IFS}--dest=org.chromium.SessionManager${IFS}/org/chromium/SessionManager${IFS}org.chromium.SessionManagerInterface.ClearForcedReEnrollmentVpd;exit;\'`

5. Press enter.
6. Back up all data to an external media (like a USB flash drive) or a cloud service (like Google Drive).
7. Press `esc+⟳+⏻ ` (`esc+refresh+power`).
8. Press `ctrl+d` and then `enter`.
9. On the scary screen with black text at the top left, press `enter` again.
10. Wait for ChromeOS to boot, and then go through the setup.
11. It should ask you to sign in with a personal account.
12. Enjoy!

# This guide below is UNFINISHED!!!

## ChromeOS v110 and below - SH1mmer
The preferred unenrollment method for ChromeOS v110 and below is using SH1mmer's very cool "deprovision" option. This takes ownership of the TPM and erases the FWMP, along with making ChromeOS not check for enrollment by putting a parameter in the RW portion of the VPD.

1. Back up all data to external media or cloud service.
2. If you are using ChromeOS, MacOS, or Windows, download [this extension](https://chromewebstore.google.com/detail/chromebook-recovery-utili/pocpnlppkickgojjlmhdmidojbmbodfm). (Linux won't work with this.) If you only have the Chromebook and this is blocked, try using [Skiovox](https://skiovox.com/skiovox.pdf). If you are using a version where Skiovox is patched, you can't use SH1mmer anyways.
3. [Identify](/device-identify.md) what Chromebook *board* you have.
4. Find your *board* [here](https://dl.darkn.bio/SH1mmer/Prebuilt/Legacy), if it's missing, good luck, use OlyBmmer.
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

13. Press `d` and then `enter`, this should come with two messages both having "SUCCESS!". Once it says "FINISHED", press `⟳+⏻ ` (refresh+power) and you should be greeted at a "OS Verification is off" screen but with no black text in the corner. Press `ctrl+d` whenever you Chromebook turns on and you see this screen. Now you can set up ChromeOS with a personal Google account and use [Full ROM](https://github.com/kkilobyte/ditch-cros/blob/main/readme.md#method-1-best-method-fullrom) or [AltFw](https://github.com/kkilobyte/ditch-cros/blob/main/readme.md#method-2-easiest-method-altfw--rw_legacy)!

## ChromeOS v118 and below - CryptoSmite
The preferred unenrollment method for ChromeOS v118 and below is using SH1mmer's not-as-cool "CryptoSmite" option. This writes a corrupted cryptohome to your data partition, or "stateful", using some random Google account, but this removes FWMP, so you can easily go into Developer Mode with no restrictions.

1. cryptosmite steps here (flash > boot > press p > cryptosmite > connect wifi > enable devmode)

## UNRELEASED!!: ChromeOS v124 and below - OlyBmmer
The preferred unenrollment method for ChromeOS v124 and below is using OlyBmmer. I do not have information about OlyBmmer other than it does *not* require an RMA shim unlike the other unenrollment exploits.

1. olybmmer steps here

## UNRELEASED!!: ChromeOS v130 and below - icarus
I do not have permission to give out information about icarus.

1. icarus steps here

# Kernver Info

## Kernver 0 and 1
These versions are basically the same. You have full access to any ChromeOS version (unless you update your kernver). If you are on kernver 1 but on ChromeOS v119 and above, you can downgrade to ChromeOS v105 to use SH1mmer deprovision, if you are on ChromeOS v118 or below, just use CryptoSmite, it's already included in SH1mmer payloads.

## Kernver 2
You have full access to ChromeOS v112 and above, if you are on ChromeOS v119 or above, you can downgrade to ChromeOS v112 to use Cryptosmite.

## Kernver 3
There is nothing you can do except wait for OlyBmmer release. If you are on ChromeOS v125 or above, you can downgrade to ChromeOS v120 and then use [caub](https://caub.glitch.me), if that site is blocked you can download the HTML at [bypassiwastaken/tinies](https://github.com/bypassiwastaken/tinies).

## Kernver 4
There is nothing you can do except wait for icarus release or cry. On newui boards like `dedede` or `nissa`, most devices with kv4 will have their *shim keys rolled*, meaning old shims will no longer work, and the new shims with the new keys have rootfs verification, meaning there will never be a shim-based unenrollment or Linux enviroment again unless we find new shims and find a way to get around verification. 
