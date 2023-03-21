
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


#### For loop
```python
animals = ["cat", "dog", "horse"]
for x in animals:
  print(x)
  
# AN

for x in "banana":
  print(x)
  
animals = ["cat", "dog", "horse"]
for x in animals:
  print(x)
  if x == "dog":
    break
    
# AND

animals = ["cat", "dog", "horse"]
for x in fruits:
  if x == "dog":
    continue
  print(x)
  
# AND

# 0 to 3
for x in range(4):
  print(x)
  
# AND

# Not including 5 (from 1 to 4)
for x in range(1, 5):
  print(x)
  
# AND

# Step 3
for x in range(2, 30, 3):
  print(x)
  
# AND

list = ["Way", "too", "good"]
for index in range(len(list)):
    print(list[index])
    
    
```

#### While Loop
```python
count = 0
while (count < 7):
    count = count + 1
    print(count)
    
# AND

animals = ["cat", "dog", "horse"]
iter_obj = iter(animals) 
while True:
    try:
        item = next(iter_obj)
        print(item)
    except StopIteration:
        break
        
        
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```

#### ...
```python
```


