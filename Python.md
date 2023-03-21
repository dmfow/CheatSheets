
#### Nice prints
```python
from pprint import pp
pp("Whatever Array or Json or other")
```


#### Import locally
```python
import filewithDef
# OR
from path import filewithDef
```


#### Check if a direcotry of file exist
```python
isExist = os.path.exists(path)
print(isExist)
```


#### Create a direcotry
```python
import os
os.mkdir(theDirPath)
```

#### File handling (read, write and append)
```python
# Write
file1 = open("myfile.txt", "w")
s = ["This is row 1 \n", "This is row 2 \n", "This is row 3"]
file1.writelines(s)
file1.close()
 
# Append
file1 = open("myfile.txt", "a")  # append mode
file1.write("A row \n")
file1.close()
 
# Read
file1 = open("myfile.txt", "r")
print(file1.read())
print()
file1.close()
```

#### Time
```python
import datetime
now = datetime.datetime.now()

print(now.strftime('%H:%M:%S'))
print(now.strftime('%Y-%m-%d %H:%M:%S'))
print(now.strftime('%H:%M:%S on %A, %B the %dth, %Y'))
```


