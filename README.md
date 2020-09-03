# Asrock X99 Extreme3 Opencore 0.6.0
The OpenCore configuration in this Repo is mostly done, there's only a few things *you should change* before you can use this for your hackintosh endeavors. I have mostly followed the Dortania Guide for this but there are two exceptions I found out after researching for a while. This was only tested with macOS Catalina 10.15.6, Big Sur updates may follow once it officially releases.

## What's already setup and mostly done?
* [Audio](https://dortania.github.io/OpenCore-Post-Install/universal/audio.html#finding-your-layout-id)
* [FileVault](https://dortania.github.io/OpenCore-Post-Install/universal/security.html#filevault)
* [Boot GUI](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html)
* Fixed RTC for UEFI Revision P3.70 (SSDT-RTC0-Range.aml)
  * Cannot guarantee it will work for any older Revision (or newer if they ever release one) since the RTC Registers are usually different with each and every UEFI Release
* Sleep should work once you do the required additions I will mention in the next section

## What will I have to setup?
* [Platform Info](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#generate-a-new-serial) and the [ROM](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-rom)
* [Complete the Emulated NVRAM Setup](https://dortania.github.io/OpenCore-Post-Install/misc/nvram.html#enabling-emulated-nvram-with-a-nvram-plist)
* If you are using a Haswell-E/EP CPU change the Fake CPU ID to what is mentioned in the Dortania [Haswell-E Guide](https://dortania.github.io/OpenCore-Install-Guide/config-HEDT/haswell-e.html#kernel) (If you are using a Broadwell-E/EP CPU you don't need to touch anything)
* If you want to boot without an USB you should follow [this](https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html#grabbing-opencore-off-the-usb) guide too
* USB Mapping (more about this in the next Section)
* And any other issue you may encounter such as: [Internal NVMe Drive detected as external](https://www.reddit.com/r/hackintosh/comments/f0cc4t/internal_drives_shown_as_external_opencore_amd/)

## How can I setup the USB Map for my System?
If you are lazy and have the same amount of front USB ports (2) as me, you can use use my USBMap.kext I placed in the root directory of this repository, place it in your kext folder and then just enable the USBMap entry in the plist (you only have make you own USBMap.kext if you have a different amount of front USB ports).

First you'll need to grab [Corpnewt's USBMap Utility](https://github.com/corpnewt/USBMap) and then rename your existing *config.plist* to something like *backup.plist* and then rename the included *usbdebug.plist* again to *config.plist*. This .plist includes some patches that remove the 15 USB port restriction **for macOS Catalina only**. Note that these shouldn't be used daily if you are too lazy to map out your USB ports since no one really knows what side effects (possible data corruption and system instability) they bring into light. After you rebooted with the new .plist open the USBMap Utility and press D. It'll bring you into Discover USB port function. Now take an USB drive and plug it in one port at a time once the tool visibly refreshes. When you're done and have all your USB ports mapped in the tool press Q once. Now press P so we can continue to the .kext creation. Look if everything seems alright (a single USB Controller shouldn't have over 16 ports) and then press K to build your kext. Now you can close the application. Take the USBMap.kext it created in the Results folder and move it to the kext folder. Now change your .plists again (rename current config.plist to anything else.plist and rename the backup.plist you renamed previously back to config.plist. Now edit the latter with [ProperTree](https://github.com/corpnewt/ProperTree) or any other editor you prefer and enable the USBMap.kext entry I have already created. *Now you're done.*

## What steps differ from the Dortania Haswell-E/Broadwell-E guide?
DevirtualiseMmio was disabled to get the system to boot and a custom kernel patch I have discovered after some research was added to get past the PCI initialization point.

## If you find any mistakes or want to add any improvements to this guide feel free to create an issue or open a pull request.

## Thanks to:
* [The OpenCore team](https://github.com/acidanthera/) for creating OpenCore
* [CorpNewt](https://github.com/corpnewt) and his utilities that make creating Hackintosh Configs in general far easier than previously.
* The [/r/Hackintosh Paradise Discord server](https://discord.gg/5B58UbG) for providing support on some issues I experience while creating this config.
* [This](https://www.reddit.com/r/hackintosh/comments/fomna7/x99_upgrade_to_catalina_10154_successfully_but/fm2w62k/) reddit comment helping me figure out the PCI Initialization error
