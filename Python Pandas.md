## Rows
#### Info about the dataframe
```python
print(df.info())
print(df.shape)
```

#### Print the first row
```python
print(myDF.iloc[0])

# Show nr of rows
print(len(df.index))
# OR (inde 0 of the shape that gives a row,col tuple)
print(df.shape[0])
# OR
rows = len(df.axes[0])
# OR (slowest)
print(df.count())

# Show nr of rows containing a specific value
print(sum(df['myFruitColumn'] == 'apple'))
print(sum(df['myCountsColumn'] >= 11))

# Count apples, oranges and bananas with groupby
print(df.groupby(['myFruitColumn']).size())
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

## Rename Dataframe
```python
# From test to TEST
myNewDF = myDF.rename(columns = {'test':'TEST', 'adi':'ADI', 'w23':'W24'}, inplace = True)
```
                              
                              

