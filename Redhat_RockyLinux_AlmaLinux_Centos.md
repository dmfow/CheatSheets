## Mixed

### Network
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/sec-configuring_ip_networking_with_nmcli

https://access.redhat.com/articles/ip-command-cheat-sheet

https://www.redhat.com/sysadmin/7-great-network-commands

```
# Checking
ip a
nmcli -p device
nmcli general status
nmcli connection show
nmcli connection show --active

# Checking routes
ip route show
ip route get 10.13.1.4

# Up and down
nmcli dev disconnect ens3
nmcli dev connect ens3
# OR
ip link set ifname down
ip link set ifname up

# Configure 
vi /etc/sysconfig/network-scripts/route-ens3
        192.168.1.3/24 via 192.168.0.1 dev ens3
        
# Configure NON-persistant (won't survive a reboot)
ip a add 192.168.1.3/24 dev ens3
ip a del 192.168.1.3/24 dev ens3

ip route add 192.168.1.0/24 via 192.168.1.1
#OR
ip route add default via 192.168.1.1 dev ens3

ip route del 192.168.1.0/24

# configure routes
ip route add 192.168.4.0/24 dev ens3
```

#### Troubleshooting (might have to be installed)
```
# Install
sudo dnf install -y bind-utils
sudo dnf -y install mtr
sudo dnf install net-tools 

netstat
ss -l
sudo ss -tnlp
tracepath -n sat65server
mtr
nslookup redhat.com
dig

```



