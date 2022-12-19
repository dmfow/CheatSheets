https://assets.ubuntu.com/v1/66fcd858-ubuntu-core-security-whitepaper.pdf
<br>
or
<br>
https://assets.ubuntu.com/v1/66fcd858-canonical-ubuntu-core-security-2018-11-13.pdf
<br>

https://wiki.ubuntu.com/Security/Features


#### automatic installation of security upgrades
```
sudo apt-get install unattended-upgrades
sudo dpkg-reconfigure  unattended-upgrades

# https://askubuntu.com/questions/578761/how-to-only-install-security-updates

# Run Once (-d = with debug)
sudo unattended-upgrades -d
```


#### remove unused packages
```
apt-get autoremove
```


#### Nmap
```
# Check port openings, install nmap
sudo apt install nmap
# Use it
nmap localhost

```

#### Netstat in Net-tools
```
# Check port openings, install netstat
sudo apt install net-tools
# Use it
sudo netstat -tunlp

```



