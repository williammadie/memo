# Python for Data Science

## Table of Contents

- [Optimized operations on DataFrames](#optimized-operations-on-dataframes)
    - [Common Solutions with Array Programming](#common-solutions-with-array-programming)
- [Handle null values in a DataFrame](#handle-null-values-in-a-dataframe)
- [Dtype Conversions on DataFrames](#dtype-conversions-on-dataframes)

## Optimized operations on DataFrames

There are different manners of manipulating data inside DataFrames. Keep in mind that some might be faster than others. The most common type of operation when workding with a DataFrame is building a new column based on the values of other columns. It is a very simple thing that can become horribly complicated or terribly slow if done with the wrong method. Let's see why:

Here are the most used method for `doing something at each row based on the values of the row`. I ordered them from the slowest to the fastest:

1. itterows
2. apply
3. np.vectorize
4. Vectorization

The following picture comes from StackOverflow. While numbers might be right or wrong, magnitudes between these different operations seem correct. 

![df-ways-of-iterating](/ds/python_for_ds/resources/python-dataframe-ways-of-iterating.png)

Let's see these methods with a common example of operation. We'll say that we need to build a new identifier which is the result of **concatenated values from other rows**.

### iterrows

`DataFrame.iterrows()` is a python generator which yields both the index and row as a Series.

Warnings:
- Iterating through pandas objects is generally slow. In many cases, iterating manually over the rows is not need and can be avoided by using an `apply function` or a `vectorized solution`.
- According to documentation, iterrows returns a `Series` for each row without preserving dtypes, this is why **you should never modify** something you are iterating over.
- Ideally, iterrows should never be used but in some edge cases you might be forced to use it (breath it'll be okay).


```python
for index, row in df.iterrows():
    print(row['first_name'] + '_' + row['last_name'])
```

### apply function

```python
df['full_name'] = df.apply(lambda row: row['first_name'] + '_' + row['last_name'])
```

### np.vectorize

As its name doesn't show it, this is not **true vectorization**. In fact, `np.vectorize` is a simple Python for loop with some enhancements/optimizations like caching. It is generally faster than a classic apply function (~10 times faster). However, this is incredibly slow compared to the power of **true vectorization** (see below).

```python
import numpy as np

def delta_smaller_than_31(delta: str) -> bool:
	return False if pd.isna(delta) else int(delta) < 31

vector_delta_smaller_than_31 = np.vectorize(delta_smaller_than_31)
screeninf_df["match_snds"] = vector_delta_smaller_than_31(screening_df["delta"])
```

### Vectorization

Vectorization is also called `array programming`. It is a **programmming paradigm** that is commonly refered to as the ability to work on a set of values in parallel (**Single Instruction Multiple Data (SIMD)** (=parrallel processing))

**Why it is so much faster than `apply` or `iterrows`?**

It is because it does not use loops. Python loops are slow because Python is a `dynamic programming language` and isn't `compiled` (so it does not benefit from optimizations at compiling time).

Generally speaking, most of `vectorized solutions` are highly optimized functions proposed by the pandas library. Such optimized functions are also present in the numpy library. 

```python
df['full_name'] = df['first_name'].str.cat(df['last_name'], sep='_')
```

### Common Solutions with Array Programming

Divide column A by column B
```python
df['new_column'] = np.where(df['B'] == 0, 0, df['A'] / df['B'])
```

Extract Year from datetime
```python
df['year'] = df['date'].dt.year
```

Calculate the minimum value between n columns
```py
date_columns = ["col1", "col2", "col3"]

# The following solution is not vectorized (for comparison only)
# tested on a DataFrame with 500k rows: ~7 seconds (70 times faster)
df["min_date"] = df[date_columns].apply(min, axis=1)

# The following solution is vectorized
# tested on a DataFrame with 500k rows: ~0.1 second
df["min_date"] = np.min(df[date_columns], axis=1)
```

## Handle null values in a DataFrame

Keep rows where at least n columns have non-NaN values
```py
df
movie   name    rating
thg     NaN     3
thg     John    4
lob     NaN     NaN
NaN     Gill    NaN

df.dropna(thresh=2)

df
movie   name    rating
thg     John    4
thg     NaN     3
```

Delete NaN values inside a column (Visualization only)
```py
df[["col1"]].dropna(thresh=1)
```

Delete NaN values inside several column (Visualization only)
```py
df[["col1", "col2"]].dropna(thresh=2)
```

## Dtype Conversions on DataFrames

Convert a column to Int64 (it accepts NaN)
```python
df["column"] = df["column"].astype("Int64")
```
```python

```
