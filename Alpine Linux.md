## Alpine Linux
Server linux with small footprint: ~250 MB size<br>
* Requirements: https://wiki.alpinelinux.org/wiki/Requirements
* User handbook: https://docs.alpinelinux.org/user-handbook/0.1a/index.html
* Wiki: https://wiki.alpinelinux.org/wiki/Installation
* Website: https://alpinelinux.org/


#### Installation
```
Pre-install (if not done before, it is difficult to go back)
* Fix network connectivity beforehand
* Get the DNS server IP/name
* Choose network, mask (/x CIDR), Default gateway
* Decide on lvm and/or disk layout (sys mode, e.g. on a hard drive, can be combined with eg LVM)
* Less important (swing it): keyboard layout, timezone
* openSSH is default
Others
* Choose a keyboard layout
* Provide a FQDN for this machine
* Select a NIC (check the name)
* Provide an IP address or “dhcp”
* Provide a new root password
* Provide a time zone (eg US/ and the Eastern, or Europe/ and then Amsterdam)
* Provide a proxy address if you are using a proxy
* Select a mirror site or “f” to find the fastest mirror for you (or hit enter)
* Set up a regular user (highly recommended)
* Provide an SSH key if desired
* Select an SSH server (openssh is the default)
* Select the disk top install the OS onto. Usually “sda”
* Select the disk layout (“sys” is good choice)
* Erase the disk


Install with ISO
Boot ISO
Login with user root, no pw (enter)
# run
setup-alpine

# Post installation (after)
Read: https://docs.alpinelinux.org/user-handbook/0.1a/Working/post-install.html
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


#### Handling
```
# Shutdown now (-r, -H, -P, respectively)
reboot
halt
poweroff

# Start/Stop services
/etc/init.d/httpd start
/etc/init.d/httpd stop
/etc/init.d/httpd restart
# OR
rc-service httpd start
rc-service httpd stop
rc-service httpd restart

# Configure service to start automatically
rc-update add <service_name> <runlevel>
# Enable at boot time
rc-update add httpd boot

# Disable service
rc-update del <service_name> <runlevel>
rc-update del httpd boot

# List of run levels
rc-status --list

# Change run level
rc boot
rc single

# Other
rc-update --help
rc-status --help
rc-service --help
rc --help


# run levels
default: Used if not specified (this is the general, use this if you don't know)
hotplugged: 
manual: 
# more run levels, special, only for advances use
sysinit: sysinit always runs when the host first starts and should not be run again
boot: in general, only use for services mounting of filesystems
single: stops all services except for those in the sysinit runlevel
reboot: changes to the shutdown runlevel and then reboots the host
shutdown: halts the server

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

# Community repo - If you didn't do "doas" in the installation, you might want sudo
apk add sudo
# In , after the line root ALL=(ALL:ALL) ALL, add your user [user ALL=(ALL:ALL) ALL]
# But read more about the impact of this.
# Alternative, eg here: https://ostechnix.com/add-delete-and-grant-sudo-privileges-to-users-in-alpine-linux/

# Delete (pruge removes config files also)
apk del nano
apk del --purge vim

# Clean the cache (to free space)
apk cache clean

# Fix broken packages
apk fix
```


#### Networking
```
# Su or su or doas
sudo nano /etc/network/interfaces

# restart/reload network services
sudo rc-service networking restart

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



