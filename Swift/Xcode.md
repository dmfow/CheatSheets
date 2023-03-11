## Package.resolved file is corrupted or malformed
```
find ./ -name Package.resolved 2>&1 | grep -v "Permission denied" 2>&1 | grep -v "not permitted" >&1 | grep -v "No such file"
rm /[PATH TO PACKAGE]/Package.resolved
```
