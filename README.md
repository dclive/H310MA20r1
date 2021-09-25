# OpenCore(0.7.4) configuration on Gigabyte H310M A 2.0 R1
Hackintosh EFI Information for Gigabyte H310M A 2.0 R1 


![AboutThisMac](https://user-images.githubusercontent.com/4536776/134783342-b85427cf-c6ff-4f68-b2ae-fa7fcd48840c.png)

**Tested macOS**

•	Big Sur 11.6 with OC73 and OC74 nightly 24/9/2021

**Hardware**

* Gigabyte H310M A 2.0 R1 BIOS F5a
* Intel i5 9400
* Radeon RX 570 4GB
* 16GB RAM
* 500GB SSD 
* EVGA PSU, NR200P Case 

**Working**

* Bluetooth, Wi-Fi and ethernet
* HDMI Audio
* Sleep / Wake
* App Store
* Apple Watch unlock, AirDrop
* USB port mapping is complete, resulting in iPhone/iPads charging at 2100mah, and Apple Watch at 1000 mah.  If yours (iPhone, iPad, Apple Watch) doesn't show at least this rate in About This Mac / System Report / USB, then your USB mapping isn't working correctly.  All USB ports on this motherboard, USB2 and USB3, are in use and 'active' (working).  

**Untested**

* Motherboard Audio
* Time Machine
* Handoff/Continuity and more advanced Bluetooth/wifi integrations

**Not Working**

* Sidecar (due to the use of iMacPro1,1 SMBIOS, this won’t work; can be fixed by flipping to iMac19,1 SMBIOS quite easily, but then AppleTV and other applications may not play as easily) 

**BIOS Settings**

* OS type: other types

**Disabled**

* Fast Boot
* Launch CSM
* Vt-d

**Enabled**

* Vt-x
* Above 4G decoding

**Next Steps - Required**

You will need to do the following: 
* Prepare a USB boot disk for Big Sur 11.6 installation.  The easiest way is on a real Mac, although gibMacOS may work for you as well.  To do so, read https://support.apple.com/en-us/HT201372 and follow the directions for Big Sur, including the terminal command to write the download to the USB stick.
* Download EFIAgent (https://github.com/headkaze/EFI-Agent) and mount the EFI partition for the USB stick you just made.  Using EFI Agent again, "open" the EFI partition so it shows on the Mac desktop.  To find EFIAgent, find the new icon in the upper right clock area.  
* Copy the contents of the attached zipfile to the USB stick, so that your files look something like the picture: 

![EFI Layout](https://user-images.githubusercontent.com/4536776/134783624-10b0c7ba-fb29-4cf1-8017-230d22f8e18b.png)

* The EFI partition on the USB stick has an EFI folder in it, and inside of that folder, there are two subfolders, OC and Boot, each with files in them.  Make sure your EFI partition looks just like this once you've unzipped the zipfile. 

Technically, you are now done.  You should be able to boot MacOS using the USB stick, and install MacOS onto your SSD.  That said, I usually suggest configuring it a bit *before* you boot into MacOS for the first time with the right serials and ROM info: 

* Download OCAT https://github.com/ic005k/QtOpenCoreConfig and open it.  Read the tooltips showing what all the icons at the top do.  Update to the latest OCAT version by finding the update button on the left side of the window and updating.  Don't continue until you've done this. 
* Open your USB stick's config.plist by using OCAT's OPEN icon.
* In OCAT, notice the row of icons on the left side.  Go to "PI" on the row. 
* Let's general a new serial for you.  Ensure, under the GENERIC tab, that for "SystemProductName" you have the iMacPro1,1.  Then click GENERATE right next to the iMacPro1,1 box.  Your serial numbers are now set up!
  
Now let's fix your MAC address (ROM) 

* [Mac: This only works if you used the USB stick to install MacOS already] Go to the Mac's terminal, type in "ifconfig", and find "en0:", your ethernet adapter.  Find the line "ether xx:xx:xx:xx:xx:xx" and write those numbers, without the :, into the ROM box.  
* [Using Windows, if Windows is installed on this motherboard] Go to Windows' commandline/powershell interface.  Type 'ipconfig /all' and find your ethernet adapter.  Find the line "Physical Address" with xx-xx-xx-xx-xx-xx letters to the right on that same line.  Key in those letters and numbers, without the -, in the ROM box. 
* [The easy way; untested] Click GENERATE immediately to the right of the ROM box. 
* Serialization and ROM setup is now complete.  Press the SAVE icon in OCAT and then quit OCAT. 
* Your USB stick is ready to use to boot your Mac and install MacOS.  

**Final Steps**

* Assuming no other issues, your setup should now be complete.  Restart, press F12 at the Gigabyte screen so you can choose a boot disk, and boot from the USB stick (select the uEFI option if prompted).  You'll then be able to step through installation of MacOS.  Once setup is done, use EFIAgent to copy the USB stick's EFI folder, with your serial number modifications, to the SSD's EFI partition, and then you'll be able to boot from that disk (and you won't need the USB stick anymore, but keep it forever as a backup!)


