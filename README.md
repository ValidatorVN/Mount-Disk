# Mount-Disk

1/ Check ổ đĩa xem phân vùng:

    lsblk

2/ Xoá dữ liệu ổ mới thuê: ở đây là sda

    fdisk /dev/sda
    
Welcome to fdisk (util-linux 2.34).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): m

Help:

  DOS (MBR)
   a   toggle a bootable flag
   b   edit nested BSD disklabel
   c   toggle the dos compatibility flag

  Generic
   d   delete a partition
   F   list free unpartitioned space
   l   list known partition types
   n   add a new partition
   p   print the partition table
   t   change a partition type
   v   verify the partition table
   i   print information about a partition

  Misc
   m   print this menu
   u   change display/entry units
   x   extra functionality (experts only)

  Script
   I   load disk layout from sfdisk script file
   O   dump disk layout to sfdisk script file

  Save & Exit
   w   write table to disk and exit
   q   quit without saving changes

  Create a new label
   g   create a new empty GPT partition table
   G   create a new empty SGI (IRIX) partition table
   o   create a new empty DOS partition table
   s   create a new empty Sun partition table


Command (m for help): d
Selected partition 1
Partition 1 has been deleted.

Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1): 
First sector (2048-209715199, default 2048): 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-209715199, default 209715199): 

Created a new partition 1 of type 'Linux' and of size 100 GiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

3/ Kiểm tra lại:

root@ubuntu-s-4vcpu-8gb-nyc1-01:~# lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  61.9M  1 loop /snap/core20/1518
loop1     7:1    0  67.8M  1 loop /snap/lxd/22753
loop3     7:3    0  49.9M  1 loop /snap/snapd/18357
loop4     7:4    0  63.3M  1 loop /snap/core20/1822
loop5     7:5    0  91.9M  1 loop /snap/lxd/24061
sda       8:0    0   100G  0 disk 
└─sda1    8:1    0   100G  0 part 
vda     252:0    0   160G  0 disk 
├─vda1  252:1    0 159.9G  0 part /
├─vda14 252:14   0     4M  0 part 
└─vda15 252:15   0   106M  0 part /boot/efi
vdb     252:16   0   466K  1 disk 

4/ Format ổ sda1:

    mkfs -t ext4 /dev/sda1
    
nhấn y để đồng ý.

5/ Mount ổ bạn muốn cài node: ví dụ .nibid

    mkdir .nibid
    chmod +x nibid
    mount -t ext4 /dev/sda1 /root/.nibid
    
6/ Thêm lưu trữ không mất dữ liệu nếu restart

    nano /etc/fstab
    
    /dev/sda1 /root/.nibid ext4  defaults     0   0
    

From LThuan

