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
   
# restore multiple databases (Existing databases on the target machine will be intact.)
mysql -u root -p < multi-databases.sql

# restore all databases (The SQL statements in the all-databases.sql file will recreate 
# all your databases in MariaDB. Existing databases on the target machine will be intact)
mysql -u root -p < all-databases.sql

# backup
mysqldump --all-databases --single-transaction > all_databases$(date +%F).sql  -u root -p
mysqldump -u root -p mysql user > user_table_dump$(date +%F).sql


# Cron (NOT TESTED)
sudo crontab -e
@daily mysqldump -u root database_name | gzip > database_name_`date +"\%Y-\%B-\%d_\%R"`.sql.gz
# delete old backups (delete all backups made in January on the first day of March)
0 0 1 3 * rm /[dir to backups]t/*January*.sql.gz

```

## Installation

#### Install
```
# First install
sudo apt update
sudo apt upgrade
sudo apt install mariadb-server
# Then secure some basic stuff
sudo mysql_secure_installation
```

#### Install for Pyhton
```
sudo apt install libmariadb3 libmariadb-dev
pip3 install mariadb

# SQLAlchemy
pip3 install mariadb SQLAlchemy

# Info about use in Python. See "Python MariaDB" file
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





