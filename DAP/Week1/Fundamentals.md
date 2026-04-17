Commands:

#### 1. pd.read_CSV()
```python
df = pd.read_csv('/Users/devaggarwal/sem6 lab/DAP/dataset.csv')
```

#### 2. df.head()
```python
# shows the top 5 entries of the dataframe
df.head()
```

#### 3. df.shape
```python
# shows the dimension of the data set
df.shape
```

#### 4. df.columns
```python
# shows all the columns in the dataset
df.columns
```

#### 5. df.dtypes
```python
# this shows the datatypes of all the coloums
df.dtypes
```

#### 6. df.info()
```python
# this gives info of the dataset
df.info()
```

#### 7. df['column name']
```python
df['geo']
```

#### 8. df['column1', 'column1', 'column1']
```python
df[['geo', 'name', '2096']]
```

#### 9. df.loc[10]
```python
# this is used for indexing the dataframe
df.log[99]
# above code gives the row that is at 99th index
```

#### 10. df.tail(n=5)
```python
df.tail(n=3)
# this gives the last 3 rows of the dataset
```

#### df.loc[[5, 6, 7]]
```python
# this gives multiple rows
df.loc[[5, 6, 7]]
```
![[Pasted image 20260402233646.png]]


#### subsetting of columns
```python
df.loc[:, ['geo', 'name']] # this uses name of the columns for indexing
# or 
df.iloc[:, [1, 5]] # this uses numeric indexers of the columns
```

