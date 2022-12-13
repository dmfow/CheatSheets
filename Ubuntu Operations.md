#### automatic installation of security upgrades
```
sudo apt-get install unattended-upgrades
sudo dpkg-reconfigure  unattended-upgrades

# https://askubuntu.com/questions/578761/how-to-only-install-security-updates
```

#### Upgrade within release
```
sudo apt update
sudo apt upgrade
```

#### Upgrade Release (eg 20.04 LTS to 22.04 TLS)
```
sudo apt install update-manager-core
sudo apt update && sudo apt dist-upgrade
sudo do-release-upgrade
```

#### Check mail logs
```
cd /var/log
cat mail.log | grep status=sent | grep "<[A-Za-z0-9.@ ]*>"
cat mail.log | grep status=deferred | grep "<[A-Za-z0-9.@ ]*>"
cat mail.log | grep status=bounced | grep "<[A-Za-z0-9.@ ]*>"
```




## Firewall

## UFW firewall
```
sudo ufw status
```

## IP tables firewall

## Backup
Try "Timeshift"

## Disk usage (GUI)
Try "Disc usage Analyzer"









