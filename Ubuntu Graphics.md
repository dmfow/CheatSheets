
#### Currently used graphics driver
```
sudo lshw -c video
```

#### Graphic cards in the system
```
lspci -nn | grep -E 'VGA|Display'
# OR
lspci | grep VGA
# OR
sudo lshw -c video
# OR
lspci -vnn | grep VGA
```
#### See installed nvidia packages
```
dpkg -l | grep -i nvidia
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

#### Problem with the installation - purge (remove) existing packages
```
sudo apt-get remove --purge '^nvidia-.*'
sudo reboot
# Redo the installation
```

