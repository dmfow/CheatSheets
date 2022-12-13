#### Check diskspace
```
df -h
# Check with with a mount point. Eg root
df -h /
# Check within a directory. Eg the home library
du -sh ~
```
#### Find a file

```
find LOCATION -name FILE_NAME
find ~ -name resolution-for-year-2022.txt
# OR
# OR
# OR

```

#### unzipp
```
# .zip
unzip thefile.zip

# .gz
gunzip < thefile.txt.gzip > newfile.txt

# .tar.gz
tar -xvf thefile.tzr.gz

# untar
untar thefile.tar
```

#### File handling
```
# Rename
mv file file2

# Move
mv file folder/file

# Copy
cp file file.bak

# Delete
rm file
# Delete multiple files
rm file file.bak
rm *.bak

```

#### Start the display (and window manager) - in this case lightdm (could be gdm, sddm etc)
```
sudo lightdm
```





