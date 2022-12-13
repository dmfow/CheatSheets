## Rows

#### Print the first row

print(myDF.iloc[0])

## Columns

#### Delete a column

del myDF['columnName']
myDF.pop('columnName')
myDF = myDF.drop(['columnName'], axis=1)

myDF = myDF.drop(['columnName', 'anotherName'], axis=1)

## Display the Dataframe

pd.set_option('display.max_rows', 5)
pd.set_option('display.max_columns', None)
pd.set_option('display.width', 1000)
pd.set_option('display.colheader_justify', 'center')
pd.set_option('display.precision', 3)
display(myDF)



