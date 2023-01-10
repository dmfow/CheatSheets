#### Install Flask
```python
pip install Flask
pip install waitress
```

#### Basic webservice
```python
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
$ export FLASK_APP=hello.py
$ flask run    
```



