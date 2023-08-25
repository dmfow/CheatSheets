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

#### DNS/DHCP
```
# DNS
/etc/resolv.conf

# DHCP
/etc/dhcp/dhclient.conf 
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


#### Upgrade
```
apt-get update
apt-get dist-upgrade
```




#### Temperature sensors
```
apt-get install lm-sensors

# 1. Adding info to information (not tested)

nano /usr/share/perl5/PVE/API2/Nodes.pm

# 2. Next, you can press F6 to search for my $dinfo and press Enter
# It should look like this
#         $res->{pveversion} = PVE::pvecfg::package() . "/" .
#             PVE::pvecfg::version_text();
# 
#         my $dinfo = df('/', 1);     # output is bytes

# 3. Change to:
        $res->{pveversion} = PVE::pvecfg::package() . "/" .
            PVE::pvecfg::version_text();
        $res->{thermalstate} = `sensors`;
        my $dinfo = df('/', 1);     # output is bytes
# 4. Save (ctrl+O, ctrl+X)

# 5. Edit another file
nano /usr/share/pve-manager/js/pvemanagerlib.js

# 6. Once in press F6 to search for my widget.pveNodeStatus and press Enter

     Ext.define('PVE.node.StatusView', {
     extend: 'PVE.panel.StatusView',
     alias: 'widget.pveNodeStatus',
 
     height: 300,
     bodyPadding: '5 15 5 15',
 
     layout: {
         type: 'table',
         columns: 2,
         tableAttrs: {
             style: {
                 width: '100%'
             }
         }
     },

# 7. Change the bodyPadding: '5 15 5 15', to bodyPadding: '20 15 20 15',
# 8. height: 300, to height: 360, 
# 9. press F6 to search for PVE Manager Version and press Enter. You will see
        {
             itemId: 'version',
             colspan: 2,
             printBar: false,
             title: gettext('PVE Manager Version'),
             textField: 'pveversion',
             value: ''
         }
# 10. Add after so it look like this
        {
            itemId: 'version',
            colspan: 2,
            printBar: false,
            title: gettext('PVE Manager Version'),
            textField: 'pveversion',
            value: ''
        },
        {
            itemId: 'thermal',
            colspan: 2,
            printBar: false,
            title: gettext('CPU Thermal State'),
            textField: 'thermalstate',
            renderer:function(value){
                const c0 = value.match(/Core 0.*?\+([\d\.]+)Â/)[1];
                const c1 = value.match(/Core 1.*?\+([\d\.]+)Â/)[1];
                const c2 = value.match(/Core 2.*?\+([\d\.]+)Â/)[1];
                const c3 = value.match(/Core 3.*?\+([\d\.]+)Â/)[1];
                return `Core 0: ${c0} ℃ | Core 1: ${c1} ℃ | Core 2: ${c2} ℃ | Core 3: ${c3} ℃`
            }
        }
# 11. Save (ctrl+O, ctrl+X)

# 12. Restart pveproxy (you might get kicked out of the shell
systemctl restart pveproxy

# More info: https://www.reddit.com/r/homelab/comments/rhq56e/displaying_cpu_temperature_in_proxmox_summery_in/?rdt=57088




```

