#### MBR2GPT - Transfer of MBR partition disk to GPT partition so UEFI boot is enabled for CUCKOO installation

###### I recommend reading all parts of this repository before intsallation attempt. Will save lots of time.

Due to problems with NVIDIA gpu's, linux, dual boot with Windows 10, I decided that it's time to switch MBR partitions of my disk to GPT. But how to do it when time is precious and loss of data would result in lengthy process of restoration from old disks and many programs would have to be reinstalled nevertheless?

#### Worked on "MSI B450 Gaming PRO Carbon AC" motherboard
#### MBR on Samsung 970 EVO Plus 1TB
How could i have MBR and UEFI + Legacy BIOS in the first place? Good question. Thing is that Samsung Migration tool is great and can copy your data with everything on your new Samsung SSD even when your PC is turned on and you are logged in your OS that you want to copy. Usually I had to do this copy from Live USB and disk to disk. So that's how I ended up with MBR partition. I was not doing a clean Windows install on fresh UEFI Bios.

* Open up your Windows 10, login to your admin account
* [WinButton] search for "diskmgmt.exe"
* Create circa 1 GB of free unallocated space to your SSD, iow: shrink your SSD a bit
* Create circa 120 GB of space on different disk (Ubuntu will be there)
* Fire up terminal cmd.exe with admin privileges and enter in this command

```
MBR2GPT /convert /allowFullOS
```

* TURN OFF PC (no hibernation, fast startup or different bs turned on)
* TURN ON PC, press DELL button many times untill you are in BIOS
* Change your boot mode from UEFI+LEGACY to UEFI
* Make sure that UEFI HDD (its ssd dont worry) is top 1 priority disk
* Find tab in Advanced, Windows Boot, where is an option Windows 10 WHQL
* Set Windows 10 WHQL to **ON** (don't ask, just do :-)
* Invisible secure boot will appear
* Turn it off
* Turn on virtualization in BIOS (its hidden somewhere and defaultly turned off on AMD CPUs) 


**Insert Live USB with ubuntu, make it the boot priority, install Ubuntu on the free space with ext4 format, that was created in Windows [!! FOLLOW [GTX 1660 Super](https://github.com/cergina/Pain-Discovered-Cuckoo-Installation/blob/main/GTX1660S_install_guide.md) or [GTX 660](https://github.com/cergina/Pain-Discovered-Cuckoo-Installation/blob/main/GTX660_install_guide.md) !!] in this repo. I recommend 660. After installation is complete,  dont forget to change BIOS Boot priority.** 

**One more warning: It's very likely you will have to find also BOOT sections priority in your BIOS (not only HDD/SSD devices). It will look like**

(ubuntu) Samsung 970 EVO Plus 1TB
(Windows Boot Manager) Samsung 970 EVO Plus 1TB

This way you are guaranteed that GRUB runs and that you can choose between Windows and Ubuntu.
**Enjoy functional transfer from MBR to GPT without loss of data**

I'd like to thank the creator of https://dillinger.io/ for the ability to live edit markdown. :-)

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [cuckoo_od]: <https://cuckoo.readthedocs.io/en/latest/installation/>
   [git_readme]: <https://github.com/cergina/Pain-Discovered-Cuckoo-Installation/blob/main/README.md>
   