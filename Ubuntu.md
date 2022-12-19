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
  # Examples
  find ~ -name resolution-for-year-2022.txt
  find . -name "*.png"
  find ~ -type f -empty
# OR to find a file with a specific text
grep -irl "text" <dir>
    # i - for case insensitive search
    # r - for recursive search inside subdirectories
    # l - to show only the file names, not the matching lines 
    # Exempel
    grep -irl "for" .

# Find large files
sudo find ~ -type f -printf '%s\t%p\n' | sort -n | tail -2
find $HOME -type f -printf '%s %p\n' | sort -nr | head -10
find / -size +100M -ls
find $DIRECTORY -type f -exec ls -s {} \; | sort -n | tail -n 5

sudo du -a /home | sort -n -r | head -n 10
sudo du -a | sort -n -r | head -n 10
du -hs * | sort -rh | head -n 10
du -Sh | sort -rh | head -n 10
sudo du -hsx * | sort -rh | head -10

ls -lSh /bin | head -5
ls -lah --sort=size
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
# Delete a directory and all directories and files within
rm -rf lampp

```

#### Start the display (and window manager) - in this case lightdm (could be gdm, sddm etc)
```
sudo lightdm
```





