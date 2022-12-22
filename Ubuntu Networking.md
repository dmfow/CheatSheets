

#### Check your IP
```
hostname -I
# OR
hostname --all-ip-address
# OR (ip addr)
ip a
# OR
ip link

# Check the public IP
curl http://info.cern.ch/
# OR
dig +short myip.opendns.com @resolver1.opendns.com
# OR
dig -6 TXT +short o-o.myaddr.l.google.com @ns1.google.com

# Link to cheetsheet for ip addr (old redhat, but should be approx the same): 
# https://access.redhat.com/articles/ip-command-cheat-sheet
```

#### DNS lookups
```
dig ubuntu.com MX
dig -x 142.93.143.135
dig ubuntu.com linuxhandbook.com
```
#### Check statusof the local resolver
```
# Ubuntu 20.04 and later
systemd-resolve --status

# Ubuntu <20.04
resolvectl status

```

#### Change resolver
```

# Temporarily
nano /etc/resolv.conf
nameserver 1.2.3.4
nameserver 1.0.1.3
# Verify
$ dig ubuntu.com | grep SERVER
;; SERVER: 1.1.1.2#53(1.1.1.2) (UDP)

# Permanent
# 1. Check your network interface name with
ip addr
# 2. 
nano /etc/netplan/
# 3. Change config (nameservers/addresses)
network:
  ethernets:
    enp1s0:
      dhcp4: true
      nameservers:
        addresses: [1.1.1.2, 1.0.0.2]
  version: 2
# 4. Save and apply
sudo netplan apply
```


#### "Open" DNS providers (they will keep your data)
```
Provider
	Primary IP Address
	Fall-back IP Address

Cloudflare
	1.1.1.1
	1.0.0.1

Cloudflare (malware blocking)
	1.1.1.2
	1.0.0.2

Google
	8.8.8.8
	8.4.4.8

Quad9
	9.9.9.9
	149.112.112.112

OpenDNS
	208.67.222.222
	208.67.220.220
  
```



