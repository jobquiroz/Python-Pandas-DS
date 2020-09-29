## 04 Coursera Advanced Pandas Assignment

Week 3: Introduction to Data Science with Python course

### Relevant snipets

#### Merging Dataframes

*Union or outer*
It merges all data, each with the same index. 
```Python
pd.merge(df_1, df_2, how='outer', left_index = True, right_index=True)
```

