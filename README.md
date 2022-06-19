# Hackintosh EFI Information for Gigabyte H310M A 2.0 R1



**Tested macOS**

* Monterey 12.2 (21D49) with OpenCore .77 1/10/2022
* Using OpenCore Aux Tools to update to OpenCore .81 works flawlessly.  Use the attached EFI and immediately update to OC81; it works fine.  
* MacOS 12.4 works well.

**Hardware**

* Gigabyte H310M A 2.0 R1 (BIOS F5, 11/29/21)
* Intel i5-9400
* Radeon RX 570 4GB
* 16GB RAM
* 500GB SATA SSD

**Working**

* Bluetooth, Wi-Fi (Fenvi FV-T919) and ethernet (LOM, the Intel integrated chip)
* HDMI Audio, Motherboard Audio
* Sleep / Wake
* App Store
* Apple Watch unlock, AirDrop
* USB port mapping is complete, resulting in iPhone/iPads charging at 2100 ma, and Apple Watch at 1000 ma.  If yours (iPhone, iPad, Apple Watch) doesn't show this rate in About This Mac / System Report / USB, then your USB mapping may not be working correctly.  All 'A' USB ports on this motherboard, USB2 and USB3, are in use and 'active' (working).  USB-C port works, but is only lightly tested.

**Untested**

* Time Machine
* Handoff/Continuity and more advanced Bluetooth/wifi integrations

**Not Working**

* Sidecar (due to the use of iMacPro1,1 SMBIOS, this won’t work; can be fixed by flipping to iMac19,1 SMBIOS quite easily, but then AppleTV and other applications may not play as easily)

**BIOS Settings**

* OS type: Other types

**Disabled**

* Fast Boot
* Launch CSM
* Vt-d

**Enabled**

* Above 4G decoding

**Next Steps - Required**

You will need to do the following:

* Prepare a USB boot disk for 12.x installation.  The easiest way is on a real Mac, although gibMacOS may work for you as well.  To follow the much easier Real Mac path, read https://support.apple.com/en-us/HT201372 and follow the directions for Monterey, including the terminal command to write the download to the USB stick.
* Download EFIAgent (https://github.com/headkaze/EFI-Agent) and mount the EFI partition for the USB stick you just made.  Using EFIAgent again, "open" the EFI partition so it shows on the Mac desktop.  Note that EFI partitions are typically GRAY in color in EFIAgent.  To find EFIAgent, locate the new icon in the upper right clock area that looks like a circular pie.  ![Screen Shot 2021-09-25 at 7 22 44 PM](https://user-images.githubusercontent.com/4536776/134790066-27597b9e-a37f-47e0-87f5-d3ebbc2af59f.png)
 >>  Remember this process for any future EFI partitions you must mount; this is a common procedure.
* Copy the contents of the attached zipfile to the USB stick, so that your files look something like the picture.  [Picture temporarily removed; pls check later.]

* The EFI partition on the USB stick has an EFI folder in it, and inside of that folder, there are two subfolders, OC and Boot, each with files in them.  Make sure your EFI partition looks just like this once you've unzipped the zipfile.

Technically, you are now done.  You should be able to boot MacOS using the USB stick, and install MacOS onto your SSD.  That said, I suggest configuring it a bit *before* you boot into MacOS for the first time with the right serials and ROM info:

* Download OCAT https://github.com/ic005k/QtOpenCoreConfig and open it.  Read the tooltips showing what all the icons at the top do.  In the future, be sure to update to the latest OCAT version by finding the update button on the left side of the window and updating.  
* Open your USB stick's config.plist by using OCAT's OPEN icon.
* In OCAT, notice the row of icons on the left side.  Go to "PI" on the row.
* Let's generate a new serial.  Ensure, under the GENERIC tab, that for "SystemProductName" you have the iMacPro1,1.  Then click GENERATE right next to the iMacPro1,1 box.  Your serial numbers are now set up.

Now let's fix your MAC address (ROM)

* [Mac: This only works if you used the USB stick to install MacOS already; assumes MacOS is installed on this motherboard] Go to the Mac's terminal, type in "ifconfig", and find "en0:", your ethernet adapter.  Find the line "ether xx:xx:xx:xx:xx:xx" and write those numbers, without the :, into the ROM box.  
* [Using Windows, if Windows is installed on this motherboard] Go to Windows' commandline/powershell interface.  Type 'ipconfig /all' and find your ethernet adapter.  Find the line "Physical Address" with xx-xx-xx-xx-xx-xx letters to the right on that same line.  Key in those letters and numbers, without the -, in the ROM box.
* [The easy way; untested] Click GENERATE immediately to the right of the ROM box.
* Serialization and ROM setup is now complete.  Press the SAVE icon in OCAT and then quit OCAT.
* **Note**:  Read https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html prior to using any Apple services like Chat and iCloud.  These details will correctly confirm that your serial information is viable.  Until complete, do not use the iServices; do not log into any Apple cloud services.
* Your USB stick is ready to use to boot your Mac and install MacOS.  

**Final Steps**

* Assuming no other issues, your setup should now be complete.  Restart, press F12 at the Gigabyte screen so you can choose a boot disk, and boot from the USB stick (select the uEFI option if prompted).  You'll then be able to step through installation of MacOS.  Once setup is done, use EFIAgent to copy the USB stick's EFI folder, with your serial number modifications, to the SSD's EFI partition, and then you'll be able to boot from that disk (and you won't need the USB stick anymore, but keep it forever as a backup!). Do note:  Until you've copied the EFI folder from your USB stick to your SSD's EFI partition, you must continue to F12-boot into your USB stick before booting into MacOS.  Once you've copied the USB stick's EFI folder to the EFI partition on the SSD, then you'll no longer need to use the USB stick to boot.  
* Versioning on the zipfile is V101.  Future versions, if required, would have higher numbers so it is easier to see what version you have.  Keep the zipfile (name, at least) around so you know what version you have.  Note this has nothing to do with the versioning of your motherboard or OpenCore.
* You can clean up logs and logging / bootup, if you wish, once you have everything sorted.  Doritania's guide has a post-install cleanup section with good details on that.
* If the resulting USB stick won't boot, a quick first-order check is to use OCAT to update OpenCore (check the tooltips and icons at the top of the window) on your USB stick, allow OCAT to fix and update the config.plist (just click SAVE in OCAT once you've opened your config.plist), and then try booting again.  
* Otherwise, please leave comments/issues here.

**Updates**

* Using OCAT to update to OpenCore .81 (and associated kexts) works flawlessly.  

**Changelog**

* The changes in v1.01 is simply OpenCore .76.  You can do the same thing by updating to the latest OCAT, ensuring your config.plist is loaded in it, and then selecting Edit/Syncronize Main Program, then saving your configuration (pressing the floppy disk icon).  That updates to OpenCore vLatest and updates a few corresponding kexts like lilu and whatevergreen.  
