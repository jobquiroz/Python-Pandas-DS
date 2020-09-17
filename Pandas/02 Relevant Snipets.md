## 02 Coursera Basic pandas: Assignment

Week 2: Introduction to Data Science with Python course

### Relevant snipets

#### Renaming columns

*Different ways to declare Series: Dictionary*
It implements a clever way to rename columns withing a loop.. 
```Python
df.rename( ... )
```

#### `idxmax`

*Implementing something like an argmax function*
```Python
def answer_one():
    return df['Gold'].idxmax(axis = 0) 
answer_one()
```

#### A complex query:
```Python
def answer_three():
    df_more = df[(df['Gold']>=1) & (df['Gold.1']) >=1]
    return (((df_more['Gold'])-(df_more['Gold.1']))/df_more['Gold.2']).abs().argmax()
answer_three()
```

#### Analyses a giant and complex query by parts:
```Python
census_df[census_df['SUMLEV']==50].groupby('STNAME')['CENSUS2010POP'].apply(lambda x: x.nlargest(3).sum()).nlargest(3).index.tolist()

# Analyzing:
# Seleccionar solo counties reales
counties = census_df[census_df['SUMLEV']==50]
# Se agrupan por estado, a la columna de pop se aplica una función que encuentra los índices de los counties más poblados... y se suman
counties.groupby('STNAME')['CENSUS2010POP'].apply(lambda x: x.nlargest(3).sum())
# de toda esta lsita se encuentran los tres más poblados
counties.groupby('STNAME')['CENSUS2010POP'].apply(lambda x: x.nlargest(3).sum()).nlargest(3)
# Se sacan los indices (nombres de estados)
counties.groupby('STNAME')['CENSUS2010POP'].apply(lambda x: x.nlargest(3).sum()).nlargest(3).index
# Se pasan valores a lista
counties.groupby('STNAME')['CENSUS2010POP'].apply(lambda x: x.nlargest(3).sum()).nlargest(3).index.tolist()
```

#### Using `startswith`:

```Python
counties_Wash = counties_and_regions[ counties_and_regions['CTYNAME'].str.startswith('Washington') ]
```
