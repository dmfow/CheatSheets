## Build a bootable USB

```
sudo lsblk -f
# Check which Disk name the USB have

# !!!!!!! NOTE- chose the right sdX - OR YOU MIGHT DESTROY YOUR COMPUTER !!!!!!!!!!!!!!!!!

# Guidance - Don't choose any disk with a mountpoint (you can see them to the right)

sudo dd status-progress if=/home/USER/downloads/theisofile.iso of=/dev/sdd

sudo eject sdd

sudo lsblk -f

```
