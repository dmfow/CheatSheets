#### print the 10 first
```python
for item in myList[:10]:
    print (item)
```
#### Print the 10 last
```python
for item in myList[-10:]:
    print (item)
```

#### Get the last item (do not remove it)
```python
last_item = next(reversed(a_list))
```

#### Get the last item and remove it
```python
last_item = a_list.pop()
```

#### Strip text from all words in an array
```python
thelist = [i.strip('.') for i in thelist]
```

#### Extract words from a text and put in a list
```python
thelist = text.split()
```

#### Sort the list
```python
# Sort alphabetically
thelist.sort()
# Sort on the word lenght
thelist.sort(key=lambda s: len(s))
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




