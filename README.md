# Python for Data Science (using the Numpy and Pandas libraries)

This repository contains information from several sources (mainly online courses) related to Python, Numpy and Pandas.
I decided to put some comments in Spanish because I think that by describing (relevant) python operations with my own words makes me realize whether or not I fully understand the concepts. 

It is divided into two folders: Python & Numpy and Pandas. 

## Python & Numpy

### Coursera - 01 Coursera Python basics and Numpy

Python notebook corresponding to week 1 from Introduction to Data Science by University of Michigan.

In this week we review some basic Python commands and a general tour for Numpy.

**Content**
 - Python functions
 - Operations on numbers, lists and strings.
 - Dictionaries and ways to iterate them
 - The `.format()`method
 - Reading and writing CSV files
 
**Relevant snipets**
*Iterating over dictionary keys and labels simultaneously* 

```Python
for name, email in x.items():
  print(name)
  print(email)
 ```
 
*Using dictionaries and `format()` for string formating*

```Python
# Data in dictionary
sales_record = {'price': 3.24, 'num_items': 4, 'person': 'Chris'} 
# String structure 
sales_statement = '{} bought {} item(s) at a price of {} each for a total of {}'
# Final formating and adding data
print(sales_statement.format(sales_record['person'], sales_record['num_items'], sales_record['price'], 
                            sales_record['num_items']*sales_record['price'])) # Operating while formating
```


                            

                            
                            
