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

