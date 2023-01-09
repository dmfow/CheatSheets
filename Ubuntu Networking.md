

#### Check your IP
```
hostname -I
# OR
hostname --all-ip-address
# OR (ip addr)
ip a
# OR
ip link

# Check the public IP behind a NAT/PAT
curl http://info.cern.ch/
# OR (info.cern.ch)
curl 188.184.21.108
# OR (they will keep your data)
dig +short myip.opendns.com @resolver1.opendns.com

# Link to cheetsheet for ip addr (old redhat, but should be approx the same): 
# https://access.redhat.com/articles/ip-command-cheat-sheet
```

#### Change IP / Default Gateway - and restart the network
```
# Find the right file in /etc/netplan/
sudo nano thefile
strl+o
ctrl+x

# This is depreciated
gateway4: 192.168.1.1
# Instead use "routes" (replace with the same indentation)
routes:
- to: default
  via: 192.168.1.1


# Restart the network on the server (through network manager)
sudo netplan apply
# OR (through network manager if installed)
sudo service network-manager restart
# OR (through systemd, at least on older systems)
sudo systemctl restart NetworkManager.service
```

#### Ethernet systemd naming convention
```
# eno1 — is the first on board NIC
# enp3s0f1 — is the NIC on pcibus 3 slot 0 and use the NIC function 1.

# Third character =>
  # o<index>[n<phys_port_name>|d<dev_port>] — devices on board
  # s<slot>[f<function>][n<phys_port_name>|d<dev_port>] — device by hotplug id
  # [P<domain>]p<bus>s<slot>[f<function>][n<phys_port_name>|d<dev_port>] — devices by bus id
  # x<MAC> — device by MAC address
# Why this? https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/
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
nano /etc/netplan/yournetworkfile
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


#### Download with Curl
```
curl http://info.cern.ch/
# Resume downloading
curl -C 1024 http://whatever.org/files/largeFile.mpv -O
# Default filename
curl -O http://www.ubuntu.com/robots.txt
# Custom filename
curl -O http://www.ubuntu.com/robots.txt googleRobots.txt
# Multiple files
curl url1 url2 url3
curl url1 url2 url3 -O -O -O 
# A range of files
curl http://www.ubuntu.com/logo/logo[1-9].png
# Modified after a specific date and time
curl url -z "DD MMM YY MM:HH:SS"
# Upload
curl -T uploadFile.txt http://whatever.org/files
# Avaid redirects
curl -L  http://www.ubuntu.com
# Authentication
curl -u username:password http://whatever.org/files/tasks.txt
# Limit transfer rate
curl --limit-rate 2K http://whatever.org/files/logoDetails.tgz
# Ignore ssl cert
curl -k https://whatever.org
# Also get header info
curl -i http://www.ubuntu.com/robots.txt
# Only get header info
curl -I http://www.ubuntu.com/robots.txt
# Send some data in the request
curl -d "token=1234abcdef&name='john john'" http://api.restful.org/getcontent
```




