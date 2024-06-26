

## Build a bootable USB - Linux

```
# Check which Disk name the USB have
  # !!!!!!! NOTE - read the right sdX - OR YOU MIGHT DESTROY YOUR COMPUTER !!!!!!!!!!!!!!!!!
 # Guidance - Don't choose any disk with a mountpoint (you can see them to the right)
sudo lsblk -f

# make the USB bootable disk
  # It is called Disk Destroyer, so write it correct
sudo dd status=progress if=/home/USER/downloads/theisofile.iso of=/dev/sdX

# Eject the USB
sudo eject sdX

# Check that is it ejected (nothing in the mountpoint column)
sudo lsblk -f

```

## Format an USB - Linux
```
# Check which Disk name the USB have
  # !!!!!!! NOTE - read the right sdX - OR YOU MIGHT DESTROY YOUR COMPUTER !!!!!!!!!!!!!!!!!
 # Guidance - Don't choose any disk with a mountpoint (you can see them to the right)
sudo lsblk -f

# Put zeros on the disk (can take a wile with large USBs) (change X to your letter)
sudo dd if=/dev/zero of=/dev/sdX bs=4k && sync

# Make a partition
sudo fdisk /dev/sdX

# m  to see the menu, then make the partition
o [+Enter]
n [+Enter] (make a new partition)
p [+Enter] (make it a raimary partition)
w [+Enter]

# Format it as vfat
sudo mkfs.vfat /dev/sdX1

# Eject it
sudo eject /dev/sdb

```


## Check integrity of a file (eg a downloaded file)
#### With OpenSSL
```
# In the library:

  # The SHA-256 checksum file (<filename>.sha256)
  # The bzip compressed Image file (<filename>.<image>.bz2)
  # The signature file (<filename>.<image>.bz2.sig)
  # The openssl public key (<filename>.pub)

1. Checksum match (so you got the whole file)
openssl sha256 <filename>.bz2
cat <filename>.sha256

2. If #1 is alright
openssl base64 -d -in <filename>.sig -out ./image.sig
openssl dgst -sha256 -verify <filename>.pub -signature ./image.sig <filename>.bz2

! Be aware of the public key (.pub), it can have been altered on it's way
! Match the checksum command output with the checksum values in the file OPNsense-<version>-OpenSSL-checksums-amd64.sha256
! If it doesn't match something is wrong

```

#### With SHA (sh256sum file + file, In the same library)
```
# In the library:
  # <filename>-sha256sum.txt
  # <filename>-Debian-12-amd64.deb

sha256sum -c <filename>-sha256sum.txt 2>&1 | grep OK

```

#### With GPG (key + sig + file to verify)
```
gpg --import <filename>-key.asc 
gpg --verify <filename>-Linux-console-x64.tar.gz.sig <filename>-Linux-console-x64.tar.gz
```


#### Others commands (not verification)
```
  # Check GPG version
  gpg --version
  # SHA
  sha256sum --version
```

