## 01 Coursera Python basics and Numpy

### Relevant Python snipets

#### Iterating over dictionary keys and labels simultaneously

```Python
for name, email in x.items():
  print(name)
  print(email)
 ```
 
#### Using dictionaries and `format()` for string formating

```Python
# Data in dictionary
sales_record = {'price': 3.24, 'num_items': 4, 'person': 'Chris'} 
# String structure 
sales_statement = '{} bought {} item(s) at a price of {} each for a total of {}'
# Final formating and adding data
print(sales_statement.format(sales_record['person'], sales_record['num_items'], sales_record['price'], 
                            sales_record['num_items']*sales_record['price'])) # Operating while formating
```

#### Easy method to read CSV files into list of dictionaries: DictReader

```Python
import csv

with open('mpg.csv') as csvfile:
  mpg = list(csv.DictReader(csvfile))
```

#### A random list comprehension:
```Python
# List of pair numbers
L = [number for number in range (0,1000) if number % 2 == 0]
```


### Relevant Numpy snipets

#### Combining arrays_ 
```Python
import numpy as np
# Example array:
p = np.ones([2, 3], int)  # Arrays of only ones, 2 rows by 3 columns
# Vertical stacking:
np.vstack([p, 2*p]) 
# Horizontal stacking:
np.hstack([p, 2*p])
```

#### Dot Product
$ \begin{bmatrix}x_1 \ x_2 \ x_3\end{bmatrix}
\cdot
\begin{bmatrix}y_1 \\ y_2 \\ y_3\end{bmatrix}
= x_1 y_1 + x_2 y_2 + x_3 y_3$

```Python
x.dot(y)
```

#### Slicing
*Start at 5th element from the end, then counting backwards by 2 until the beginning of the array*
```Python
s[-5::-2]
```
*Selecting range of rows and columns*
```Python
r[1:5, ::2]
```

#### Conditional indexing
*Selecting only values > 30*
```Python
r[r>30]
```

***Changing** only values where > 30*
```Python
r[r>30] = 30
```

#### Iterating over arrays
*Iterate over row and index*
```Python
for i, row in enumerate(test):
  print('row', i, 'is', row)
```

#### `zip` function
*Use `zip` to iterate over multiple iterables*
```Python
for i, j in zip(test, test2):
  print(i, '+', j, '=', i + j)
```








