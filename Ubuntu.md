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

# Disk temp
hddtemp /dev/sda
# OR if it doesn't work
smartctl -a /dev/sdb | grep 190
  $ 190 Airflow_Temperature_Cel 0x0032   073   062   000    Old_age   Always       -       27
# OR if it doesn't work
hddtemp --debug /dev/sdb | grep 190
  $ field(190)       = 27
  

# Other temperature - ACPI: Probably CPU socket temp,  ISA: Probably the CPUs cores temp
sensors

# Install hddtemp
apt install hddtemp
# Install xsensors
apt install xsensors
# Scan for sensors
sensors-detect

# SSD Disks: For reliability, between 30ºC and 50ºC (86ºF to 122ºF) for SSDs under load in a standard desktop computer
# even if they are rated up to 70*C
# https://harddrivegeek.com/ssd-temperature/

``


#### Find a file

```
find LOCATION -name FILE_NAME
  # Examples
  find ~ -name resolution-for-year-2022.txt
  find . -name "*.png"
  find ~ -type f -empty
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


#### SCP copy files between 2 linux boxes with scp (Secure copy over ssh)
```
scp -r *.* user@host:/directory
```




