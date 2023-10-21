# Big Data

## Table of Contents

- [Working with Large Datasets](#working-with-large-datasets)

## Working with Large Datasets

Data Science is all fun and games until we encounter a **large datasets**. What am I talking about ? I'm talking about a bunch of CSV files with around 20 millions rows each. What a nightmare...

Data scientists are used to work with well-known libraries such as `pandas`. DataFrames are very convenient but using `df.read_csv()` will not necessarily work because it can overload main memory which is physically limited. When dealing with 2 or 3 dataframes, it can quickly become unmanagable.

In these conditions, there is a **unique solution** which can take different shapes: **dividing the problem into subproblems**. It could mean particionning, reducing, filtering or working with chunks of data. For a treatment on a very large file, it could mean reading the file line by line instead of loading everything in main memory.  
