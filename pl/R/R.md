# The R langage

## Table of Contents

- [What is R ?](#what-is-r-?)
- [Add New Libraries](#add-new-libraries)
    - [CRAN](#cran)
    - [Install and Load Libraries](#install-and-load-libraries)
    - [Overview of the Main Libraries](#overview-of-the-main-libraries)
- [Basic Commands](#basic-commands)
- [Operators](#operators)
    - [Arithmetic Operators](#arithmetic-operators)
    - [Logical Operators](#logical-operators)
- [R Data Types & Structures](#r-data-types)
    - [R Data Types High-level](#r-data-types-high-level)
    - [R Data Types Low-level](#r-data-types-low-level)
    - [R Data Structures](#r-data-structures)
- [Fundamentals](#fundamentals)
    - [Write a Function](#write-a-function)
- [DataFrames](#dataframes)
    - [Basic Operations](#basic-operations)
- [R for Statistics](#r-for-statistics)
    - [Histogram](#histogram)
    - [Boxplot](#boxplot)

## What is R ?

R is a programming langage for statistical computing and graphics. It is especially good at performing mathematical operations on matrix or vectors and statistical analysis. 

This langage is quite similar to **Python** due to being open-source too. It is maintained by a large community which continuously add new libraries and tools on the *CRAN* (Comprehensive R Archive Network) which is a sort of **package manager**.

![r-langage](/programming_languages/R/resources/r-langage.webp)

## Add New Libraries

### CRAN

The *CRAN* (Comprehensive R Archive Network) is a sort of **package manager**. It is quite similar to **PIP for Python**. People can upload/retrieve/download R libraries from this source.

Here is an oversimplified mapping of the CRAN:

![cran-map](/programming_languages/R/resources/cran-overview.jpg)

### Install and Load Libraries

Install a package from CRAN
```R
install.packages('pckg_name')
```

Install a package from GitHub (requires devtools CRAN package)
```R
install.packages('devtools')    # Prerequisite
devtools::install_github('username/repository_name')
```

Load a package (independently from the source GitHub or CRAN)
```
library(library_name)
```

### Overview of the Main Libraries

- **Dplyr**: Functions for **manipulating data frames** (select, filter, arrange, mutate, summarize, sample, group by, pipe...).
- **Ggplot2**: One of the most used libraries for **data visualization**.
- **Shiny**: The "Data Scientist's best fiend", a library for easily building interactive web apps.

## Basic Commands

launch a R interpreter
```bash
sudo R
```

Leave a R interpreter
```R
q()
```

Get general help
```R
help()
```

Load a built-in dataset into the environment (from a package)
```R
data('dataset_name')    # Prequeresite: given pckg needs to be loaded
```

## Operators

### Arithmetic Operators

| **Operator** |  **Description** |
|:------------:|:----------------:|
|       +      |     addition     |
|       -      |   substraction   |
|       *      |  multiplication  |
|       /      |     division     |
|    ^ or **   |    exponential   |
|    x %% y    |      modulus     |
|    x %/% y   | integer division |

### Logical Operators

| **Operator** |    **Description**    |
|:------------:|:---------------------:|
|       <      |       less than       |
|      <=      | less than or equal to |
|       >      |       more than       |
|      >=      | more then or equal to |
|      ==      |   exactly equal to    |
|      !=      |      not equal to     |
|      !x      |         not x         |
|    x \| y    |         x or y        |
|     x & y    |        x and y        |
|   isTRUE(x)  |   test if x is TRUE   |

### Assignement Operator

Oh yeah! A dedicated part to the assignement operator! You don't see why? Oh let me explain:

```R
c = 1 + 2
c
>> 3
# seems to be identical to:
d <- 1 + 2
d
>> 3
```

Do you see the problem now? There are **two assignement operators**... Oh yes, life is complicated...

There a different reasons why there are two operators.

1. It is used to avoid mixing variables which are declared **in the scope of a function** and variables which are declared **in the scope of the user workspace**.

In this example, we can't call x in the first case because it is not declared in the user workspace (only in the scope of the function)
```R
median(x = 1:10)
x   
## Error: object 'x' not found
```

In the second case, we can call x in the user workspace.

```R
median(x <- 1:10)
x    
## [1]  1  2  3  4  5  6  7  8  9 10
```

2. It is a sort of convention to use `<-` instead of `=` in R because it assures compatibility with old versions of an analytical & statistical tool called **S-Plus** based on the **S langage**.

In short, if you want to be safe, keep with `<-`. If you're more advanced and rebellious (and know what you're doing) you can use `=`

## R Data Types & Structures

### R Data Types (High-level)

- character `<chr>` => refers to **a single character** as well as **a sequence of characters**
- numeric => refers to **a real number** as well as **a decimal number**
- integer `<int>` => refers to an integer
- logical => refers to a **boolean**
- complex => refers to a **complex number**

Check an object type (high-level)
```R
class(obj)
```

### R Data Types (Low-level)

- double `<dbl>` => refers to **a decimal number** (= numeric high-level type)

Check an object type (low-level)
```R
typeof(R)
```

### R Data Structures

#### Vectors

A **Vector** is a collection of elements of **the same type** (`character`, `logical`, `integer`, `numeric`).

If given elements are not of the same type, they will be cast implicitly.

Instantiate a Vector
```R
c(1, 113, 45, 7)
>> 1 113 45 7
```

Sort a Vector (ascending order)
```R
a = c(1, 113, 45, 7)
sort(a)
>> 1 7 45 113 
```

Sort a Vector (descending order)
```R
a = c(1, 113, 45, 7)
sort(a, decreasing=TRUE)
>> 113 45 7 1 
```
#### Lists

A **List** is a collection of elements of **different types**

- matrix
- data frame
- factors `<fct>` => 

## Fundamentals

### Write a Function

```R
#' Title
#'
#' Description
my_function <- function(p1, p2, pn) {
    # function body
    return(res)
}
```

## DataFrames

### Basic Operations

Access a specific column (see all)
```R
df$my_col
```

Access a specific column (See head only)
```R
df['my_col']
```

Create a column filled with a specific value
```R
df$my_col <- NA
df$my_col <- 0
df$my_col <- "PDA-1"

# OR

df['my_col'] <- NA
df['my_col'] <- 0
df['my_col'] <- "PDA-1"

# Here, the two ways provide the same results
```

Create a column by applying a transformation on the values from another column
(In this example, we create a new column *year_week* based on the values of *time*. (time: yyyy-mm-dd) and (year_week: yyyy-wn) where *wn = week number*)
```R
fun1 <- function(time) strftime(time, format = "%Y-%V")
df$year_week <- mapply(fun1, df$time)
```

Keep only specific columns
```R
keeps <- c("country_code", "year_week", "time", "new_cases")
df <- df[keeps]
```

## R for Statistics

### Histogram

### Scatterplot

`plot()`

### Boxplot

`boxplot` (FR: boîte à moustaches)

### Sample

The sample function is used to generate a sample of random values in a range of values.

The following function:
- generates `number_of_values` inside `value_range`
- `replace = T` means that the draw is done with discount ([FR] tirage avec remise)
```R
sample(value_range, number_of_values, replace = T)

# The following function generates 100 numbers
# between 1 and 6
d2 = sample(1:6, 100, replace = T)
```
Output
```bash
  [1] 4 5 3 2 3 2 6 1 4 1 4 5 5 1 5 3 5 3 3 5 5 6 6 6 5 5 1 1 5 1 1 3 2 4 4 1 2
 [38] 3 1 5 6 5 5 1 1 6 2 3 3 4 5 5 4 1 4 3 2 3 3 4 3 3 3 3 5 5 4 1 3 1 4 5 2 3
 [75] 4 5 4 2 2 5 3 5 2 4 5 5 1 5 6 2 2 2 5 1 5 4 1 2 5 2
```

### Table

The table function is used to obtain the number of ocurences of each element inside a vector.

```R
d2 = sample(1:6, 100, replace = T)
d1 = sample(1:6, 100, replace = T)

# This line sums d1 and d2 vectors
s = d1 + d2;

# This function creates a vector of occurences for each 
# element present inside the s vector 
tab.s = table(s)

# Then, we can find the occurence of the ith value with:
tab.s[i]
```

### Rbind

The `rbind` function concatenates two dataframes

### Sum

This function counts how many times a given value appears inside a vector. 

The following code simulates two dices
```R
d2 = sample(1:6, 100, replace = T)
d1 = sample(1:6, 100, replace = T)

# keep in mind that the values of s are between 2 and 12.
s = d1 + d2;

# This shows the how many times the sum of the two
# dices equals 2.
sum(s == 2);
```

### pmax

This function returns the maximum values across vectors 

Example
```R
# Create two vectors
x <- c(2, 4, 6, 7, 9)
y <- c(1, 3, 5, 8, 10)

# Use pmax to calculate the element-wise maximum
result <- pmax(x, y)

print(result)
```

Output
```R
[1]  2  4  6  8 10
```

### Runif

Generate uniform random numbers between 0 and 1
```R
r <- runif(10, -1, 1)
r
# [1] -0.46469398 -0.45269714  0.18161681  0.03550296  0.08549162  0.35735277
# [7]  0.47083597 -0.84420644  0.77130939  0.87615484
```

```R
x = runif(100)
y = runif(100)
plot(x, y)

cov(x,y)    # Covariance
cor(x,y)    # Correlation Coefficient (between -1 and 1)
# The correlation describes the linearity and the direction of the timeseries
```

### The Poisson Distribution

```R
# exponential
exp(-3);

# poisson distribution with x = 0 and lambda = 3
dpois(0, 3);

# here P(X = 0) = exp(-3)*3^2/2!
```

Write a custom function that calculate the probability that
2 persons have their birthday on the same day
```R
anniv = function(N) {
    p = 1
    for (n in 2:N) p = p*(366-n)/365
    p = 1-p; p
}

anniv(2); 1-364/365;
```

