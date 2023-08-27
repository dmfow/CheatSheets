
## Issues in general

#### Some logs to check if an update went south
```
sudo cat /var/log/apt/history.log
sudo cat /var/log/dpkg.log
```


## Issues with the grapical (display manager, windows manager)

#### Some logs to check
```
sudo cat /var/log/sddm/lightdm.log
sudo cat /var/log/lightdm/lightdm.log
sudo cat /var/log/x-0.log
sudo cat /var/log/x-1.log
cat ~/.xsession-errors
```

#### Display drivers
```
lsmod | grep nvidia
ubuntu-drivers devices
nvidia-smi
```

## Fix graphical

#### Try A - Remove the last installed packages
```
# Check the logfile for the date and time
cat /var/log/apt/history.log
# Take out the lines from a specific date, and place it in a file in the /tmp directory
# the file will be removed at reboot, if you want to keep it, place it somewhere else
grep -A 2 'Start-Date: 2023-04-21  12:10:37' /var/log/apt/history.log | tail -1 >/tmp/packages.txt
sed -i 's/Install://' /tmp/packages.txt
tr ',' '\n' < /tmp/packages.txt | sed '/automatic)/d' | awk '{ print $1}' > /tmp/final.packages.txt
wc -l /tmp/final.packages.txt
nano /tmp/final.packages.txt    # If needed, edit the file
p="$(</tmp/final.packages.txt)"
# Remove the packages
sudo apt-get --purge remove $p
# Do some cleanup
sudo apt-get clean
sudo apt-get autoremove
```

#### Try B - fix a broken apt installation
```
sudo apt --fix-broken install
sudo apt-get clean
sudo apt-get autoremove
```

#### Try C - install the latest NVidia driver
```
sudo apt-get install nvidia-driver-[version number] nvidia-settings
```

#### Other Nvidia
```
# remove a specific nvidia driver
sudo apt-get remove --purge nvidia-driver-[version number]

# Remove all nvidia drivers
sudo apt-get remove --purge nvidia-*
```

#### Nvidia driver version
```
# List of different Linux version
# https://www.nvidia.com/en-us/drivers/unix/

# Latest
# https://www.nvidia.com/Download/index.aspx?lang=en-us
```



