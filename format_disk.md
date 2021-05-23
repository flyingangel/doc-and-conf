# Format a disk in ext4

```bash
#list device block
lsblk
#check more info
fdisk -l
#begin format disk
fdisk /dev/sdb
#new partition
n
#primary
p
#(Press ENTER) (Use default partition number)
#(Press ENTER) (Use default first sector)
#(Press ENTER) (Use default last sector)
#write
w
#recheck block list
lsblk
#format with ext4 filesystem
mkfs -t ext4 /dev/sdb1

#configuration for automount and mount at boot
cp /etc/fstab /etc/fstab.backup
nano /etc/fstab
#Write the following lines at the end
/dev/sdb1 /some/path ext4 defaults 0 2
#Then exit fstab

#create folder to mount
mkdir -p /some/path
#auto mount
mount -a
```
