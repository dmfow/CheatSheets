#### Check version
```
lsb_release -a
# OR
lsb_release -d
# OR
cat /etc/os-release
# OR
cat /etc/issue
# OR
hostnamectl
```

#### Check diskspace
```
df -h
# Check with with a mount point. Eg root
df -h /
# Check within a directory. Eg the home library
du -sh ~
```

#### Check the disk names and volumns
```
sudo lsblk -f

# Check disk model
lshw -class disk
# OR
hwinfo --disk
# OR
smartctl -i /dev/sda
```
#### Check  hardware
```
# motherboard hardware
lspci
lspci - vnn
# Audio
lspci -v | grep -A7 -i "audio"
# Network
lspci -nnk | grep net -A2
# CPU
lscpu
# Hardware
lshw
lshw -short
# Hardware
hwinfo
# usb
lsusb
```

#### Find a file

```
find LOCATION -name FILE_NAME
  # Examples
  find ~ -name resolution-for-year-2022.txt
  find . -name "*.png"
  find ~ -type f -empty
  
  find ./ -name myfile 2>&1 | grep -v "Permission denied" 2>&1 | grep -v "not permitted" 2>&1 | grep -v "No such file"
  
# OR to find a file with a specific text
grep -irl "text" <dir>
    # i - for case insensitive search
    # r - for recursive search inside subdirectories
    # l - to show only the file names, not the matching lines 
    # Exempel
    grep -irl "for" .

# Find large files
sudo find ~ -type f -printf '%s\t%p\n' | sort -n | tail -2
find $HOME -type f -printf '%s %p\n' | sort -nr | head -10
find / -size +100M -ls
find $DIRECTORY -type f -exec ls -s {} \; | sort -n | tail -n 5

sudo du -a /home | sort -n -r | head -n 10
sudo du -a | sort -n -r | head -n 10
du -hs * | sort -rh | head -n 10
du -Sh | sort -rh | head -n 10
sudo du -hsx * | sort -rh | head -10

ls -lSh /bin | head -5
ls -lah --sort=size
```

#### unzipp
```
# .zip
unzip thefile.zip

# .gz
gunzip < thefile.txt.gzip > newfile.txt

# .tar.gz
tar -xvf thefile.tzr.gz

# untar
tar -xvf thefile.tar -C ./
sudo tar -xvf thefile.tar -C ./
untar thefile.tar

# bz2 (sudo apt install bzip2)
bzip2 -d thefile.bz2


# bz2 compress
bzip2 thenewbz2file
# OR
bzip2 -z thenewbz2file


```

#### File handling
```
# Rename
mv file file2

# Move
mv file folder/file

# Copy
cp file file.bak
# Copy library recursively
cp -R lib/* lib2/

# Delete
rm file
# Delete multiple files
rm file file.bak
rm *.bak
# Delete a directory and all directories and files within
rm -rf lampp

```

#### Start the display (and window manager) - in this case lightdm (could be gdm, sddm etc)
```
sudo lightdm
```


#### Set the time
```
sudo timedatectl set-time 21:45:53
sudo timedatectl set-time 2019-04-10

# Timezones
timedatectl list-timezones
timedatectl list-timezones | grep keyword
sudo timedatectl set-timezone Region/Location

# NTP time sync
sudo timedatectl set-ntp yes
sudo timedatectl set-ntp no
```

#### Stop lightDM
```
alt+ctl+F1 (or other F button)
Try different Fx till you find the terminal where you started lightDM
ctrl+C
```

#### Journal
```
# Since time/date
journalctl -S "2020-91-12 07:00:00"
journalctl --since "2015-01-10" --until "2015-01-11 03:00"
journalctl --since yesterday
journalctl --since 09:00 --until "1 hour ago"

# Since previous boot
journalctl -b -1

# Bya unit
journalctl -u nginx.service
journalctl -u nginx.service --since today
journalctl -u nginx.service -u php-fpm.service --since today

# Byt group/user
journalctl _PID=8001

# Check a UID and then use it
id -u www-data
journalctl _UID=33 --since today

# See group IDs
journalctl -F _GID

# By component path
journalctl /usr/bin/bash

# Kernel
journalctl -k
journalctl -k -b -5

# By priority
journalctl -p err -b

# Limit the number of rows
journalctl -n 20

# Output json
journalctl -o json

# Actively follow the logs
journalctl -f

```

#### Journal management
```
# Disk usage of the journal system
journalctl --disk-usage

# Remove entries (in this case keep 1G of entries)
sudo journalctl --vacuum-size=1G

# Remove entries (in this case keep 1 year of entries)
sudo journalctl --vacuum-time=1years

```




#### SCP copy files between 2 linux boxes with scp (Secure copy over ssh)
```
scp -r *.* user@host:/directory
```



#### Sound Troubleshooting
```
inxi -SMA

sudo alsa force-reload
# sudo apt-get install --reinstall alsa-base pulseaudio
pulseaudio --start
```

#### Install sound packets
```
sudo apt install inxi

```






