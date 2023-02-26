

#### Info about the DB
```
# MySQL Datadirectory
  /var/lib/mysql

# Mariadb conf
  /etc/mysql/mariadb.cnf
# MySQL conf
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





