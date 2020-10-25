# !!!!WIP!!!
# NOT 100% GUARANTEED TO WORK WITH BIG SUR SINCE I DO NOT HAVE THIS HARDWARE ANYMORE, PLEASE TEST ON YOUR OWN HARDWARE!!!
# ONLY FOR EXPERTS/PEOPLE THAT KNOW WHAT THEY'RE DOING!!! ONLY USE THIS AS A BASE FOR YOUR OWN CONFIGURATION!!!
# Asrock X99 Extreme3 Hackintosh Config using the OpenCore Bootloader
The OpenCore configuration in this Repo is mostly done, there's only a few things you *should* change before you can use this for your hackintosh endeavors. I have mostly followed the Dortania Guide for this but there are two exceptions I found out after researching for a while.
If you are just here for the PCI Initialization patch I have left a plist in the repository root so you can just copy it over to your existing plist (no clue if this patch is still needed or even works for Big Sur).

## What's already setup and mostly done?
* [Audio](https://dortania.github.io/OpenCore-Post-Install/universal/audio.html#finding-your-layout-id)
* [FileVault](https://dortania.github.io/OpenCore-Post-Install/universal/security.html#filevault)
* [Boot GUI](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html)
* Fixed RTC for UEFI Revision 3.70 (SSDT-RTC0-Range.aml)
  * Cannot guarantee it will work for any other Revision since the RTC Registers are usually different with each and every UEFI Release
* Sleep should work once you do the required additions I will mention in the next section

## What will I have to setup?
* [Platform Info](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#generate-a-new-serial) and the [ROM](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-rom)
* ~~[Complete the Emulated NVRAM Setup](https://dortania.github.io/OpenCore-Post-Install/misc/nvram.html#enabling-emulated-nvram-with-a-nvram-plist)~~
  *  After a bit of trial I have concluded that Nvram works on FW Ver. 3.70, so you can skip this step
* If you are using a Haswell-E/EP CPU change the Fake CPU ID to what is mentioned in the Dortania [Haswell-E Guide](https://dortania.github.io/OpenCore-Install-Guide/config-HEDT/haswell-e.html#kernel) (If you are using a Broadwell-E/EP CPU you don't need to touch anything)
* If you want to boot without an USB you should follow [this](https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html#grabbing-opencore-off-the-usb) guide too
* USB Mapping (more about this in the next Section)
* And any other issue you may encounter such as: [Internal NVMe Drive detected as external](https://www.reddit.com/r/hackintosh/comments/f0cc4t/internal_drives_shown_as_external_opencore_amd/) or other NVMe issues like proper power management (NVMeFix.kext is already included, just enable it)

## How can I setup the USB Map for my System?
Please follow the [Dortania USB Mapping Guide](https://dortania.github.io/OpenCore-Post-Install/usb/)

## What steps differ from the Dortania Haswell-E/Broadwell-E guide?
DevirtualiseMmio was disabled to get the system to boot and a custom kernel patch I have discovered after some research was added to get past the PCI initialization point on Catalina, however I do not know if this patch is still required on Big Sur so please conduct testing on your own to see if it is still needed.

## If you find any mistakes or want to add any improvements to this guide feel free to create an issue or open a pull request.

## Thanks to:
* The [OpenCore developers](https://github.com/acidanthera/)
* [CorpNewt](https://github.com/corpnewt)
* The [/r/Hackintosh Paradise Discord](https://discord.gg/5B58UbG)
* [This reddit comment](https://www.reddit.com/r/hackintosh/comments/fomna7/x99_upgrade_to_catalina_10154_successfully_but/fm2w62k/)
