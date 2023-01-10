#### Install Flask
```python
pip install Flask
```

#### Basic webservice
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def whatever():
    return 'Hello World!'

# The run from the Prompt    
$ export FLASK_APP=hello.py
$ flask run    
```



