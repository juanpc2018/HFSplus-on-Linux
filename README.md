# HFSplus-on-Linux

Linux Free HFSplus driver is limited to 2TB, No Journal, No Raname Volumes, etc... </br>
HDD formated in Linux with HFSplus are called "untitled" </br>
if you have multiple drives/partitions when mounted are called: "untitled1", 2, 3, etc..., </br>
Requires Real OSX 10.6 or Newer to rename HFSplus HHDs, Drives or Partitions. </br>
HFS+ Journaled can be Read in Linux, No Write, upto 2TB. </br>
HFSplus No-Journaled can be RW in Linux, upto 2TB. </br>

there are alternatives like: paid Linux drivers from Paragon: </br> 
https://www.paragon-software.com/home/apfs-linux/ </br>
https://www.paragon-software.com/home/ntfs-linux-professional/ </br>

## Why HFSplus? 

people that need to move files from Windows to OSX to Linux, </br>
in an office or workplace, </br>
have a hard time doing it. </br>
Windows & OSX can Read & Write ExFAT, </br>
but ExFAT is Not the best file system. </br>
has many problems with long file names, or file names with special characters, </br>
if you save a webpage, and move it, it becomes a nightmare. </br>
most of the times requires compression and decompression, </br>
but if you need to move too much files, </br>
it becomes 2x nightmares. </br>
a quest searching the best Trifecta FS driver, for: </br>
Win, Mac, Linux. </br>
ExFAT is discarded, FAT32 worse, NTFS same, </br>
Linux Free APFS driver is super bad </br>
Linux HFSplus is an option, but has some issues. </br>

Workaround: </br>
have 3 machines, using 10Gbps SFP+ Network, SFP+ 10G Router limited to 1200MB/s. </br>
Paragon Universal driver is more cost effective, No speed limit, less energy consumption. </br>
when HDD is offline, driver is better. </br>
3 machines is too much energy, $, 3x keyboards, 3x screens, 3x mouse, etc.. </br>
ebven using VNC is still too much HW just to move files ,</br>
Making Backups between Trifecta becomes a Nightmare. </br>

Paragon UAPFS Universal-APFS driver, works up to Kernel 5.19 </br>
Newer Kernel support is in development. </br>
current limitations like: No Format HDD with APFS. </br>
to format APFS requires Real OSX HighSierra 10.13.x or Newer, OSX Catalina 10.15.7 </br>
OSX Catalina is the last macOS 100% amd64 "intel", No 32-Bit </br>
OSX HighSierra is the last macOS 32 & 64-Bit intel, </br>
OSX Mohave 10.14.6 does Not load 32-Bit drivers. </br>
Newer OSX are Hybrid Kernel, intel machines Run Emulated "slower -30%". </br>
OSX BigSur 11, Monterey 12, Ventura 13, Sonnoma 14, Not recommended with Intel machines. </br>

when Apple drop/delete support for old machines every 6 years, in newer OSX, </br>
most people install Linux or force installing Newer OSX, </br>
OSX is required if you have a specific Harware, with closed source drivers, </br>
like Matrox MXO2, Avid HDX, imacon scsi scanner, etc... </br>

some Apple owners try to install New OSX, but its poinless, machine becomes slower. </br>
Linux makes machine faster. </br>
https://en.wikipedia.org/wiki/Usage_share_of_operating_systems#Desktop_and_laptop_computers </br>
NTFS is inferior, vs. HFS+, Ext4, XFS, APFS, ZFS, Btrfs, etc... </br>
but superior than ExFAT, FAT32, etc... </br>
can be Read in OSX, No write unless you buy/install NTFS driver for OSX, </br>
Apple Bootcamp drivers allow to Read/Write HFS+ in Windwows, haven tested over 2TB. </br>
XFS is best file system for large drives 18TB, but Linux Only, havent tested ZFS, APFS. </br>
Paragon has Read Only drivers for OSX and Windows. </br>
after much consideration, </br>
APFS is the best crossover file system today, </br>
R/W all Operating Systems, </br>
if paragon makes R/W XFS for Windows & OSX, </br>
XFS becomes the standar, </br>
APFS today is the best crossover option. </br>
like ExFAT but much better. </br>
2nd best option Paragon HFS+, 3rd option free HFSplus. </br>
For those reasons, Gparted should support Paragon Universal Drivers. </br>
to make easier for people to jump into Linux, from other OS. </br>

Gparted has a Gui version of: </br>
$ mount -t uapfs \ḑev\sd** \media\uapfs </br>
$ umount -t uapfs \ḑev\sd** \media\uapfs </br>
but does Not have -t uapfs </br>
and... </br>
[View][File System Support][Rescan] </br>
Not asking much, just small details ... </br>
Apple released HFS+ and APFS as Open Source, </br>
but Nobody has created a Good version for Linux, </br>
APFS is Open, search apple developer website. </br>
Paragon downloaded Apple source code, created a "working" but incomplete version, similar to FUSE https://osxfuse.github.io/ for Linux & Win. </br>
same with HFS+, someone downloaded the source code from Apple, created a Free version for Linux called HFSplus, incomplete. </br>
HFS+, APFS and FUSE are Open Source. </br>
https://github.com/libfuse/libfuse </br>
https://github.com/osxfuse/osxfuse/wiki/List-of-macFUSE-File-Systems </br>
https://github.com/sgan81/apfs-fuse </br>
Paragon has a Free Open Source Read Only version. </br>
https://github.com/Paragon-Software-Group/paragon_apfs_sdk_ce </br>

[APFS_user_manual.pdf](https://github.com/juanpc2018/HFSplus-on-Linux/files/13272392/APFS_user_manual.pdf)

----------

## What does No-Journaled really means?

it means that sometimes, when mounted, wont Write,  </br>
because it had an error previously, was Nto shutdown properly, power failure, Dolphin or Nautilus crash, Not enough memory, etc..  </br>
the sollution is very simple: </br>
do a file system check, unmounted, but Not removed... </br>

using gnome-disks or gparted, umount the drive,  </br>
but before umount, see what physical path it has, </br>
and mount again, Problem SOLVED. </br>
Journaled does that automatically, recording a log of all changes done, in a small portion of the HDD. </br>
No-Journaled wont allow to Write, unless you solve the problem manually. </br>

example: </br>
if its an external NVMe with an USN3.0 case,  </br>
$ sudo fsck.hfs -f /dev/nvme0n1p4 </br>
or standard HDD-USB </br>
$ sudo fsck.hfs -f /dev/sdc1 </br>

$ sudo mkdir untitled1 </br>
$ sudo mount -t hfsplus -o rw /dev/sdc1 /media/(whoami)/untitled1 </br>

the default mounting point is /mnt/untitled </br>
but /media/(whoami)/ is ok, but if you reboot the machine often a custom mounting point it becomes annoyin, </br>
unless you add to fstab configuration file.

$ cat /etc/fstab
