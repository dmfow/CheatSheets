## Alpine linx
Server linux with small footprint: ~250 MB size<br>

#### Install
```
Pre-install (if not done before, it is difficult to go back)
* Fix network connectivity beforehand
* Get the DNS server IP/name
* Choose network, mask (/x CIDR), Default gateway
* Decide on lvm and/or disk layout (sys mode, e.g. on a hard drive, can be combined with eg LVM)
* Less important (swing it): keyboard layout, timezone

```

#### Update/Upgrade
```
su
apk update
apk upgrade
# or (both update and upgrade)
apk -U upgrade

# Force upgrade even if it is the same version number
apk upgrade --available

# If the kernel is upgraded, sync and reboot
sync
reboot

# Upgrade the package manager (sometimes required)
apk add --upgrade apk-tools

```

#### Package info
```
# List all installed packages
apk info

# List packages in with info and in alphabetical order
apk -vv info

# Search for a specific
apk search -v nano
```

#### Install some basic packages (or delete)
```
# There is an editor, maybe you want another
apk add -u nano

# Delete
apk del nano

```


#### ...
```
```

#### ...
```
```

#### ...
```
```

#### ...
```
```



