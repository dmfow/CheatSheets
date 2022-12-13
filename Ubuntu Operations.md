#### automatic installation of security upgrades
```
sudo apt-get install unattended-upgrades
sudo dpkg-reconfigure  unattended-upgrades
```
https://askubuntu.com/questions/578761/how-to-only-install-security-updates

#### Upgrade within release
sudo apt update
sudo apt upgrade

#### Upgrade Release (eg 20.04 LTS to 22.04 TLS)
sudo apt install update-manager-core
sudo apt update && sudo apt dist-upgrade
sudo do-release-upgrade

