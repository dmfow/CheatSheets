## Alpine linx
Server linux with small footprint: ~250 MB size<br>

#### Install
```
Pre-install (if not done before, it is difficult to go back)
* Fix network connectivity beforehand
* Get the DNS server IP/name
* Choose network, mask (/x CIDR), Default gateway
* Decide on lvm and/or disk layout
* Less important (swing it): keyboard layout, timezone

```

#### Update/Upgrade
```
su
apk update
apk upgrade
sync
reboot
```

#### Package info
```
# List all installed packages
apk info

# List packages in with info and in alphabetical order
apk -vv info
```
