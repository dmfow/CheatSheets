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



