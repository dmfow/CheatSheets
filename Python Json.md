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

#### Clear/fix json strings
```
# Replace ' with "
jstring = jstring.replace("'", '"')

# Replace ' with " when escaped single qoutes exist (not tested). Replace only non escaped qoutes
import re
def replaceSingleQoutes(s):
        p = re.compile(r"(?<!\\)'")
        return p.sub('"', s)
jstring_corrected = replaceSingleQoutes(jstring)

# Remove trailing commas from json file (and remove tabs and new lines to make it a single string)
with open(filename, 'r') as f:
        s = f.read()
        s = s.replace('\t', '').replace('\n','').replace(',}', '}'). replace(',]', ']')
        jobj = json.loads(s)
```
#### Clear/fix json strings, and convert it into a dict
```
import ast
json_dict = ast.literal_eval(json_string)
```



#### json object to string
```
s = json.dumps(jdata)
```

