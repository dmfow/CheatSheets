## Rows

#### Print the first row

print(myDF.iloc[0])

## Columns

#### Delete a column

del myDF['columnName']
myDF.pop('columnName')
myDF = myDF.drop(['columnName'], axis=1)

myDF = myDF.drop(['columnName', 'anotherName'], axis=1)

