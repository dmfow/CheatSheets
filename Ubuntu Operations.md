#### remove cloud init
```
# Disable
sudo touch /etc/cloud/cloud-init.disabled
reboot

# Remove
sudo apt purge cloud-init -y
sudo rm -rf /etc/cloud && sudo rm -rf /var/lib/cloud/
reboot

```


#### automatic installation of security upgrades
```
sudo apt-get install unattended-upgrades
sudo dpkg-reconfigure  unattended-upgrades

# https://askubuntu.com/questions/578761/how-to-only-install-security-updates

# Run Once (-d = with debug)
sudo unattended-upgrades -d

```

#### Upgrade within release
```
sudo apt update
sudo apt upgrade

```

#### Upgrade Release (eg 20.04 LTS to 22.04 TLS)
```
sudo apt install update-manager-core
sudo apt update && sudo apt dist-upgrade
sudo do-release-upgrade

```

#### Clear diskpace for Journal
```
  journalctl --disk-usage
  sudo journalctl --rotate
  sudo journalctl --vacuum-time=1w
  sudo journalctl --vacuum-time=1h
  # Clear all (down to 1 second)
  sudo journalctl --vacuum-time=1s
  
```

#### Check SSD health/wear
```
# Explanation of items
# https://en.wikipedia.org/wiki/Self-Monitoring,_Analysis,_and_Reporting_Technology

smartctl -a /dev/sda

# Calculate TB written
smartctl /dev/sda --all |grep "Sector Size"
  $ Sector Size:      512 bytes logical/physical
# 512 Byte/LBA (Sector size)
smartctl -a /dev/sda | grep "Total_LBAs_Written" | grep -o '[^ ]\+$' | awk '{ SUM = ($1 * 512) / 1000000000000 } END {print SUM " TB written"}'

# Drive health ??
smartctl -a /dev/sda | grep "Wear_Leveling_Count" | grep -o '[^ ]\+$' | awk 'END {print $1 "%"}'
# Drive power-on time
smartctl -a /dev/sda | grep "Power_On_Hours" | grep -o '[^ ]\+$' | awk '{ SUM = $1 / 24 / 365 } END {print SUM " years"}'

# Other outputs
smartctl -aA /dev/sda
smartctl -l /dev/sda
smartctl -A /dev/sda | grep -i 'media_wearout_indicator' | tr -s ' ' | cut -d' ' -f4-5

# Check which disks are present
sudo lsblk -f

```


#### Check mail logs
```
cd /var/log
cat mail.log | grep status=sent | grep "<[A-Za-z0-9.@ ]*>"
cat mail.log | grep status=deferred | grep "<[A-Za-z0-9.@ ]*>"
cat mail.log | grep status=bounced | grep "<[A-Za-z0-9.@ ]*>"

```




## Firewall


## IP tables firewall

## Backup
Try "Timeshift"

## Disk usage (GUI)
Try "Disc usage Analyzer"

## List rules
```
sudo iptables -v -x -n -L
sudo iptables -t nat -v -x -n -L

```

## UFW firewall
```
sudo ufw status

```








