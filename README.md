# Asrock X99 Extreme3 Opencore 0.6.0
The OpenCore configuration in this Repo is mostly done, there's only a few things you *should* change before you can use this for your hackintosh endeavors. I have mostly followed the Dortania Guide for this but there are two exceptions I found out after researching for a while. This was only tested with macOS Catalina 10.15.6, Big Sur updates may follow once it officially releases.
If you are just here for the PCI Initialization patch I have left a plist in the repository root so you can just copy it over to your existing plist. 
(Friendly reminder that X99 is a horrible platform in general and that if you want a stable hack please buy something else, even AMD Ryzen was easier to setup that this)

## What's already setup and mostly done?
* [Audio](https://dortania.github.io/OpenCore-Post-Install/universal/audio.html#finding-your-layout-id)
* [FileVault](https://dortania.github.io/OpenCore-Post-Install/universal/security.html#filevault)
* [Boot GUI](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html)
* Fixed RTC for UEFI Revision 3.70 (SSDT-RTC0-Range.aml)
  * Cannot guarantee it will work for any older Revision (or newer if they ever release one) since the RTC Registers are usually different with each and every UEFI Release
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
If you are lazy and have the same amount of front USB 3.0 ports (2) as me, you can use use my USBMap.kext I placed in the root directory of this repository, extract it, place it in your kext folder and then enable the USBMap entry in the plist (you only have make you own USBMap.kext if you have a different amount of front USB ports).

First you'll need to grab [Corpnewt's USBMap Utility](https://github.com/corpnewt/USBMap) and then enable the USB Port Limit Remove patches in the .plist under Kernel>Patch (*These only work for Catalina*) and USBInjectAll.kext under Kernel>Add. Then go ahead and reboot. Now open up the USBMap utility and press D to discover all your USB ports. Now you need an USB 2.0 and 3.0 device. Proceed to plug each of those devices into every USB port and leave it there until the USBMap utility visibly refreshes. After you are done press Q to quit and then just press P to enter the .kext creation section and finally after that press K to build your USB map kext. (If it asks you to automatically it in your EFI folder just press N to dismiss it). Now go and move your finished USB map into your kext folder, disable the USB port limit kernel patches and USBInjectAll.kext and enable the entry for USBMap.kext I have added.

## What steps differ from the Dortania Haswell-E/Broadwell-E guide?
DevirtualiseMmio was disabled to get the system to boot and a custom kernel patch I have discovered after some research was added to get past the PCI initialization point.

## If you find any mistakes or want to add any improvements to this guide feel free to create an issue or open a pull request.

## Thanks to:
* [OpenCore devs](https://github.com/acidanthera/)
* [CorpNewt](https://github.com/corpnewt)
* The [/r/Hackintosh Paradise Discord server](https://discord.gg/5B58UbG)
* [This](https://www.reddit.com/r/hackintosh/comments/fomna7/x99_upgrade_to_catalina_10154_successfully_but/fm2w62k/) reddit comment
