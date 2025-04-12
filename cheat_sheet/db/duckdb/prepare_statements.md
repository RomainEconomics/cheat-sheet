# DuckDB Prepare Statements

See [DuckDB Documentation](https://duckdb.org/docs/sql/query_syntax/prepared_statements)

## Deallocate Statement

```sql
DEALLOCATE my_query;
```

## Auto Increment

````sql
Can chain multiple `?`.

```sql
PREPARE my_query AS
  SELECT *
  FROM table
  WHERE column = ?;

EXECUTE my_query('value');
````

## Positional Parameters

```sql
PREPARE my_query AS
  SELECT *
  FROM table
  WHERE column1 = $2 AND column2 = $1;

EXECUTE my_query('value1', 'value2');
```

## Named Parameters

```sql
PREPARE my_query AS
  SELECT *
  FROM table
  WHERE column1 = $value1 AND column2 = $value2;

EXECUTE my_query(value1:='value1', value2:='value2');
```
