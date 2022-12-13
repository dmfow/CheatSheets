## Rows

#### Print the first row
```python
print(myDF.iloc[0])
```

## Columns

#### Delete a column
```python
del myDF['columnName']
myDF.pop('columnName')
myDF = myDF.drop(['columnName'], axis=1)

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
## Merge Dataframes
```python
myDF.update(mySecondDF, raise_conflict=True)
```

