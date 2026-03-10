


#### Unauthorized app
```
System Preferences -> Security & Privacy -> click “Open ABC## anyway”

Maybe - Click the lock
 + Enter your Administrators Username and Password
```


#### Unauthorized app - Catalina
```
xattr -d com.apple.quarantine <app-path>
```

#### Stop your Mac from sleeping
```
# In the terminal run
caffeinate
  # caffeinate switches
  caffeinate -d : Also prevent the display from sleeping
  caffeinate -t 3600 : Prevent a specific time (this is 1 hour)
  caffeinate -i : Will enable control-command-Q to sleep (or apple-menu/sleep)
  caffeinate -s : Prevent sleep, but only if it is plugged-in
# GUI
Go to: System settings/Lock screen/Turn display off when inactive (+choose "never" in the drop down)

```
  
