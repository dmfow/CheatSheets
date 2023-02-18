## Mixed network stuff
https://wiki.debian.org/NetworkConfiguration

#### Bridge an interface
```
# /etc/network/interfaces

auto lo
iface lo inet loopback

iface enp6s0 inet manual

auto vmbr0
iface vmbr0 inet static
        address 10.0.0.2/24
        gateway 10.0.0.1
        bridge-ports enp6s0
        bridge-stp off
        bridge-fd 0


$ ifreload -a

```
        


## Proxmox

#### Enable ipv4
```
# /etc/sysctl.conf
net.ipv4.ip_forward=1
net.ipv4.conf.all.accept_redirects = 0
```

#### Chrony
```
# /etc/chrony/chrony.conf
pool ntp.server.com

# set and restart
timedatectl set-ntp yes
systemctl restart chronyd
timedatectl

```

