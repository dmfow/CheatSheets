#### New empty dataframe
```python
df = pd.DataFrame()
```

## Rows
#### Info about the dataframe
```python
print(df.info())
print(df.shape)

# Column names
print(df.columns.values)

# Datatypes
print(df.dtypes)

```

#### Print the Nth row
```python
# The first row
print(myDF.iloc[0])

```

#### Print others
```python
# Without index
print(df.to_string(index=False))

```



#### Count rows in different ways
```python
# Show nr of rows containing a specific value
print(sum(df['myFruitColumn'] == 'apple'))
print(sum(df['myCountsColumn'] >= 11))

# Count apples, oranges and bananas with groupby
print(df.groupby(['myFruitColumn']).size())

# Show nr of rows
print(len(df.index))
# OR (inde 0 of the shape that gives a row,col tuple)
print(df.shape[0])
# OR
rows = len(df.axes[0])
# OR (slowest)
print(df.count())
```

## Columns
#### Show
```python
print(len(df.columns))
# OR
print(df.shape[1])
# OR
cols = len(df.axes[1])
```


#### Delete a column
```python
# 3 Different alternatives
del myDF['columnName']
myDF.pop('columnName')
myDF = myDF.drop(['columnName'], axis=1)

# Multi delete
myDF = myDF.drop(['columnName', 'anotherName'], axis=1)

# By index
df.drop(df.columns[0], axis=1, inplace=True)

# Delete na values
df = df.dropna()

# Recalculate the index
df = df.reset_index(drop=True)
```

## Display the Dataframe
```python
pd.set_option('display.max_rows', 5)
pd.set_option('display.max_columns', None)
pd.set_option('display.width', 1000)
pd.set_option('display.colheader_justify', 'center')
pd.set_option('display.precision', 3)
display(myDF)
```
## Merge identical column Dataframes
```python
import pandas as pd
myNewDF = pd.concat[(myDF, mySecondDF], axis=0)

# Horisontal merge
myNewDF = pd.concat[(myDF, mySecondDF], axis=1)
```

## Copy dataframe columns columns
```python
myDF['mycol'] = otherDF[['colname']].copy()
```


## Rename Dataframe
```python
# From test to TEST
myNewDF = myDF.rename(columns = {'test':'TEST', 'adi':'ADI', 'w23':'W24'}, inplace = True)
```

## Files
#### csv
```python
# Save
myDf.to_csv(filename, sep=";")

# Load
myDf = pd.read_csv(filename, sep=";", axis=0)

# Load with spearator regex (at least 2 blandspaces)
myDf = pd.read_csv(filename, sep="\s{2,}", axis=0)

# Treat values as na values
data = pd.read_csv(file,na_values=['*', '**', '***'])

# Only import some columns
data = pd.read_csv(filename, sep = "\t", usecols = ["Date", "Items", "Name", "SomeOtherCol"])


# Save to CSV file
Station1.to_csv(file1, sep=",", index=False, float_format="%.2f")

```
#### plain text (everything to 1 column)
```python
data = []
with open('filename', "r") as f_in:
  for line in map(str.strip, f_in):
    if now line
      continue
    data.append({"colname": line})
    
myDF = pd.DataFrame(data)

```
                              
#### Calculate
```python
.median()
.round(0)

# Standard deviation
.std()

# Unique occurences
.nunique()
```

#### String stuff
```python
.astype(str)
.str.slice(start = 0, stop= 6)

```

#### Re-type
```python
.astype(int)


# Print the types
print(df.dtypes)
```

#### Get different items from a DF
```python
Station1_may = Station1.loc[Station1["YR--MODAHRMN"].astype(str).str.slice(start = 0, stop= 6) == '201705']

```

#### Get different items from a DF
```python

# Print the top rows
myDF.head()
# Print the last rows
myDF.tail()

```

#### Time and date
```python
# Convert 'Date' from string to datetime format (example 'Date': ['20200101', '20200201', '20200301', '20200401'])
data['Date'] = pd.to_datetime(data['Date'], format='%Y%m%d')

# Extracting year, month, and day from the 'Date' column
data['Year'] = data['Date'].dt.year
data['Month'] = data['Date'].dt.month
data['Day'] = data['Date'].dt.day
```



#### Grouping and multiindex
```python
# Group a DF
df_grp = data.groupby(["Year","Month"]).mean(numeric_only=False)
# Get a subset DF based on the grouping index
df_march = df_grp.loc[2020,3]
# Take out one of the columns
mean_sweden = df_march["Sweden_Daily"]

# Loop through the groups
for idx, df_select in df_grp.groupby(level=[0, 1]):
    # Convert the month number to name
    s = datetime.date(1900, idx[1], 1).strftime('%B')

    # Add the data to the array
    a.append([idx[0], s, round(df_select["Sweden_Daily"].mean(),0)])

# More: https://pandas.pydata.org/docs/reference/groupby.html

```

#### Filter based on / Find data based on
```python
# Create 2 new dataframes based on an content in a column (in this case the column AnimalId)
newDF1 = df.loc[selected["AnimalId"] == 2998]
newDF2 = df.loc[selected["AnimalId"] == 2850]

#Identify the peak 
idx_max_Sweden = df['Sweden_Daily'].idxmax()
theDate = data.loc[idx_max_Sweden,"Date"].date()

# Get the sum of the Sweden_Daily values, when Date = March (m)
theSum = df.loc[df["Date"].dt.month==3]["Sweden_Daily"].sum()

```



