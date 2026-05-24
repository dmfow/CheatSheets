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

#### Use ssh certificates instead of password
```
# Step 1 of 4 — Creating SSH Keys. Do it on your client/PC.
#   The private key will be called id_rsa and the associated public key will be called id_rsa.pub
#   run:
ssh-keygen

#   The program will prompt you to select a location for the keys that will be generated.Output
#   Choose the destination folder or use the deault by hitting enter
#   If you get "Overwrite (y/n)?" choose n and rething where the keys should be, keys already exist with the same name
#   Then you will get "Enter passphrase (empty for no passphrase):"
#     choose enter (no passphrase) for easier handling, but choose a passphrase for more secure
#      (an attacker can't use it directly if they get the hands on the key files
#    If you enter one, you will have to provide it every time you use this key
#      (unless you are running SSH agent software that stores the decrypted key)

# Step 2 of 4 - Copying an SSH Public Key to Your Server
# ssh-copy-id, it will login to the remote host and ask for the remote host username's password.
ssh-copy-id username@remote_host

# OR
cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# OR, manually
ssh username@remote_host
mkdir -p ~/.ssh
exit
cd ~/.ssh
scp ./id_rsa.pub username@remote_host:~/.ssh/

# OR, manually
cat ~/.ssh/id_rsa.pub
# copy the text ouput
ssh username@remote_host
mkdir -p ~/.ssh
# replace [public_key_string] with your copied text
echo [public_key_string] >> ~/.ssh/authorized_keys

# Step 3 of 4 - Testing - Authenticating to Your Server Using SSH Keys
ssh username@remote_host

# Step 4 of 4 - Disabling Password Authentication on Your Server
# Make sure you are on the server
sudo nano /etc/ssh/sshd_config
  PasswordAuthentication no
sudo systemctl restart ssh

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


