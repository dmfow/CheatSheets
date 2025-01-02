#### Clear current command line commands from geting into the history file (.bash_history)
```
history -c

# Check where the history file reside
echo $HISTFILE

```



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


#### File rights
```
# Set user (and group) permission
# chown user:group file
chown user1:group2 myfile

# See what group a user belong to
groups user1

# Set read, write, execution rights - chmod number
# Change the file type
# Add/mark the file for execution
chmod +x myfile

# Add or remove for user (u), group (g), everyone (o)
chmod u+x myfile
chmod u=rwx,g+w,o-x myfile

# Use octal represenation
# See the rights from ls command
# number example: d|rwx|r-x|r-x
#                 File type|owner permission|group permission|everyone else
#                 Think byte, mark with 1 as permit: rwx = 111 = 4+2+1 = 7
#                                                    r-x = 101 = 4+0+1 = 5
#    750 => owner get rwx, group get rx, everyone else get nothing
#    Avoid 777
chmod 750 myfile
# Recursively
chmod -R 750 mydirectory



```


