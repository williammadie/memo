# Spreadsheets

## Table of Contents
- [Google Sheets](#google-sheets)
    - [Basic commands](#basic-commands)
    - [Basic Functionalities](#basic-Functionalities)
    - [Useful formulas](#useful-formulas)

## Google Sheets

### Basic Commands

- `CTRL` + `SHIFT` + `↑` : select all upcells (same column)
- `CTRL` + `SHIFT` + `←` : select all leftcells (same line)
- `CTRL` + `SHIFT` + `→` : select all rightcells (same line)
- `CTRL` + `SHIFT` + `↓` : select all downcells (same column)

### Basic Functionalities

**Search and replace**
It is located in `Edit -> Select and replace` and is used to replace a specific value on a given range by another given value. For example, you can replace all *Hello!* with *Goodbye!* on an entire column.

You can also open this menu with the shortcut `CTRL` + `H`

Note:
In order to replace every empty cell of a column, you have to replace `^\s*$` *(= designates the null character in GSheets)* using `Match case` and `Search using regular expressions`


### Useful Formulas

Write text in a cell depending on the value present in another cell.
For instance, here, we write "response-text1" if "text1" is present. In all other cases, we write "response-text3"
```
=IFS(A1="text1";"response-text1";OR(A1="text2";A1="text3");"response-text3)
```