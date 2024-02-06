
#### Nice prints
```python
from pprint import pp
pp("Whatever Array or Json or other")
```

#### More prints
```python
print(f"The median: {myVar_median}")
print(f"The standard deviation of maximum temperature is {round(temp_max_std, 1)}")

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

#### Datatypes
```python
str
int, float, complex
list, tuple, range          
dict
set, frozenset
bool
bytes, bytearray, memoryview
NoneType


List: ["apple", "banana", "cherry"]
Tuple: ("apple", "banana", "cherry")
Range: range(6)
Dict: {"name" : "John", "age" : 36}
Set: {"apple", "banana", "cherry"}
Frozenset: frozenset({"apple", "banana", "cherry"})
Bytes: b"Hello"
Bytearray: bytearray(5)
Memoryview: memoryview(bytes(5))

x = "what"
print(type(x))
```



#### Match (Switch)
```python
# Integer ranges
    match temp:
        case _ if temp < -2:
            cold.append(temp)
        case _ if temp < 2:
            slippery.append(temp)
        case _ if temp < 15:
            comfortable.append(temp)
        case _ if temp >= 15:
            warm.append(temp)
# Integers
   match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"

# Tuples
# point is an (x, y) tuple
match point:
    case (0, 0):
        print("Origin")
    case (0, y):
        print(f"Y={y}")
    case (x, 0):
        print(f"X={x}")
    case (x, y):
        print(f"X={x}, Y={y}")
    case _:
        raise ValueError("Not a point")

# With a class
from enum import Enum
class Color(Enum):
    RED = 'red'
    GREEN = 'green'
    BLUE = 'blue'

color = Color(input("Enter your choice of 'red', 'blue' or 'green': "))

match color:
    case Color.RED:
        print("I see the red!")
    case Color.GREEN:
        print("The grass is green")
    case Color.BLUE:
        print("The ocean is blue")
```



#### Check if it is a function
```python
inspect.isfunction(fahr_to_celsius)

# Check that the function has one parameter
t_params = list(inspect.signature(fahr_to_celsius).parameters.keys())
assert len(t_params) == 1

# Check if a variable exist
if 'ones' in locals():
   # And print the value of the variable
   print(ones)

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


