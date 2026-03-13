## Json (and pandas)

#### use the following imports
```
import pandas as pd
import json
```

#### Read well structured json file
```
df = pd.read_json(filename)
```


#### Dict into a Pandas Dataframe
```
data = [{'name':'Karen', 'year':'1750'},{'name':'Bob', 'year':'1751'}]
df = pd.DataFrame.from_dict(data, orient='columns')
```

#### Normalize dict into a Pandas Dataframe
```
data = [{'Name':{'firstname':'Karen','lastname':'consert'}, 'year':'1750'},{'name':{'firstname':'Bob','lastname':'bigtree'}, 'year':'1751'}]
df = pd.DataFrame.from_dict(pd.json_normalize(data), orient='columns')
```

#### String to Pandas Dataframe via converting to json object
```
jstring = '{"001":{'firstname':'Karen','lastname':'consert'}, "002":{'firstname':'Bob','lastname':'bigtree'}}'
jdata = json.loads(jstring)
df = pd.DataFrame(jdata).T
```

#### json object to string
```
s = json.dumps(jdata)
```

