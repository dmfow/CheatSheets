## Build a bootable USB

```
sudo lsblk -f
# Check which Disk name the USB have

# !!!!!!! NOTE- chose the right sdX - OR YOU MIGHT DESTROY YOUR COMPUTER !!!!!!!!!!!!!!!!!

dd status-progress if=/home/USER/downloads/theisofile.iso of=/dev/sdd


```
