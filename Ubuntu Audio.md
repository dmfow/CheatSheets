## Audio fixes


#### No audio? Try
```
pulseaudio --start

# If it doesn't work try
sudo alsa force-reload
pulseaudio --start

```



#### Fix static noise when nothing is playing
```
# Check
cat /sys/module/snd_hda_intel/parameters/power_save

# Fix (until you reboot)
sudo su
echo 0 > /sys/module/snd_hda_intel/parameters/power_save
exit

```

#### Get info
```
inxi -SMA
```



#### Install sound packets
```
sudo apt install inxi

sudo apt-get install --reinstall alsa-base pulseaudio

```




