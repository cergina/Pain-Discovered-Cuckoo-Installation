# Pain Discovered Cuckoo installation


This installation guide is aimed to help people, who dont want to struggle with Cuckoo sandbox install
and need (almost) straightforward guide as I woul'd be gratefull for when I wasted whole week with it.
Sadly, I realized cuckoo installation is not as simple as I thought and is very platform dependent, but
never ever in my wildest dreams I thought NVIDIA Turing Architecture could interfere. 

ps.: this is the first time i envy people with integrated gpus

##### Therefore I list my full HW relevant information, because it can be very important for you as well.
  - AMD Ryzen 5 2600
  - MSI B450 Gaming Pro Carbon AC { American Megatrends Inc. 1.60, 3/6/2019 } : BIOS
  - 2 x 8 GB DDR4 3000MHz CL16 (Dual-channel mode)
  - GTX 1660 Super (in one part of installation, unstable)
  - GTX 660 (in another part of installation, more stable)
  - 1TB Samsung 970 EVO Plus {929.42GB NTFS | 100 MB EFI | 2 GB Unallocated} : GPT        
  - 1TB WD Green 5400RPM {819.20GB NTFS | 512MB FAT32 | 110.85GB | 976MB } : MBR
  - DUAL BOOT w Windows 10 : UEFI

#### This readme points to other files within this repo
[GTX 1660 Super - install] - much much trouble (worked only once, didn't retest)
[GTX 660 - install] - this should work for everyone as I tested few times
[MBR2GPT - tutorial] - this is in case you have LEGACY or UEFI + LEGACY bios

### Some usefull links

Cuckoo sandbox is an usefull piece of SW, but some knowledge is required. Therefore I urge you to
study a few materials I linked here, that I believe have the most credibility or validity.

| MY VIDEO ABOUT THIS | LINK TO YOUTUBE |
| ------ | ------ |
| Cuckoo startup after reboot + example file scan | [my youtube][cuckoo_my_youtube] |

| Install guides | LINK WITHIN REPO |
| ------ | ------ |
| Cuckoo on GTX 1660 Super | [git/cergina/GTX1660S_install_guide.md][1660S_git_this] |
| Cuckoo on GTX 660 | [git/cergina/GTX660_install_guide.md][660_git_this] |
| Convert MBR2GPT | [git/cergina/mbr2gpt.md][mbr2gpt_git_this] |
| Ubuntu installation freeze | [git/mari-linhares/guide.md][ubuntufreeze_git_other] |

 * Just a reminder, that a pure follow of steps in either of those in links didn't work for me.

| BRIEF DESCRIPTION | LINK |
| ------ | ------ |
| Official documentation | [cuckoo.readthedocs][cuckoo_od] |
| Cuckoo Setup hatching | [hatching][cuckoo_hatch] |
| Cuckoo Setup part.1 | [youtube][cuckoo_notmine_youtube] |

##### Famous quote by Linus Torvalds I cannot dissagree with.

> ... and NVIDIA has been the single worst company
> we've ever dealt with, so NVIDIA Fuck You!

No, this is not my first troublesome installation with NVIDIA, I had NVIDIA Jetson TX2
for my bachelor's thesis, that was directly designed to work with Ubuntu 16.04 LTS and
even that was pain, that finally ended on warranty reclamation, which solved some problems
but the terrible instructions on their website were not up to date either.

### Help

Want to contribute or help? Great!
Test it yourself and confirm/dissent, write pull request, report bug or whatever

License
----

MIT


**Enjoy, i guess.**
I'd like to thank the creator of https://dillinger.io/ for the ability to live edit markdown. :-)

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [cuckoo_od]: <https://cuckoo.readthedocs.io/en/latest/installation/>
   [cuckoo_hatch]: <https://hatching.io/blog/cuckoo-sandbox-setup/>
   [cuckoo_notmine_youtube]: <https://www.youtube.com/watch?v=QlQS4gk_lFU>
   [cuckoo_my_youtube]: <https://youtu.be/nIhoUfK7oTY>

   [1660S_git_this]: <https://github.com/cergina/Pain-Discovered-Cuckoo-Installation/blob/main/GTX1660S_install_guide.md>
   [660_git_this]: <https://github.com/cergina/Pain-Discovered-Cuckoo-Installation/blob/main/GTX660_install_guide.md>
   [mbr2gpt_git_this]: <https://github.com/cergina/Pain-Discovered-Cuckoo-Installation/blob/main/MBR2GPT_guide.md>
   [ubuntufreeze_git_other]: <https://gist.github.com/mari-linhares/cef4cb3440408e44963d1447a7db5ae0>
