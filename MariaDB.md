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





