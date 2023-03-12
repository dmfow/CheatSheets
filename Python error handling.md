#### Try - Except
```
try:
  cursorI.close()
except Exception as e:
  print(str(e))

  
# OR (not tested)  

try:
    pass
except Exception as e:
    if hasattr(e, 'message'):
        print(e.message)
    else:
        print(e)

# OR (not tested)  

try:
    raise Exception
except Exception as e:
    s,r = getattr(e, 'message', str(e)), getattr(e, 'message', repr(e))
    print ('s:', s, 'len(s):', len(s))
    print ('r:', r, 'len(r):', len(r))
    
# OR (not tested)  

try:
    # Open file in read-only mode
    with open("not_here.txt", 'r') as f:
        f.write("Hello World!")
except IOError as e:
    print("An error occurred:", e)
    
```
