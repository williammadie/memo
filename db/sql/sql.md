## Comments

```sql
-- one line comment

/* multi-line comment */
```

## SELECT

In `SQL`, request structure is ordered. **Keywords order can't be changed**

Order of keywords:
```sql
SELECT      -- item(s), aggregates or axis of aggregation
FROM        -- table on which we search items
WHERE       -- filter on each row of the table
JOIN        -- add information from another table
GROUP BY    -- axis of aggregation
HAVING      -- filter on aggregates
```

> SELECT Structure (Simple)
```sql
SELECT what_to_select
FROM which_table
WHERE condition_to_satisfy;
```

> Order a result (ascending order (default) 0 -> 10)
```sql
SELECT what_to_select
FROM which_table
WHERE condition_to_satisfy
ORDER BY reference_column;
```

> Order a result (descending order 10 -> 0)
```sql
SELECT what_to_select
FROM which_table
WHERE condition_to_satisfy
ORDER BY reference_column DESC;
```

> Aggregate a result
```sql
SELECT SUM(salary), department_code
FROM employee
GROUP BY department_code;
```

In the example above, we print the agregated information `SUM(salary)` and we also print the column name `department_code`. Because, we added a column without an agregated function inside the select, we have to add it to the GROUP BY.

> Filter on an aggregated funcion
```sql
SELECT SUM(salary), department_code
FROM employee
GROUP BY department_code
HAVING SUM(salary) > 50000.00;
```

Keep in mind that having is used because this kind of request is not possible:
```sql
SELECT SUM(salary), department_code
FROM employee
WHERE SUM(salary) > 50000.00
GROUP BY department_code;
```

> Join another table
```sql
SELECT employee.firstname, employee.lastname, department.code
FROM employee
LEFT OUTER JOIN department
    ON employee.department_code = department.code
ORDER BY department_code;
```

Is it possible to make a joint on the same table than the one in FROM ?

-> Yes, it is possible

> Use an alias
```sql
SELECT employee.firstname + ' ' + employee.lastname AS 'Full Name'
```

## Joint Types

- `INNER JOIN`
- `NATURAL JOIN`
- `LEFT JOIN`
- `RIGHT JOIN`
- `ANTI`

![sql-joins](/db/sql/resources/SQL_Joins.png)

## Tables

Create, Modify, Delete a table
```sql
CREATE
ALTER
DROP
```

## Data

Insert new rows in a table (no col names)
```sql
INSERT INTO tablename VALUES 
('val1', 'val2', 'valn'),
('val1', 'val2', 'valn'),
('val1', 'val2', 'valn');
```

Insert new rows in a table (with col names)
```sql
INSERT INTO tablename (col1, col2, col3) VALUES 
('val1', 'val2', 'valn'),
('val1', 'val2', 'valn'),
('val1', 'val2', 'valn');
```

Update an already existing row
```sql
UPDATE tablename
SET coln = 'valn'
WHERE col2 = 'valm';
```