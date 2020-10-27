## 03 Coursera Advanced Pandas

Week 3: Introduction to Data Science with Python course

### Relevant snipets

#### Merging Dataframes

*Union or outer*
It merges all data, each with the same index. 
```Python
pd.merge(df_1, df_2, how='outer', left_index = True, right_index=True)
```

*Intersection or inner*
Only data that appears in both df
```Python
pd.merge(df_1, df_2, how='inner', left_index = True, right_index = True)
```

*From left or right*
Useful when one DF has more information we want to keep, and just add some specific information from the other df

```Python
pd.merge(staff_df, student_df, how = 'left', left_index = True, right_index = True)
# or
pd.merge(staff_df, student_df, how = 'right', left_index = True, right_index = True)
```

*Mixing index*
Sometimes the index do not match, and we have to indicate which columns are set to join.
```Python
df_1 = df_1.reset_index()
df_2 = df_2.reset_index()
pd.merge(df_1, df_2, how = 'left', left_on = 'Name', right_on = 'Name')
```

*Repeated columns*
Sometimes when two DF are merged some column names are repeated, but the information they contain is different, in this case pd set the sufix _x and _y.

*Merging through more than 1 index*
A list of column names is used:
```Python
pd.merge(staff_df, student_df, how = 'inner', left_on=['First Name', 'Last Name'], right_on = ['Firstm Name', 'Last Name'])
```

#### Idiomatic Pandas. Making pandas pandorable

*Filtering data, droping NaN, setting multi-index and renaming columns in a pandorable way:*
```Python
(df.where(df['SUMLEV']==50) # Deja igual a las filas que cumplen la condición (True) y a las que no les asigna NaN
     .dropna()              # Elimna las que valen NaN (es decir, que no cumplen la condición dad)
     .set_index(['STNAME','CTYNAME'])  # Con las que sobran establece un multi-índice Nombre de Estado y County
     .rename(columns={'ESTIMATESBASE2010': 'Estimates Base 2010'}) ) # Renombra columnas
```

*Apply*
Sometimes it is better to define a set of operations to be applied as a specific python function, and then use the `apply` method with the DF

```Python
def min_max(row):   #Input is a row.... can be a columns too
    data = row[['POPESTIMATE2010', ..., 'POPESTIMATE2015']]  # Selects specific columns of the row... 
    return pd.Series({'min': np.min(data), 'max': np.max(data)})
    
df.apply(min_max, axis=1) # See resulting table in code... Axis 1 is operations over rows...
```
There are two other ways to implement this same function with different styles.

#### Group by

*Iterating over group by*
```Python
for group, frame in df.groupby('STNAME'):
    avg = np.average(frame['CENSUS2010POP'])
    print('Counties in state' + group + 'have an average population of' +  str(avg))
```

*An advanced way to use group by + a function*
Instead of giving to df.groupby() a column name to reorganize the frame index, we can provide a function. The output of this function will be the index of the frame (although this is not very intuitive)

```Python
def fun(item):   #the index name
    if item[0] < 'M':   #first letter of word
        return 0
    if item[0] < 'Q':   
        return 1
    else:
        return 2

#Iterating throug frames
for group, frame in df.groupby(fun):
    print('There are' + str(len(frame)) + 'records in group' + str(group) + 'for processing'
```

#### Method `agg()`
Aggregation functions

*Computing average value for all columns*
```Python
df.groupby('STNAME').agg(np.average)
```

*Computing average for a single column*
```Python
df.groupby('STNAME').agg({'CENSUS2010POP': np.average})
```

*Agrupando por el mismo indice,... aplica para multiindex DF*
level = 0 refiere a agrupar con base en el primer indice, level = 1, al segundo y etcetera.

```Python
df.set_index('STNAME').groupby(level=0)['CENSUS2010POP'].agg(avg = np.average, sum = np.sum)).head()
```
Of course this only applies when the used index is the same for several data, otherwise is not useful.


#### Scales
Useful for categorical data.

*Defining it:*
```Python
df['Grades'].astype('category').head()
```

*Defining ordinal categorical data:*

```Python
grades = df['Grades'].astype(CategoricalDtype(categories=['D', 'D+', 'C-', 'C', 'C+', 'B-', 'B', 'B+', 'A-', 'A', 'A+'],
                                              ordered=True)
```

*Dividing data into bins with `cut`*

```Python
df = pd.read_csv('data/census.csv')
df = df.set_index('STNAME').groupby(level=0)['CENSUS2010POP'].agg(avg = np.average)

# The following code divides the data into 10 different bins:
pd.cut(df['avg'],10)
```

*Using labels with cut*
```Python
pd.cut(df['avg'],10, labels = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
```


#### Pivot Tables
Conver the data from the way it is organized into the DF to a pivot table.
The pivot table is created based on three arguments:  values (inside the table), index, and columns. Additionally an aggregation function is set.
```Python
df.pivot_table(values='(kW)', index='YEAR', columns='Make', aggfunc=np.mean)

# More complicated
df.pivot_table(values='(kW)', index='YEAR', columns='Make', aggfunc=[np.mean,np.min], margins=True)
```


#### Dates

*Timestamp and Periods*
```Python
pd.Timestamp('9/1/2016 10:05AM')  # -> Useful for index
pd.Period('1/2016')               # Also useful for index
```

*Index*
```Python
t1 = pd.Series(list('abc'), [pd.Timestamp('2016-09-01'), pd.Timestamp('2016-09-02'), pd.Timestamp('2016-09-03')])
t2 = pd.Series(list('def'), [pd.Period('2016-09'), pd.Period('2016-10'), pd.Period('2016-11')])
```

*To_datetime*
Change text in various forms to datatime
```Python
d1 = ['2 June 2013', 'Aug 29, 2014', '2015-06-26', '7/12/16']   ->  pd.to_datetime   -> [2013-06-02, 2013-06-02....]

```

*Timedeltas* 
Time delta is an interval between timestamp, or the result of a timestamp + timedelta.


*More examples of working with dates in a Dataframe inside the notebook*

