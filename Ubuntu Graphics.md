#### [Check the gpu/video driver](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#check-gpuvideo-driver)
1. [Currently used graphics driver](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#currently-used-graphics-driver)
2. [Graphic cards in the system](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#graphic-cards-in-the-system)
3. [See installed nvidia packages](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#see-installed-nvidia-packages)
4. [See if cc is installed (if not install the toolkit)](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#see-if-cc-is-installed-if-not-install-the-toolkit)

#### [GPU utilization](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#gpu-utilization-1)
5. [Current (momentan) utilization of an Nvidia GPU](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#current-momentan-utilization-of-an-nvidia-gpu)

#### [GPU actions](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#gpu-actions-1)
6. [Reset the memory](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#reset-the-memory)

#### [Installation](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#installation-1)
7. [Driver](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#driver)
8. [More recent driver](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#more-recent-driver)
9. [Problem with the installation - purge (remove) existing packages (this might crash stuff!)](https://github.com/dmfow/CheatSheets/blob/main/Ubuntu%20Graphics.md#problem-with-the-installation---purge-remove-existing-packages-this-might-crash-stuff)


## Check gpu/video driver
### Currently used graphics driver
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
#### See if cc is installed (if not install the toolkit)
```
nvcc --version
```

## GPU utilization
#### Current (momentan) utilization of an Nvidia GPU
```
nvidia-smi
```

## GPU actions
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

