## Pandas

import pandas as pd

Pandas is a widely-used open-source data manipulation and analysis library for Python. 
It provides high-performance, easy-to-use data structures and functions for handling and processing structured data, such as spreadsheets, time series, and relational databases. 
Pandas has become an essential tool for data scientists, analysts, and quantitative traders due to its flexibility, efficiency, and compatibility with other Python libraries, such as NumPy and matplotlib.

In a trading environment, pandas is indispensable for managing and analyzing financial data, as it offers various capabilities for data cleaning, transformation, aggregation, and visualization. 
The following are some key features and applications of pandas in quantitative trading:

### DataFrame and Series

The primary data structures in pandas are the DataFrame and Series, which are designed to handle two-dimensional and one-dimensional data, respectively. These data structures are highly flexible and efficient, enabling traders to store, manipulate, and analyze large financial datasets with ease. For example, a trader can use a DataFrame to store historical stock prices, technical indicators, and fundamental data, while a Series can be employed to represent the closing prices or returns of a single stock.


#### DataFrames

A Pandas DataFrame is a 2 dimensional data structure, like a 2 dimensional array, or a table with rows and columns.

Create a simple dataframe:

```python

import pandas as pd
data = {
  'names' : ['Esra', 'Chava'],
  'ages'  : [28, 27]
}

#load data into a DataFrame object:
df = pd.DataFrame(data)
print(df)
```



