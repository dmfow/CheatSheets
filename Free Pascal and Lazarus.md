## Functionality

#### Update / Paint
<b>Refresh</b> is there so you can override, do your unique updates and then call the inherited
, which eg is calling repaint.
 
<b>"Invalidate"</b> basically will call send a Paint message to the control after other messages in the queue have
been processed
It also invalidates the whole control and forces a complete update.
Windows will purge any pending invalidate after this gets processed so you don't get repeating painting 

<b>"Update"</b> what it suppose to do is basically force a WM_PAINT to the control directly if there
was a invalidate done but still sitting in the buffer, this is suppose to check for that check and force
the repaint and then remove the pending invalidate.
"Update" will also process all the other waiting messages and process any regions waiting.

<b>Repaint</b> just simple does the whole control

When you call Invalidate or InvalidateRect, Paint method will follow. 
Even more, Paint may be called by widgetset of some reason. It may happen that you call InvalidateRect, then other Invalidate or requirement to repaint is called, and Paint of the full area will come (i.e. repaint of the single rectangle specified in InvalidateRect never happen).

```
```



