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

# A) Create a user and it's library
sudo adduser THEUSER

# B) Do your python script with Flask (Eg the above file)
# Eg Place it in: /home/THEUSER/flask_app/thepython.py

# C) Maybe you have to do this (if it's not already there)
chown THEUSER thepython.py 
chmod +x thepython.py

# D) Create the service in systemd

# sudo nano /etc/systemd/system/THESNAME.service

[Unit]
Description=Flask application
After=multi-user.target

[Service]
Type=simple
User=THEUSER
WorkingDirectory=/home/THEUSER/flask_app
ExecStart=python3 /home/THEUSER/flask_app/thepython.py

[Install]
WantedBy=multi-user.target

# (for forking and oneshot apps use a different type in the config file above)


# E) Enable the service and reload stuff
sudo systemctl enable THESNAME.service
sudo systemctl daemon-reload
sudo systemctl restart THESNAME.service

# Check it
sudo systemctl status THESNAME.service

# Check the logs of systemd
journalctl -u THESNAME.service -S today


# Not necessary
sudo -H -u THEUSER pip3 install THELIB

# systemd: where to place the service file of you own systemd services
* Modifications done by system administrator (user) go into /etc/systemd/system/
    (files that ships in packages downloaded from distribution repository go into /usr/lib/systemd/)

```



