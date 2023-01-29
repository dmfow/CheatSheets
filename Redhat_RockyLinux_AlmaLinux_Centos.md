## Mixed

### Network
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/sec-configuring_ip_networking_with_nmcli

https://access.redhat.com/articles/ip-command-cheat-sheet

```
# Checking
ip a
nmcli -p device
nmcli general status
nmcli connection show
nmcli connection show --active
nmcli dev disconnect ens3
nmcli dev connect ens3

# Configure
ip a add 192.168.1.3/24 dev ens3
ip a del 192.168.1.3/24 dev ens3
``

