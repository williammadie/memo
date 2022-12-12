# JSON File Format

## Table of Contents

- [An Introduction to JSON](#an-introduction-to-json)
- [JSON Authorized Types](#json-authorized-types)
- [An Example of JSON file](#an-example-of-json-file)
- [Accessibility](#accessibility)
- [Serialization and Deserialization](#serialization-and-deserialization)

## An Introduction to JSON

**JSON** stands for **JavaScript Object Notation**. It refers to a lightweight text-based open standard for human-readable data interchange.

This type of files can be easily recognized because it uses the `.json` filename extension.

Nowadays, JSON is used everywhere:
- HTTP Requests
- Configuration Files
- Mock Data files for API tests

## JSON Authorized Types

JSON supports only a limited number of types which are:

| **Type** |                 **Description**                |                 **Example**                 |
|:--------:|:----------------------------------------------:|:-------------------------------------------:|
|  Number  | Double precision floating-point (**Decimal Only**) |   `0`, `1.0E+2`, `56.23`, `-234.13`, `12`   |
|  String  |              Series of characters              |       `M`,`"Hello World!"`, `"Jason"`       |
|  Boolean |                  true or false                 |              `true` or `false`              |
|   Array  |           Ordered sequence of values           |  `["kitchen", "cooking", "oven", "spoon"]`  |
|  Object  |     Unordered collection of key/value pairs    | `[{"name": "Henri"}, {"name": "Rodrigue"}]` |
|   Null   |                  Null or Empty                 |            `null` or `[]` or `{}`           |or `[]` or `{}`           |

## An Example of JSON file

```json
{
    "scope": {
        "source": "isco-08-ilo",
        "source_description": "International Standard Classification of Occupations",
        "tags": [
            "ISCO-08-ILO"
        ],
        "data_quality": "Official",
        "frequency": "daily",
        "frequency_start_hour": 1,
        "frequency_end_hour": 1,
        "reference_user": "International Labour Organization",
        "reporting_email": "isco@ilo.org",
        "globals": [
            {
                "variable": "source"
            }
        ],
        "update_scope": [
            {
                "variable": "source"
            }
        ]
    },
    "acquisition": {
        "channel": {
            "name": "url",
            "url": "https://www.ilo.org/ilostat-files/ISCO/newdocs-08-2021/ISCO-08/ISCO-08%20EN%20Structure%20and%20definitions.xlsx",
            "sheet": "ISCO-08 EN Struct and defin"
        },
        "format": {
            "name": "xls",
            "decimal_sign": ".",
            "thousands_separator": "",
            "date_format": "%Y-%m-%d",
            "encoding": "UTF-8"
        }
    },
    "columns": [
        {
            "name": "ISCO 08 Code",
            "variable": "isco_08_code",
            "action": "insert"
        },
        {
            "name": "Title EN",
            "variable": "isco_08_label",
            "action": "insert"
        }
    ]
}
```

## Accessibility

Currently, a vast majority of programming languages support **reading from JSON and writing to JSON**. Here is a quick list of these languages:

- JavaScript (of course)
- PHP
- Python
- C#
- C++
- Java

## Serialization and Deserialization

JSON is a format that *encodes objects in a string*.

**Serialization** is the process of converting an object into that string

```python
import json
data = {
    "user": {
        "name": "Billy Hartgrove",
        "age": 23
    }
}

json_str = json.dumps(data)
print(json_str)
>>> `"{user:{"name": "Billy Hartgrove", "age": 23}}"`
```

**Deserialization** is the reversed process of converting a string into an object

```python
import json
json_str = "{"name": "Romy", "gender": "female", "age": "43"}"

data = json.loads(json_str)
print(type(data))
>>> `dict`
print(data["name"])
>>> "Romy"
```