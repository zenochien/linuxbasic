---
title : "Storage in Linux"
date : "`r Sys.Date()`"
weight : 8
chapter : false
pre : " <b> 2.8 </b> "
---
![Createacloud](/images/2-Prerequiste/8/1.png)

### Introduction to Storage Basic
**List all Block devices**
- Block devices are special files that refer to or represent a device (which could be anything from a hard drive to a USB drive). So naturally, there are command line tools that help you with your block devices-related work.

- Major Number is used to identigy the type of block device, value 8 represent a SCSI device starts with SD.
![Createacloud](/images/2-Prerequiste/8/2.png)

1. Minor Number is uset to distuinguish individual, physical or logical devices.

```
$ lsblk 
```
```
$ ls -l /dev/ | grep "^b"
```
2. To Print,Create and Delete the parition table use fdisk -l command
![Createacloud](/images/2-Prerequiste/8/3.png)

```
$ sudo fdisk -l /dev/sda
```

### PARTITION TYPES – PRIMARY, EXTENDED AND LOGICAL

3. Createting Partitions

```
$ gdisk /dev/sdb
GPT fdisk (gdisk) version 1.0.1

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present
Found valid GPT with protective MBR; using GPT.

Command (? for help): ?
b back up GPT data to a file
c change a partition's name
d delete a partition
i show detailed information on a partition
l list known partition types
n add a new partition
o create a new empty GUID partition table (GPT)
p print the partition table
q quit without saving changes
r recovery and transformation options (experts only)
s sort partitions
t change a partition's type code
v verify disk
w write table to disk and exit
x extra functionality (experts only)
? print this menu

Command (? for help): n
Partition number (1-128, default 1): 1
First sector (34-41943006, default = 2048) or {+-}size{KMGTP}: 2048
Information: Moved requested sector from 34 to 2048 in
order to align on 2048-sector boundaries.
Use 'l' on the experts' menu to adjust alignment
Last sector (2048-41943006, default = 41943006) or {+-}size{KMGTP}: 41943006
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300):
Changed type of partition to 'Linux filesystem'
Command (? for help): w
Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!
Do you want to proceed? (Y/N): Y
OK; writing new GUID partition table (GPT) to /dev/vdb.
The operation has completed successfully.
```

```
$ sudo fdisk -l /dev/sdb
Disk /dev/sdb: 20 GiB, 128035676160 bytes, 250069680 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 7CABF26E-9723-4406-ZEA1-C2B9B6270A23
Device Start End Sectors Size Type
/dev/sdb1 2048 41943006 204800 20GB Linux filesystem
```

### Working with Ext4
![Createacloud](/images/2-Prerequiste/8/4.png)

4. To create a file system we will make use of /dev/sdb disk, run below command

```
$ mkfs.ext4 /dev/sdb1
```

5. Now create a directory to mount the filesystem use below commands

```
$ mkdir /mnt/ext4;

$ mount /dev/sdb1 /mnt/ext4
```

6. To verify if the filesystem is mounted use

```
$ mount | grep /dev/sdb1

$ df -hP | grep /dev/sdb1
```

### NFS 
![Createacloud](/images/2-Prerequiste/8/5.png)

7. NFS server maintains an export configuration file at /etc/exports that defines the clients which should be able to access the directories on the server. /etc/exports looks like this
![Createacloud](/images/2-Prerequiste/8/6.png)

```
$ /etc/exports
/software/repos 10.61.35.201 10.61.35.202 10.61.35.203
```

8. To exports all the mounts defined in /etc/exports use
![Createacloud](/images/2-Prerequiste/8/7.png)

```
$ exportfs -a
```
```
$ exportfs -o 10.61.35.201:/software/repos
```

### Working with Logical Volume Manager
9. To make use of LVM, install the package LVM .
![Createacloud](/images/2-Prerequiste/8/8.png)

```
$ apt-get install lvm2
```

10. Use pvcreate command to create a Physical Volume.

```
$ pvcreate /dev/sdb
Physical volume "/dev/sdb" successfully created
```

11. Use vgcreate command to create a Volume Group.

```
$ vgcreate caleston_vg /dev/sdb
Volume group "caleston_vg" successfully created
```

12. Use pvdisplay command to list all the PVs their names, size and the Volume group it is part of.

```
$ pvdisplay
--- Physical volume ---
  PV Name /dev/sdb
  VG Name caleston_vg
  PV Size 20.00 GiB / not usable 3.00 MiB
  Allocatable yes
  PE Size 4.00 MiB
  Total PE 5119
  Free PE 5119
  Allocated PE 0
  PV UUID iDCXIN-En2h-5ilJ-Yjqv-GcsR-gDfV-zaf66E
```

13. Use `vgdisplay` to see more details of the VG.
![Createacloud](/images/2-Prerequiste/8/9.png)

```
$ vgdisplay
--- Volume group ---
  VG Name caleston_vg
  System ID
  Format lvm2
  Metadata Areas 1
  Metadata Sequence No 1
  VG Access read/write
  VG Status resizable
  MAX LV 0
  Cur LV 0
  Open LV 0
  Max PV 0
  Cur PV 1
  Act PV 1
  VG Size 20.00 GiB
  PE Size 4.00 MiB
  Total PE 5119
  Alloc PE / Size 0 / 0
  Free PE / Size 5119 / 20.00 GiB
  VG UUID VzmIAn-9cEl5bA-lVtm-wHKX-KQaObR
```

14. To create the Logical Volumes, you can use lvcreate command

```
$ lvcreate –L 1G –n vol1 caleston_vg
Logical volume "vol1" created.
```

15. To display the Logical Volumes, you can use lvdisplay command

```
$ lvdisplay
--- Logical volume ---
  LV Path /dev/caleston_vg/vol1
  LV Name vol1
  VG Name caleston_vg
  LV UUID LueYC3-VWpE31-UaYk-wjIR-FjAOyL
  LV Write Access read/write
  LV Creation host, time master, 2020-03-31 06:26:14
  LV Status available
  # open 0
  LV Size 1.00 GiB
  Current LE 256
  Segments 1
  Allocation inherit
  Read ahead sectors auto
  - currently set to 256
  Block device 252:0
```

16. To list the volume, you can use lvs command

```
$ lvs
 LV VG Attr LSize Pool
 vol1 caleston_vg -wi-a----- 1.00g
```

17. Now to create an filesystem you can use mkfs command

```
$ mkfs.ext4 /dev/caleston_vg/vol1
```

18. To mount the filesystem use mount command

```
$ mount –t ext4 /dev/caleston_vg/vol1 /mnt/vol1
```

19. Now logical volume is now available for use. Lets resize the filesystem on vol1 while it is mounted. Check the free space available.

```
$ vgs
VG #PV #LV #SN Attr VSize VFree
caleston_vg 1 1 0 wz--n- 20.00g 19.00g
```
```
$ lvresize -L +1G -n /dev/caleston_vg/vol1
Logical volume vol1 successfully resized.
```
```
$ df –hP /mnt/vol1
Filesystem Size Used Avail Use% Mounted on
/dev/mapper/caleston_vg-vol1 976M 1.3M 908M 1% /mnt/vol1
```

20. Now to resize the file system use resize2fs command.

```
$ resize2fs /dev/caleston_vg/vol1
resize2fs 1.42.13 (17-May-2015)
Filesystem at /dev/mapper/caleston_vg-vol1 is mounted on
/mnt/vol1; on-line resizing required
old_desc_blocks = 1, new_desc_blocks = 1
The filesystem on //dev/mapper/caleston_vg-vol1 is now 524288
(4k) blocks long.
```

21. Now run df -hp command to verify the size of the mounted filesystem

```
$ df –hP /mnt/vol1
Filesystem Size Used Avail Use% Mounted on
/dev/mapper/caleston_vg-vol1 2.0G 1.6M 1.9G 1% /mnt/vol1
```
