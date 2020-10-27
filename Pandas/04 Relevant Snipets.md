## 04 Coursera Advanced Pandas Assignment

Week 3: Introduction to Data Science with Python course

### Relevant snipets

#### Renaming columns by using dictionary

```Python
energy = energy.rename(index = {'Bolivia...': 'Bolivia', "China2": "China"})
```

#### Dropping columns with consecutive number names

```Python
GDP.drop([str(x) for x in range(1960,2006)], axis = 1, inplace = True)
```

#### Merging Dataframes

*outer*
It merges all data, each with the same index. 
```Python
energy_GPD = pd.merge(energy, GDP, how = 'outer', left_index = True, right_index = True)
```

#### Using `apply` to format number
Adding commas between numbers

```Python
PopEst.apply(lambda x: '{:,}'.format(x))  ->>  1,346,232,231.102023
```

