# Create and Mount a New Partition
[ [ Intro ] ](README.md) -- [ [Add User](user.md) ] -- [ [**Create Partition**](harddrive.md) ] -- [ [Install & Run Daemon](daemon.md) ] -- [ [Optimization](optimization.md) ] -- [ [Monitoring](monitor.md) ]

-----
## Check Available Drives
- `$ sudo fdisk -l | grep sd`
```
Disk /dev/sda: 931.5 GiB, 1000204886016 bytes, 1953525168 sectors
```
You should see your hard drive listed on there. Here I'm using `/dev/sda`.YMMV.
## Create a Partition on the Drive
First, let's see all existing partitions on the drive.
- ```$ sudo fdisk /dev/sda```
```
Command (m for help): p
Disk /dev/sda1: 931.5 GiB, 1000137777152 bytes, 1953394096 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x486b65c4
```
Delete existing partition(s) as you wish.
`Command (m for help): d`

Then we create a new partition.
```
Command (m for help): n  
Partition type  
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p):
Using default response p.  
Partition number (1-4, default 1):  
First sector (2048-1953525167, default 2048):  
Last sector, +sectors or +size{K,M,G,T,P} (2048-1953525167, default 1953525167):
Created a new partition 1 of type 'Linux' and of size 931.5 GiB.
```
Finally we change the partition type.
```
Command (m for help): t  
Selected partition 1  
Partition type (type L to list all types): L

 0  Empty           24  NEC DOS         81  Minix / old Lin bf  Solaris
 1  FAT12           27  Hidden NTFS Win 82  Linux swap / So c1  DRDOS/sec (FAT-
 2  XENIX root      39  Plan 9          83  Linux           c4  DRDOS/sec (FAT-
 3  XENIX usr       3c  PartitionMagic  84  OS/2 hidden or  c6  DRDOS/sec (FAT-
 4  FAT16 <32M      40  Venix 80286     85  Linux extended  c7  Syrinx
 5  Extended        41  PPC PReP Boot   86  NTFS volume set da  Non-FS data
 6  FAT16           42  SFS             87  NTFS volume set db  CP/M / CTOS / .
 7  HPFS/NTFS/exFAT 4d  QNX4.x          88  Linux plaintext de  Dell Utility
 8  AIX             4e  QNX4.x 2nd part 8e  Linux LVM       df  BootIt
 9  AIX bootable    4f  QNX4.x 3rd part 93  Amoeba          e1  DOS access
 a  OS/2 Boot Manag 50  OnTrack DM      94  Amoeba BBT      e3  DOS R/O
 b  W95 FAT32       51  OnTrack DM6 Aux 9f  BSD/OS          e4  SpeedStor
 c  W95 FAT32 (LBA) 52  CP/M            a0  IBM Thinkpad hi ea  Rufus alignment
 e  W95 FAT16 (LBA) 53  OnTrack DM6 Aux a5  FreeBSD         eb  BeOS fs
 f  W95 Ext'd (LBA) 54  OnTrackDM6      a6  OpenBSD         ee  GPT
10  OPUS            55  EZ-Drive        a7  NeXTSTEP        ef  EFI (FAT-12/16/  
11  Hidden FAT12    56  Golden Bow      a8  Darwin UFS      f0  Linux/PA-RISC b  
12  Compaq diagnost 5c  Priam Edisk     a9  NetBSD          f1  SpeedStor  
14  Hidden FAT16 <3 61  SpeedStor       ab  Darwin boot     f4  SpeedStor  
16  Hidden FAT16    63  GNU HURD or Sys af  HFS / HFS+      f2  DOS secondary  
17  Hidden HPFS/NTF 64  Novell Netware  b7  BSDI fs         fb  VMware VMFS  
18  AST SmartSleep  65  Novell Netware  b8  BSDI swap       fc  VMware VMKCORE  
1b  Hidden W95 FAT3 70  DiskSecure Mult bb  Boot Wizard hid fd  Linux raid auto  
1c  Hidden W95 FAT3 75  PC/IX           bc  Acronis FAT32 L fe  LANstep  
1e  Hidden W95 FAT1 80  Old Minix       be  Solaris boot    ff  BBT

Partition type (type L to list all types): 83  
Changed type of partition 'Linux' to 'Linux'.
```
Check if partition was created corractly.
```
Command (m for help): p
Disk /dev/sda1: 931.5 GiB, 1000137777152 bytes, 1953394096 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x486b65c4
```
Save and Quit.
```
Command (m for help): w  
The partition table has been altered.  
Calling ioctl() to re-read partition table.  
Syncing disks.
```
## Assign a filesystem to the Partition
We need to unmount the partition first
- `$ sudo umount /dev/sda1`

Assign `ext4` to the partition. You may choose whatever filesystem you prefer.
- `$ sudo mkfs.ext4 /dev/sda1`
```
mke2fs 1.42.13 (17-Feb-2019)  
Creating filesystem with 244190390 4k blocks and 61054976 inodes  
Filesystem UUID: fb0b2abd-a3ac-3301-a41a-8d9ca2376ba7  
Superblock backups stored on blocks:  
    32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
    4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968,
    102400000, 214990848

Allocating group tables: done  
Writing inode tables: done  
Creating journal (32768 blocks): done  
Writing superblocks and filesystem accounting information: done
```
## Make a New Directory for the Partition and Mount it
Make a new directory.
- `$ mkdir /home/storj/<disk_name>`

Mount the partition to that directory.
- `$ sudo mount /dev/sda1 /home/storj/<disk_name>`

Set correct permission.
- `sudo chown storj:storj /home/storj/<disk_name>`
- `sudo chmod 777 /home/storj/<disk_name>`

-----

Next: [Install & Run Daemon](daemon.md)