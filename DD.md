

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

## Check integrity of a file (eg a downloaded file)
#### With OpenSSL
```

```

#### With SHA (sh256sum file + file, In the same library)
```
  # In the library:
  # [program]-sha256sum.txt
  # [program]-Debian-12-amd64.deb

sha256sum -c veracrypt-1.25.9-sha256sum.txt 2>&1 | grep OK
```

#### With GPG (key + sig + file to verify)
```
gpg --import [Program]-key.asc 
gpg --verify [Program]-Linux-console-x64.tar.gz.sig [Program]-Linux-console-x64.tar.gz
```


#### Others commands (not verification)
```
  # Check GPG version
  gpg --version
  # SHA
  sha256sum --version
```

