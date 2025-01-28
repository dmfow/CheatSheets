## Free BSD stuff 

#### See release and disks
```
# Version
uname -a
# Relese
freebsd-version -u

# Disk
df -hi

# vi editor cheat sheet
# https://ryanstutorials.net/linuxtutorial/cheatsheetvi.php
```

#### Restart the filesystem
```
/etc/rc.d/devfs restart
# OR
service devfs restart
```

## Network
```
# Check
ifconfig
netstat -r
netstat -nr

# Add persistant routes
# https://docs.freebsd.org/en/books/handbook/advanced-networking/#network-routing
# in /etc/rc.conf (add net1 and net2 as a persistent static route)
static_routes="net1 net2"
route_net1="-net 192.168.0.0/24 192.168.0.1"
route_net2="-net 192.168.1.0/24 192.168.1.1"

# Add routes (Non persistant)
route add default 10.20.30.1
route add -net 192.168.2.0/24 192.168.1.2

# Restart the service
service netif restart && service routing restart

# Check network adapters
pciconf -lv | grep -A1 -B3 network

```


## Various package commands
```
pkg bootstrap -f
pkg upgrade -f

pkg -d update -f
pkg update -f

pkg clean -ya
```


