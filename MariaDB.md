Mariadb is an inplacement fork/clone of mysql, therefor a lot of mysql stuff is seen

#### Info about the DB
```
# Mariadb Datadirectory
  /var/lib/mysql

# Mariadb conf
  /etc/mysql/mariadb.cnf
# MySQL conf as this points to mariadb.cnf in two symlinks
  /etc/my.cnf

```
  
  
#### Handle the database
```
# restore database
   mysql -u [username] -p[password] < [filename].sql 
```

#### Login for mariadb
```
mariadb -u [username] -p
```


#### Install
```
# First intsall
sudo apt update
sudo apt upgrade
sudo apt install mariadb-server
# Then secure some basic stuff
sudo mysql_secure_installation
```





