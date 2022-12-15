#### [Check driver](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#check-driver-1)
1. [Currently used graphics driver](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#currently-used-graphics-driver-1)
2. [Graphic cards in the system(https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#graphic-cards-in-the-system-1)
3. [See installed nvidia packages(https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#see-installed-nvidia-packages)
<br>
#### [Reset and do stuff](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#reset-and-do-stuff-1)
1. [Reset the memory](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#reset-the-memory)
<br>
#### [Installation](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#installation-1)
1. [Driver](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#driver)
2. [More recent driver]()
3. [Problem with the installation - purge (remove) existing packages (this might crash stuff!)]()


## Check driver
#### Currently used graphics driver
```
sudo lshw -c video

# If Nvidia
nvidia-smi
# OR
grep "X Driver" /var/log/Xorg.0.log

# More Nvidia
find /usr/lib/modules -name nvidia.ko
find /usr/lib/modules -name nvidia.ko -exec modinfo {} \;

```

#### Graphic cards in the system
```
lspci -nn | grep -E 'VGA|Display'
# OR
lspci | grep VGA
# OR
lspci -vnn | grep VGA
```
#### See installed nvidia packages
```
dpkg -l | grep -i nvidia
```

## Reset and do stuff
#### Reset the memory
```
nvidia-smi
nvidia-smi --gpu-reset -i "gpu ID"
# OR
fuser -v /dev/nvidia*
kill -9 "PID"
```


## Installation

#### Driver
```
apt search nvidia-driver
sudo apt update
sudo apt upgrade
ubuntu-drivers devices
sudo apt install [driver_name]
# Example: sudo apt install nvidia-driver-495
sudo reboot
```

#### More recent driver
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt upgrade
ubuntu-drivers devices
sudo apt install [driver_name]
# Example: sudo apt install nvidia-driver-470
sudo reboot
```

#### Problem with the installation - purge (remove) existing packages (this might crash stuff!)
```
sudo apt-get remove --purge '^nvidia-.*'
sudo reboot
# Redo the installation

# OR
sudo dpkg -P $(dpkg -l | grep nvidia-driver | awk '{print $2}')
sudo apt autoremove
# Redo the installation
```
#### Nvidia driver download
https://www.nvidia.com/Download/index.aspx?lang=en-us

