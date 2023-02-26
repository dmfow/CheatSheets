Mariadb is an inplacement fork/clone of mysql, therefor a lot of mysql stuff is seen

#### Login for mariadb
```
mariadb -u [username] -p
```

#### Check users
```
SELECT User, Host FROM mysql.user WHERE Host <> 'localhost';
```

## Config

#### Info about the DB
```
# Mariadb Datadirectory
  /var/lib/mysql

# Mariadb conf
  /etc/mysql/mariadb.cnf
# MySQL conf as this points to mariadb.cnf in two symlinks
  /etc/my.cnf
```


#### Network issus
```
# Look into all these files (for bind-address)
# The MariaDB/MySQL tools read configuration files in the following order:
# 0. "/etc/mysql/my.cnf" symlinks to this file, reason why all the rest is read.
# 1. "/etc/mysql/mariadb.cnf" (this file) to set global defaults,
# 2. "/etc/mysql/conf.d/*.cnf" to set global options.
# 3. "/etc/mysql/mariadb.conf.d/*.cnf" to set MariaDB-only options.
# 4. "~/.my.cnf" to set user-specific options.

# Change config, and then
systemctl restart mariadb.service
ss -patn | grep 3306
```




## Backup & restore
  
#### Handle the database
```
# restore database
   mysql database -u [username] -p[password] < [filename].sql 
```

## Installation

#### Install
```
# First intsall
sudo apt update
sudo apt upgrade
sudo apt install mariadb-server
# Then secure some basic stuff
sudo mysql_secure_installation
```

## Error messages

```
# mysql_secure_installation
/usr/bin/mysql_secure_installation: 218: cannot create .mysql.1024: Permission denied
/usr/bin/mysql_secure_installation: 220: cannot open .mysql.1024: No such file
Password update failed!
Cleaning up...
# Solution, run as sudo, see above
```





