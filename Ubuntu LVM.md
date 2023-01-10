## Disc system

#### Check if lvm is used
```
cat /etc/fstab

#If the line starts with UUID=xyz, this means it's a physical partition.
#If the line starst with /dev/sdaX, it also means it's a physical partition.
#The indicator for LVM would be something with /dev/mapper/xyz
```

#### Create a logical volume
https://www.howtogeek.com/howto/40702/how-to-manage-and-use-lvm-logical-volume-management-in-ubuntu/
```
# Other stuff
vdisplay

# List existing volumes
fdisk -l

# Create a new volume
fdisk /dev/sdb

# Warning: The following steps will format your hard drive. 
# Make sure you don’t have any information on this hard drive before following #these steps.
#    n = create new partition
#    p = creates primary partition
#    1 = makes partition the first on the disk

# Push enter twice
#
# To prepare the partition to be used by LVM use the following two commands.
#    t = change partition type
#    8e = changes to LVM partition type
#
#Verify and write the information to the hard drive.
#    p = view partition setup so we can review before writing changes to disk
#    w = write changes to disk

# After those commands, the fdisk prompt should EXIT and you will be back to the bash prompt of your terminal.
# Enter pvcreate /dev/sdb1 to create a LVM physical volume on the partition we just created
vgcreate vgpool /dev/sdb1
lvcreate -L 3G -n lvstuff vgpool

# Format
mkfs -t ext3 /dev/vgpool/lvstuff

# Create a mount point
mkdir /mnt/stuff
mount -t ext3 /dev/vgpool/lvstuff /mnt/stuff
    
```

#### Extend a volume
https://www.howtogeek.com/howto/40702/how-to-manage-and-use-lvm-logical-volume-management-in-ubuntu/
```
sudo fdisk -l
# Look for /dev/sda
sudo cfdisk /dev/sda
# Look for Free Space on Device
# Choose New  -> Primary -> Specify Bytes
# It got a new sdaX number for X
# Create a new volume (replace X with your number)
pvcreate /dev/sdaX

# Check yoyr vg name of the "old" physical volume
sudo pvdisplay

# Add New Hard Drive to Volume Group (replace X with your number)
vgextend vgname /dev/sdaX

# Check the name of the logical volume
sudo lvdisplay

# Extend Logical Volume
lvextend -L8G /dev/vgname/lvname
lvextend -L+3G /dev/vgname/lvname

# Extend File System
resize2fs /dev/vgname/lvname
```


#### Shrink a volume
https://www.howtogeek.com/howto/40702/how-to-manage-and-use-lvm-logical-volume-management-in-ubuntu/

#### Make a snapshot
https://www.howtogeek.com/howto/40702/how-to-manage-and-use-lvm-logical-volume-management-in-ubuntu/

#### Delete a logical volume
```
# first make sure the volume is unmounted,
mount /mnt/lvstuff
lvremove /dev/vgpool/lvstuff
vgremove vgpool
pvremove /dev/sdb1 /dev/sdc1
```





