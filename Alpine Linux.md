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

# Dependencies
apk info -R nano

# Origin
apk info -W /etc/rc.conf

# Installed size
apk info -s nano

# Stats
apk stats

```

#### Install some basic packages (or delete)
```
# Some basic packages
apk add -u nano
apk add python3

# Some basic packages need the community repo. Unmark the following line in the file /etc/apk/repositories
http://dl-cdn.alpinelinux.org/alpine/v3.19/community

# Community repo
apk add py3-pip


# Delete (pruge removes config files also)
apk del nano
apk del --purge vim

# Clean the cache (to free space)
apk cache clean

# Fix broken packages
apk fix
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



