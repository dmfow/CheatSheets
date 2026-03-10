## Mac specific

#### Prevent the Mac from sleep during a long run (not yet tested)
```
import sys
import subprocess


if 'darwin' in sys.platform:
    p1 = subprocess.Popen('caffeinate')
    
    # Your code here
    # ...
    # ...
    
    # Close and cleanup
    p1.stdout.close()
    if p1.stderr:
       p1.stderr.close()
    p1.stdin.close()
    p1.wait()

    # More info on subprocess: https://docs.python.org/3/library/subprocess.html

    # Info on this page suggest terminate or kill (and that close is not sufficient):
    #    https://stackoverflow.com/questions/9585874/proper-way-of-re-using-and-closing-a-subprocess-object
    p1.terminate()
    p1.kill()

```
    
