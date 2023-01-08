## Build a bootable USB - Linux

```
# Check which Disk name the USB have
  # !!!!!!! NOTE - read the right sdX - OR YOU MIGHT DESTROY YOUR COMPUTER !!!!!!!!!!!!!!!!!
 # Guidance - Don't choose any disk with a mountpoint (you can see them to the right)
sudo lsblk -f

# make the USB bootable disk
  # It is called Disk Destroyer, so write it correct
sudo dd status-progress if=/home/USER/downloads/theisofile.iso of=/dev/sdd

# Eject the USB
sudo eject sdd

# Check that is it ejected (nothing in the mountpoint column)
sudo lsblk -f

```
