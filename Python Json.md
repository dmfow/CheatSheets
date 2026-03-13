## JSON (and Pandas)

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
data_dict = [{'Name':{'firstname':'Karen','lastname':'consert'}, 'year':'1750'},{'name':{'firstname':'Bob','lastname':'bigtree'}, 'year':'1751'}]

# Normalize all
df = pd.DataFrame.from_dict(pd.json_normalize(data_dict), orient='columns')

# Normalize only the first level (0 index levels)
df = pd.DataFrame.from_dict(pd.json_normalize(data_dict), orient='columns', max_level=0)
```

#### Normalize json object into a Pandas Dataframe
```
# Normalize some fields and in certain order
data = [{
        "company":"nike",
        "tagline": "just do it",
        "sells": {"shoes": "jordan"},
        "departments": [
          {"name":"shoes", "revenue":50},
          {"name":"shirts", "revenue":20}
        ]
}]

df = pd.DataFrame.from_dict(pd.json_normalize(data), "department", ["company", "tagline", ["sells", "shoes"]])
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

