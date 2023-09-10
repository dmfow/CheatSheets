## Free BSD stuff 

#### See release and disks
```
# Version
uname -a
# Relese
freebsd-version -u

# Disk
df -hi

```

#### Restart the filesystem
```
/etc/rc.d/devfs restart
# OR
 service devfs restart
```


## Various package commands
```
pkg bootstrap -f
pkg upgrade -f

pkg -d update -f
pkg update -f

pkg clean -ya
```


