## 01 Coursera Basic pandas

Week 2: Introduction to Data Science with Python course


### Relevant snipets

#### Series: Declaring Series

*Different ways to declare Series: Dictionary*
```Python
sports = {'Archery': 'Bhutan',
          'Golf': 'Scotland',
          'Sumo': 'Japan',
          'Taekwondo': 'South Korea'}
s = pd.Series(sports)
```

*Different ways to declare Series: Series function*
```Python
s = pd.Series(['Tiger', 'Bear', 'Moose'], index=['India', 'America', 'Canada'])
```

*Combining both...*
```Python
sports = {'Archery': 'Bhutan',
          'Golf': 'Scotland',
          'Sumo': 'Japan',
          'Taekwondo': 'South Korea'}
s = pd.Series(sports, index=['Golf', 'Sumo', 'Hockey'])
```

#### Series: Querying Series

`iloc` and `loc`

```Python
sports = {'Archery': 'Bhutan',
          'Golf': 'Scotland',
          'Sumo': 'Japan',
          'Taekwondo': 'South Korea'}

s.iloc[3] -> 'South Korea'  # By index order
s.loc['Golf'] -> 'Scotland' # By index name
s[3]  -> 'South Korea'     # "Equivalent" to iloc... 
s['Golf']  -> 'Scotland'  # "Equivalent" to loc... 
```

**Put attention on the last two**...
If the Series has numeric index then using s[0] will cause an error... It is better to be specific-> s.iloc[0]
```Python
sports = {99: 'Bhutan',
          100: 'Scotland',
          101: 'Japan',
          102: 'South Korea'}
s[0]  -> Error!
s.iloc[0] -> 'Bhutan'
```

#### The DataFrame data structure: Declaring them...

*Union of series*
All of the series have the same Index, however, when they are concatenated those indexes will be the columns of the DataFrame.
The dataframe will have its own indexes. 

```Python
purchase_1 = pd.Series({'Name': 'Chris', 
                        'Item Purchased': 'Dog Food',
                        'Cost': 22.50})
purchase_2 = pd.Series({'Name': 'Kevyn',
                        'Item Purchased': 'Kitty Litter',
                        'Cost': 2.50})
purchase_3 = pd.Series({'Name': 'Vinod',
                        'Item Purchased': 'Bird Seed',
                        'Cost': 5.00})
df = pd.DataFrame([purchase_1, purchase_2, purchase_3], index=['Store 1', 'Store 1', 'Store 2'])
```

#### DataFrame: Queries

*Straightforward ways*
```Python
df.loc['Store 1'] -> Returns a series
df.loc['Store 1, 'Cost'] -> Returns also a series, first consult all elements with index = Store 1, and then with columns = 'Cost'
```

*Selecting all index, but only a few columns*
```Python
df.loc[:,['Name', 'Cost']]
```

*Conditionals*
```Python
df['Gold'] > 0    #Returns a dataframe with rows indicating True or False (not that useful)
only_gold = df.where(df['Gold'] > 0)   # Returns only the rows where the condition occurs (way more useful)
df[df['Gold'] > 0]   # Same as the previous one but more elegant.
```

*More complex conditional*
```Python
df[(df['Gold'] > 0) | (df['Gold.1'] > 0)]
```


#### Loading CSV
*The most common way*
```Python
df = pd.read_csv('data/olympics.csv')
```

*More advanced options (see documentation)*
```Python
df = pd.read_csv('data/olympics.csv', index_col = 0, skiprows=1)
```

#### DataFrame: Operations
*Transposing them: changing columns to row names*
```Python
df.T -> Dataframe 
```

*Counting*
```Python
df['Gold'].count()   #Count the number of rows
```

*Unique values*
```Python
df['SUMLEV'].unique()   #Returns an array with unique values.. 
```

*Droping values*
```Python 
df.drop('Store 1')  # Removes row in a Non-destructive way
del df['Name']      # Removes column destructively
```

*Droping NaN values*
```Python 
only_gold = only_gold.dropna()
```

*Filling NaN values*
```Python
df = df.fillna(method='ffill')  # See documentattion to see more methods... 
```

#### Indexing dataframes

*Setting a column as index*
```Python
df['country'] = df.index  #First 'saves' actual index
df = df.set_index('Gold')  # Switch index
```

*Setting more than one column as hierarchical index*  -> Similar to groupby
```Python
df = df.set_index(['STNAME', 'CTYNAME'])  # NO hay que usar forzosamente groupby

# This type of dataframes are indexed as:
df.loc['Michigan', 'Washtenaw County']

# or as:
df.loc[ [('Michigan', 'Washtenaw County'),
         ('Michigan', 'Wayne County')] ]
```

*Reseting index [from 0 to n]
```Python
df = df.reset_index()
```

*Sorting index 
```Python
df = df.sort_index()
```


*Selecting only some columns*
```Python
columns_to_keep = ['STNAME',
                   'CTYNAME',
                    ...
                   'POPESTIMATE2015']
df = df[columns_to_keep]
```




```Python

```





