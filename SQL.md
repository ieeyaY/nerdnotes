# SQL
## Query

```SQL
SELECT [column1, column2, ...]
[FROM <table>]
[WHERE <condition>]
[GROUP BY <column1, column2, ...>]
[HAVING <condition>]
[ORDER BY <column1 [ASC|DESC], column2 [ASC|DESC], ...>]
[LIMIT <number> [OFFSET <number>]];
```

``` SQL
#Select 子表
SELECT
    (SELECT <subquery_column> FROM <subquery_table> WHERE <condition>) AS <alias>
FROM <table> ...
#Where 子表
SELECT <columns> FROM <table>
WHERE <column> [operator]
    (SELECT <subquery_column> FROM <subquery_table> WHERE <condition>);
#首部
SELECT TOP number|percent 
SELECT TOP colname(n)
```
condition
```SQL
> < = <>(!=) >= <= BETWEEN..AND LIKE IN() AND OR
BETWEEN v1 AND v2
LIKE '%PATTERN%'
IN(v1, v2, ..)
IS NULL
```
LIKE通配符
- `%`
- `_`
- `[]`
- `[^]` `[!]`

### JOIN
![](https://www.runoob.com/wp-content/uploads/2019/01/sql-join.png)

```SQL
SELECT * FROM
A [JOIN | INNER JOIN | LEFT JOIN | RIGHT JOIN | FULL OUTER JOIN] B;
```

### Union
每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。
```SQL
SELECT column_name(s) FROM table1
UNION 
SELECT column_name(s) FROM table2;

SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2; 允许重复值
```

## Insert

```SQL
INSERT INTO <table_name> [(column1,column2,column3,...)]
VALUES (value1,value2,value3,...);
```
Select Into
```SQL
SELECT ... INTO <newtable>;

INSERT INTO <table_name> [(column1,column2,column3,...)]
SELECT <...>;

CREATE TABLE 新表
AS
SELECT * FROM 旧表 
```

## Delete

```SQL
DELETE FROM table_name
WHERE condition;
```

```SQL
DROP TABLE [IF EXISTS] <table>;
DROP INDEX [IF EXISTS] <indexname> ON <tablename>;
DROP DATABASE [IF EXISTS] <dbname>;

TRUNCATE TABLE <tablename>;
```

## Update

```SQL
UPDATE table_name
SET column1 = value1, column2 = value2, ...
[WHERE condition];
```

```SQL
ALTER TABLE table_name ADD column_name datatype;
ALTER TABLE table_name DROP COLUMN column_name datatype;
ALTER TABLE table_name ALTER|MODIFY COLUMN column_name datatype;
```

## Create
CREATE DATABASE - 创建新数据库
CREATE TABLE - 创建新表

Create Table
```SQL
CREATE TABLE (
    col datatype constraint,
    ...);
```
Create Index
```SQL
CREATE INDEX index_name
ON table_name (column_name);
CREATE UNIQUE INDEX index_name
ON table_name (column_name);
```
Create View
```SQL
CREATE VIEW view_name AS
SELECT ...
```

constraint
- `NOT NULL` - 指示某列不能存储 `NULL` 值。
- `UNIQUE` - 保证某列的每行必须有唯一的值。
- `PRIMARY KEY` - `NOT NULL` 和 `UNIQUE` 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
- `FOREIGN KEY` - 保证一个表中的数据匹配另一个表中的值的参照完整性。`FOREIGN KEY REFERENCES <table>(<col>)`
- `CHECK` - 保证列中的值符合指定的条件。
- `DEFAULT` - 规定没有给列赋值时的默认值。
