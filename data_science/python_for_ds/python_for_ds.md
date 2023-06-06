# Python for Data Science

## Table of Contents

## Optimized operations on DataFrames

There are different manners of manipulating data inside DataFrames. Keep in mind that some might be faster than others. The most common type of operation when workding with a DataFrame is building a new column based on the values of other columns. It is a very simple thing that can become horribly complicated or terribly slow if done with the wrong method. Let's see why:

Here are the most used method for `doing something at each row based on the values of the row`. I ordered them from the slowest to the fastest:

1. itterows
2. apply
3. vectorization

Let's see these methods with a common example of operation. We'll say that we need to build a new identifier which is the result of **concatenated values from other rows**.

### iterrows

`DataFrame.iterrows()` is a python generator which yields both the index and row as a Series.

Warnings:
- Iterating through pandas objects is generally slow. In many cases, iterating manually over the rows is not need and can be avoided by using an `apply function` or a `vectorized solution`.
- According to documentation, iterrows returns a `Series` for each row without preserving dtypes, this is why **you should never modify** something you are iterating over. 


```python
for index, row in df.iterrows():
    print(row['first_name'] + '_' + row['last_name'])
```

### apply function

```python
df['full_name'] = df.apply(lambda row: row['first_name'] + '_' + row['last_name'])
```

### vectorization

Vectorization is also called `array programming`. It is commonly refered to as the ability to work on a set of values in parallel (**Single Instruction Multiple Data (SIMD)** (=parrallel processing))

Why it is so much faster than `apply` or `iterrows`?

It is because it does not use loops. Python loops are slow because Python is a `dynamic programming language` and isn't `compiled` (so it does not benefit from optimizations at compiling time).

Generally speaking, most of `vectorized solutions` are highly optimized functions proposed by the pandas library. Such optimized functions are also present in the numpy library. 

```python
df['full_name'] = df['first_name'].str.cat(df['last_name'], sep='_')
```