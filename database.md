# Database

## MySql Notes

### Query statement

```sql
SELECT DISTINCT column, column, ...
    FROM table
    INNER JOIN another_table
        ON table.id = another_table.id
    WHERE condition
        AND|OR condition
        AND|OR condition
    ORDER BY column ASC|DESC
    LIMIT num_lim OFFSET num_off;
```
- `SELECT`
- `JOIN`: tableL.id = tableR.id (omit: idL = idR)
- `WHERE`
    - condition operator
        - `=`
        - `!=`, `<>`
        - `LIKE`, `NOT LIKE`
        - `%`, `_`
        - `IN (...)`, `NOT IN (...)`
        - `IS`/`IS NOT` `NULL`
- `ORDER BY`
- `LIMIT`, `OFFSET`: from num_off on count for num_lim

```sql
SELECT <expression> AS newcolumn
    FROM table
    WHERE <expression>
    ...;
```

## Convert

[mdb to sqlite](https://github.com/arturasn/mdb2sqlite)
