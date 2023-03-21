## Requests module
https://docs.python-requests.org/en/latest/user/quickstart/

#### Basic usage API (and GET)
```python
import requests
r = requests.get('https://api.github.com/events')
# OR
# Don't do pass in clear text like this
r = requests.get('https://api.github.com/user', auth=('user', 'pass'))
# OR
r = requests.post('https://httpbin.org/post', data={'key': 'value'})
# OR
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get('https://httpbin.org/get', params=payload)


r.status_code
r.headers['content-type']
r.encoding
r.text
r.json()             # JSON
r.content            # Binary

# RAW / Stream
r = requests.get('https://api.github.com/events', stream=True)
r.raw
r.raw.read(10)
with open(filename, 'wb') as fd:
    for chunk in r.iter_content(chunk_size=128):
        fd.write(chunk)


```

#### POST
```python
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.post('https://httpbin.org/post', data=payload)
# OR
payload_tuples = [('key1', 'value1'), ('key1', 'value2')]
r1 = requests.post('https://httpbin.org/post', data=payload_tuples)
payload_dict = {'key1': ['value1', 'value2']}
r2 = requests.post('https://httpbin.org/post', data=payload_dict)
# => r1 give the same result as r2

# JSON
import json
url = 'https://api.github.com/some/endpoint'
payload = {'some': 'data'}
r = requests.post(url, data=json.dumps(payload))

```

#### Headers
```python
url = 'https://api.github.com/some/endpoint'
headers = {'user-agent': 'my-app/0.0.1'}
r = requests.get(url, headers=headers)
```


#### Certificates
```python
# Local cert matching the websites
requests.get('https://github.com', verify='/path/to/certfile')

requests.get('https://kennethreitz.org', verify=False)
```

#### Create an imaga from the binary data
```python
from PIL import Image
from io import BytesIO
i = Image.open(BytesIO(r.content))
```



