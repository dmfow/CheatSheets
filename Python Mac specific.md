## Mac specific

#### Prevent the Mac from sleep during a long run (not yet tested)
'''Python
# More info https://docs.python.org/3/library/subprocess.html
import sys
import subprocess


if 'darwin' in sys.platform:
    p1 = subprocess.Popen('caffeinate')
    
    # Your code here
    # ...
    # ...
    
    p1.stdout.close() 
    
'''
    
