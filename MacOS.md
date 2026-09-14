


#### Unauthorized app
```
System Preferences -> Security & Privacy -> click “Open ABC## anyway”

Maybe - Click the lock
 + Enter your Administrators Username and Password
```

#### Better prompt in the terminal
```
# ~/.zshrc or (/etc/zshrc , not tested)
#   %n is your account username.
#   %m is your Mac's model name.
#   %1~ means the current working directory path, where the ~ strips the $HOME directory location.
#   %# means that the prompt will show # if the shell is running with root (administrator) privileges and % if it doesn't. 
nano ~/.zshrc 
 PS1="%n@%m %1~ %#"
source ~/.zshrc

# Show only where you are
 PS1='%~ $ '
# 
 PS1='\u@\H:\w$'
# Just username 
PS1='%n:~$'
# Date or time
PS1='%n:%D:~$'
PS1=='%n@%T>~$'


# More acrynoms: https://zsh.sourceforge.io/Doc/Release/Prompt-Expansion.html

# Other suggestions (not tested)
#Display date and time right aligned in the window on the prompt row
RPROMPT='%D @ %T'
# Prompt color (the number is from 256 different 8-bit colors table)
PROMPT='%F{cyan}%n%f:~$'
PROMPT='%F{51}%n%f:~$'
# Set default
PROMPT="%n@%m %1~ %#"

# With export
export PS1='\u@\H:\w$'
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
# Install with brew (https://brew.sh). This will "listen" to python3.X command

# Possibility to make an alias in the .zprofile to use the python command (and pip command) to run the python/pip of your choice
alias python="[path to the python execution file of your choice]"
alias pip="[path to the python execution file of your choice]"
```

#### Network
```
# Add persistant routes
#   networksetup -setadditionalroutes [name] [destination], [subnet mask], [gateway]
networksetup -setadditionalroutes Wi-Fi 192.168.50.0 255.255.255.0 192.168.1.1

# See used ports
sudo lsof -iTCP -sTCP:LISTEN -P -n

#  See routes
netstat -rn

# More on networksetup
#  https://support.apple.com/en-euro/guide/remote-desktop/apdd0c5a2d5/mac
#  https://www.unix.com/man_page/osx/8/networksetup/
```


