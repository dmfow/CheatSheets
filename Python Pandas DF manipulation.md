## Make a new DF
```
# Make a new standalone DF
newDf = df_first.copy(deep=True)

# Matching specific value
newDf = df.loc[df["Year"] == 2024]

# Transpose a Row to a list
stocks = ['sp500','nasdaq']
row = df.iloc[0]
df_temp = row[stocks].transpose().to_frame(name="value").sort_values(by=["value"], ascending=False)

# If the names are in the index. Take the 10 first stocks and convert it to a list
stocklist = df.head(10).index.to_list()

# Make a new DF where a row with the stockname in the col stocknames match a list of stocks (stocklist)
df_selected = df_stocks[df_stocks['stocknames'].isin(stocklist)]

# Pandas series, to a list
s = pd.Series([1, 2, 3])
list = s.to_list()
# OR
idx = pd.Index([1, 2, 3])
list = idx.to_list()

```

## Selecting
#### Rows
```python
mask = (df['SKU_A'] == df['SKU_B'])
newDf = df[mask]
# OR
newDf = df[df['SKU_A'] == df['SKU_B']]
# OR
newDf = df.query('SKU_A == SKU_B')

# Not equal
newDf = df[df['SKU_A'] != df['SKU_B']]
# OR
df = df[~(df['SKU_A'] == df['SKU_B'])]
# OR
df = df.query('SKU_A != SKU_B')

# NAN
NaN == NaN is False.
NaN != NaN is True.
Any comparison of a non-NaN value with NaN (e.g., 'X453' == np.nan or 'X453' != np.nan) results in False for == and True for !=

# More advance to handle nan values
both_nan = df['SKU_A'].isna() & df['SKU_B'].isna()
both_not_nan_and_equal = df['SKU_A'].notna() & df['SKU_B'].notna() & (df['SKU_A'] == df['SKU_B'])
newDf = df[both_nan | both_not_nan_and_equal]

```

#### Cols
```python
```


## Insert
```python
# Insert last (append)
df.loc[len(df)] = [name, address, variable2]

# Inser a new column
df["myCol"] = df_1["cars"]+df_1["bikes"]

```

## Insert to a list
#### Take a DF with one column and choose rows by index and insert into a list
```python
myList.append(df.iloc[last:last+nr+add])

# Append a list as a row in a list (as Pandas series, per list row)
myList.append(pd.Series(anotherList))
```


## Delete

#### Delete a row
```python
# Remove the first row
df.drop(index=df.index[0], axis=0, inplace=True)

# Remove the last row
df.drop(df.tail(1).index, inplace = True)

# Delete rows from the beginning to first non-NAN value
idx = df.first_valid_index()
df = df.iloc[idx-1:]

# Delete NA values
df = df.dropna()

# All rows where age is 21
rows = df[df["Age"] == 21].index
df.drop(rows, inplace=True)

# All rows where age is 20-22
rows = df[(df["Age"] >= 20) & (df["Age"] <= 22)].index
df.drop(rows, inplace=True)

# All rows where Department = HR
rows = df[df["Department"] == "HR"].index
df.drop(rows, inplace=True)

# All rows where column matches something in a list
rows = df[df["Department"].isin(["HR", "Finance"])].index
df.drop(rows, inplace=True)

# All rows where Department is not IT
rows = df[df["Department"] != "IT"].index
df.drop(rows, inplace=True)

# Remove rows where column values are not the same, but keep if a column value is empty (col called V2 and V3)
# It take the value of V2 if V3 is empty and then compare, but in the end takes the original values
newDf = df[df.V3.fillna(df.V2).eq(df.V2)]

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
```

## Recalculate
```python
# Recalculate the index
df = df.reset_index(drop=True)
```

## Merge

## Merge identical column Dataframes
```python
import pandas as pd
myNewDF = pd.concat[(myDF, mySecondDF], axis=0)

# Horisontal merge
myNewDF = pd.concat[(myDF, mySecondDF], axis=1)
```
## Copy

## Copy dataframe columns columns
```python
myDF['mycol'] = otherDF[['colname']].copy()
```

## Numeric
#### 
```python
# Multiply all col values with a formula in a function
def multiply2(number):
        return 2 * number
df.iloc[:, 4:cols] = df.iloc[:, 4:cols].apply(multiply2)
```


