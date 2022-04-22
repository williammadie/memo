# The R langage

## Table of Contents

- [What is R ?](#what-is-r-?)
- [Add New Libraries](#add-new-libraries)
    - [CRAN](#cran)
    - [Install and Load Libraries](#install-and-load-libraries)
    - [Overview of the Main Libraries](#overview-of-the-main-libraries)
- [Basic Commands](#basic-commands)
- [R Data Types & Structures](#r-data-types)
    - [R Data Types High-level](#r-data-types-high-level)
    - [R Data Types Low-level](#r-data-types-low-level)
    - [R Data Structures](#r-data-structures)

## What is R ?

R is a programming langage for statistical computing and graphics. It is especially good at performing mathematical operations on matrix or vectors and statistical analysis. 

This langage is quite similar to **Python** due to being open-source too. It is maintained by a large community which continuously add new libraries and tools on the *CRAN* (Comprehensive R Archive Network) which is a sort of **package manager**.

![r-langage](/R/resources/r-langage.webp)

## Add New Libraries

### CRAN

The *CRAN* (Comprehensive R Archive Network) is a sort of **package manager**. It is quite similar to **PIP for Python**. People can upload/retrieve/download R libraries from this source.

Here is an oversimplified mapping of the CRAN:

![cran-map](/R/resources/cran-overview.jpg)

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

Instanciate a Vector
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