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

#### Limit the Journal filespace
```
# First edit the journald.conf file, add or change the SystemMaxUse entry
sudo nano /etc/systemd/journald.conf
SystemMaxUse=100M
# Then restart the service
sudo service systemd-journald restart
```



#### Diskspace handling
```
# Search for large files
find / -size +50M -ls

# Remove unnecessary dependencies
sudo apt autoremove

# Find manual installed packages
## some of packages are not installed by the user but are pre-installed packages and can be ignored
apt-mark showmanual
# Remove
sudo apt remove <package-name>

# Check snapd usage
du -h /var/lib/snapd/snaps

# check apt cache
sudo du -sh /var/cache/apt
# Clean up apt cache
sudo apt clean

# Check AWS header files
#   Linux kernel headers for Amazon Web Services (AWS) systems
du -h -d1 /usr/src/ | sort -hr
# Remove unnecessary
sudo apt autoremove
# If getting error: Reading package lists... Error!
# remove one or two (the oldest)  manual (be careful)
cd /usr/src
ls -lt
sudo rm -r linux-aws-headers-4.3.0-1012
sudo apt autoremove
# If still error
apt --fix-broken install
sudo apt autoremove

```


#### Check CPU temperatures
```
# See temperature
sensors

# Continuesly (eg checking every 8 seconds) (-f gives farenheit)
watch -n 8 -d sensors

# To detect sensors (run once)
sudo sensors-detect



# Another one (not tested)
sudo apt install lm-sensors

# Description of output
# Intel
#  cpu: coretemp
#  GPU core: gpu in the cpu
# AMD
#  cpu: k10temp
#  GPU core: amdgpu


```

#### Check disk temperature
```
# Disk temp
hddtemp /dev/sda
# OR if it doesn't work
smartctl -a /dev/sdb | grep 190
 $ 190 Airflow_Temperature_Cel 0x0032   073   062   000    Old_age   Always       -       27
# OR look for 194
smartctl -a /dev/sdb
# OR if it doesn't work
hddtemp --debug /dev/sdb | grep 190
  $ field(190)       = 27
# OR look for 194
hddtemp --debug /dev/sdb

# Other temperature - acpitz (ACPI thermal zone): Probably CPU socket temp,  ISA: Probably the CPUs cores temp
sensors

# Install hddtemp
apt install hddtemp
# Install xsensors
apt install xsensors
# Scan for sensors
sensors-detect

# Fix hddtemp "WARNING: Drive /dev/sda doesn't seem to have a temperature sensor."
  # insert into /etc/hddtemp.db this line (or wherever the hddtemp.db is):
  # "Samsung SSD 850 EVO 120G B"                            190  C  "Samsung SSD 850 EVO 120GB"
  # To get a reading directly from "hddtemp /dev/sda". 190 is the number you choose from "hddtemp --debug /dev/sdb" output


# SSD Disks: For reliability, between 30ºC and 50ºC (86ºF to 122ºF) for SSDs under load in a standard desktop computer
# even if they are rated up to 70*C
# https://harddrivegeek.com/ssd-temperature/

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








