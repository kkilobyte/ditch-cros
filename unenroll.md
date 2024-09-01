# Unenrollment for Chrome OS Devices
Useful for ditching ChromeOS and using Full ROM, AltFw, or RW_Legacy methods.
Remember! You can always use the Shim method for Linux without unenrollment!

## Why?
Every method except the Shim method requires FWMP to be missing as Developer Mode is required, but FWMP blocks Developer Mode. Thus we need to remove FWMP. 

## What Kernver and ChromeOS version do I have?
To verify your kernver and your ChromeOS version, you need to first boot ChromeOS and then press `alt+v`, you will find a number followed by other numbers, only the first 2 or 3 numbers matter, such as `94`, `110` or `127`. Take note of this number and find the method related. If it is `120` or higher, you should check your kernver. Press `esc+⟳+⏻ `, and then `tab`. 

On `oldui` boards (with a white background, such as `snappy` or `octopus`), you just scroll down with your eyes until you find `tpm_ver`, and then look to the right of that to find `kernver`, and your kernver will be the last number to the right of kernver, this means `kernver=0x00010004` is kernver 4 or kv4.

On `newui` boards like `nissa` or `dedede`, you have to use the  key to scroll down to the bottom where you should find kernver

# How?

## ChromeOS v110 and below - SH1mmer
The preferred unenrollment method for ChromeOS v110 and below is using SH1mmmer's very cool "deprovision" option. This takes ownership of the TPM and erases the FWMP, along with making ChromeOS not check for enrollment by putting a parameter in the RW portion of the VPD.

1. sh1mmer steps here (flash > boot > press d > reboot)

## ChromeOS v118 and below - CryptoSmite
The preferred unenrollment method for ChromeOS v118 and below is using SH1mmer's not-as-cool "CryptoSmite" option. This writes a corrupted cryptohome to your data partition, or "stateful", using some random Google account, but this removes FWMP, so you can easily go into Developer Mode with no restrictions.

1. cryptosmite steps here (flash > boot > press p > cryptosmite > connect wifi > enable devmode)

## UNRELEASED!!: ChromeOS v124 and below - OlyBmmer
The preferred unenrollment method for ChromeOS v124 and below is using OlyBmmer. I do not have information about OlyBmmer other than it does *not* require an RMA shim unlike the other unenrollment exploits.

1. olybmmer steps here

## UNRELEASED!!: ChromeOS v130 and below - icarus
I do not have permission to give out information about icarus.

1. icarus steps here (flash > boot > _ > _ > _)

# Kernver Info

## Kernver 0 and 1
These versions are basically the same. You have full access to any ChromeOS version (unless you update your kernver). If you are on kv1 but are on ChromeOS v111, or v120 and above, you can downgrade to ChromeOS v105 to use SH1mmer deprovision, if you are on ChromeOS v118 or below, just use CryptoSmite, it's already included in SH1mmer payloads.

## Kernver 2
You have full access to ChromeOS v112 and above, if you are on ChromeOS v119 or above, you can downgrade to ChromeOS v112 to use Cryptosmite.

## Kernver 3
There is nothing you can do except wait for OlyBmmer release. If you are on ChromeOS v125 or above, you can downgrade to ChromeOS v120 and then use [caub](https://caub.glitch.me), if that site is blocked you can download the HTML at [bypassiwastaken/tinies](https://github.com/bypassiwastaken/tinies).

## Kernver 4
There is nothing you can do except wait for icarus release or cry. On newui boards like `dedede` or `nissa`, most devices with kv4 will have their *shim keys rolled*, meaning old shims will no longer work, and the new shims with the new keys have rootfs verification, meaning there will never be a shim-based unenrollment or Linux enviroment again unless we find new shims and find a way to get around verification. 