#### Install Flask
```python
pip install Flask
pip install waitress

# Don't run it as root (which prohibits it to use port 1-1024). Instead use a loadbalancer or reverse proxy infront.
```

#### Basic webservice
```python
# Eg call this file: start.py

from flask import Flask
app = Flask(__name__)

@app.route('/')
def whatever():
    return 'Hello World!'
    
if __name__ == '__main__':
    from waitress import serve
    serve(app, host="0.0.0.0", port=8080)
    #app.run()


# The run from the Prompt    
$ python3 start.py
# OR
# The run from the Prompt    
$ export FLASK_APP=start.py
$ flask run    
```


#### Run Flask as a service
```
# => Replace THEUSER with your username
# => Replace THESNAME with the name of your new service

# A)
# Create a user and it's library
sudo adduser THEUSER

# B)
# ut your pythonscript with Flask in /home/THEUSER/flasklib
# Eg the above file. Call it eg thepython.py 

# C)
# Maybe you have to do (if it's not already there)
chown THEUSER thepython.py 
chmod +x thepython.py

# D)
# Create the service in systemd
# sudo nano /etc/systemd/system/THESNAME
[Unit]
Description=Flask application
After=multi-user.target

[Service]
Type=simple
User=THEUSER
WorkingDirectory=/home/theuser/flasklib
ExecStart=python3 /home/theuser/flasklib/thepython.py

[Install]
WantedBy=multi-user.target


# E)
sudo systemctl enable THESNAME.service
sudo systemctl daemon-reload
sudo systemctl restart THESNAME.service


```



