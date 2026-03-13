


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
  caffeinate -w [PID] : Stay awake until a specific process ID exits
# GUI
Go to: System settings/Lock screen/Turn display off when inactive (+choose "never" in the drop down)

```
  
#### Python
```
# These three alternative installs different Python libraries
# Default and connected to xcode. Don't remove this. Might be older then the last release. This will "listen" to python3 command
# Install from python.org. This will "listen" to python3.X command
# Install with brew. This will "listen" to python3.X command

# Possibility to make an alias in the .zprofile to use the python command (and pip command) to run the python/pip of your choice
alias python="[path to the python execution file of your choice]"
alias pip="[path to the python execution file of your choice]"
```




