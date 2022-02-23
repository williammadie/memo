# Spreadsheets

## Table of Contents
- [Google Sheets](#google-sheets)
    - [Basic commands](#basic-commands)
    - [Useful formulas](#useful-formulas)

## Google Sheets

### Basic Commands

- `CTRL` + `SHIFT` + `↑` : select all upcells (same column)
- `CTRL` + `SHIFT` + `←` : select all leftcells (same line)
- `CTRL` + `SHIFT` + `→` : select all rightcells (same line)
- `CTRL` + `SHIFT` + `↓` : select all downcells (same column)

### Useful Formulas

Write text in a cell depending on the value present in another cell.
For instance, here, we write "response-text1" if "text1" is present. In all other cases, we write "response-text3"
```
=IFS(A1="text1";"response-text1";OR(A1="text2";A1="text3");"response-text3)
```