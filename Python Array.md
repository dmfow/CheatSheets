## Print

#### print the Nth first/last
```python
# The first row
print(myDF[0])

# The last row
print(myDF[-1])

Print the 10 first
for item in myList[:10]:
    print (item)

Print the 10 last
for item in myList[-10:]:
    print (item)

# Get the length
print(len(myarray))

```

## Add

### add
```python
# Initialize multiple empty list
l1 = []

# Initialize an empty list
l1, l2, l3, l4 = ([] for i in range(4))

# String or numbers
myList.append(strOrNumber)
myList.extend(strOrNumber)
myList.insert(index, strOrNumber)

# Arrays
myList = list1 + list2
myList.extend(list1)

```

## Get

### Get the last item (do not remove it)
```python
last_item = next(reversed(a_list))
```

#### Get the last item and remove it
```python
last_item = a_list.pop()
```

## To and from Array

#### Extract words from a text and put in a list
```python
thelist = text.split()
```

## Transform

#### Strip text from all words in an array
```python
thelist = [i.strip('.') for i in thelist]
```

#### Remove words shorter or longer than len
```python
# Keep longer (remove shorter)
thelist2=[x for x in thelist if len(x)>=5]
```

#### Remove words duplicate words with Pandas
```python
import pandas as pd
thelist2 = pd.Series(thelist).unique().tolist()
print ("The list of words is : " +  str(thelist2))

# Other ways https://datagy.io/python-remove-duplicates-from-list/
```


## Sort
#### Sort the list
```python
```

#### Sort the list
```python
# Sort alphabetically
thelist.sort()
# Sort on the word lenght
thelist.sort(key=lambda s: len(s))
```

#### String functions on the list
```python
.lower()
.strip()

```

#### Other functions on a list
```python
# Count he occurance of a specific value (in this case the number 1)
.count(1)

```


#### A point
```python
center = (59.5, 11.2)
print(center[0])
print(center[1])
```




