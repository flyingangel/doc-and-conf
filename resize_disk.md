# Resize a disk

## Type LVM

Warning: it is important to write down the old start/end cylinder. Otherwise there will be data lost.

Normally they are calculated automatically, but just in case.

```bash
#detect new disk if not regconize by the OS / or reboot
echo '1' > /sys/class/scsi_disk/0\:0\:0\:0/device/rescan

#list device block
lsblk
#check more info
fdisk -l
#write down the start/end cylinder here

#begin format disk
fdisk /dev/sda
#select primary
p
#delete partition
d

#recreate primary partition
n
p
#(Press ENTER) (Use default partition number)
#(Press ENTER) (Use default first sector)
#(Press ENTER) (Use default last sector)
#choose partition type
t
#type LVM code
8e
#verify
p
#write
w

#restart PC
reboot

#check LVM state
vgdisplay
pvdisplay
lvdisplay

#update free space so the OS regconize it
pvresize /dev/sda2

#find free space
vgdisplay
#See: Free PE / Size 7339 / 30 GB
#write down the number 7339

#list all logical volume
lvdisplay
#See: LV Name /dev/SystemVG/RootLV

#to extend size
lvextend -l +7339 /dev/SystemVG/RootLV
#or to reduce: lvreduce -l -7339 /dev/SystemVG/RootLV

#check result
lvdisplay /dev/SystemVG/RootLV

#final resize filesystem
resize2fs /dev/SystemVG/RootLV
#on CentOS: xfs_growfs /dev/centos/root

#restart pc
reboot
df -h
```
