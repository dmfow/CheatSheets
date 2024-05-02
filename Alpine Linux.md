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
reboot
```

#### Update
```
su
apk update
apk upgrade
sync
reboot
```
