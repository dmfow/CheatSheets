## Commands

#### String
First position often start at 1 instead of 0 as in several languages
```
# Get the 5th word in a string
s := ExtractWord(5,Text,[' ']);

# Substring (the first two characters)
newstring := copy(myString,1,2);

# Exist in string (i will be 6, start on 1)
s:='news book';
i:=pos('book',s);

```

#### Json
https://www.getlazarus.org/json/
```
```

#### Stringgrid
```
# Example code
https://wiki.freepascal.org/TStringGrid
# Grids Reference Page
https://wiki.freepascal.org/Grids_Reference_Page
```

#### Sleep in Console app
```
https://forum.lazarus.freepascal.org/index.php?topic=31526.0
https://forum.lazarus.freepascal.org/index.php?topic=51763.0
```

#### Process messages in Console app
```
https://forum.lazarus.freepascal.org/index.php?topic=13462.0
```

## Functionality

#### Update / Paint
<b>Repaint</b> 
Repaint just simple does the whole control
Repaint will handle all messages that have to do with painting invalidate, paint etc at the time it will be called. I used it to show progress updates on screen with out calling processmessages.

<b>Refresh</b> 
It is called by the end user to refresh the area of a control usually when there are property changes that do not refresh the control.
It is there so you can override, do your unique updates and then call the inherited
, which eg is calling repaint.
 
<b>Invalidate</b> 
Basically will call send a Paint message to the control after other messages in the queue have
been processed
It also invalidates the whole control and forces a complete update.
Windows will purge any pending invalidate after this gets processed so you don't get repeating painting 

Example InvalidateRect, The invalidated areas accumulate in the update region until the region is processed when the next WM_PAINT message occurs or until the region is validated by using the ValidateRect or ValidateRgn function.
source
https://msdn.microsoft.com/en-us/library/windows/desktop/dd145002(v=vs.85).aspx
In short it does not matter how ofter you call invalidaterect it will accumulate the rect in to single region which will be passed to the next paint method. Used to speed things up.



<b>Update</b> 
What it suppose to do is basically force a WM_PAINT to the control directly if there
was a invalidate done but still sitting in the buffer, this is suppose to check for that check and force
the repaint and then remove the pending invalidate.
"Update" will also process all the other waiting messages and process any regions waiting.


When you call Invalidate or InvalidateRect, Paint method will follow. 
Even more, Paint may be called by widgetset of some reason. It may happen that you call InvalidateRect, then other Invalidate or requirement to repaint is called, and Paint of the full area will come (i.e. repaint of the single rectangle specified in InvalidateRect never happen).

<b>Use</b>
As an end user - repaint
As a component writer - Invalidate


```
```



