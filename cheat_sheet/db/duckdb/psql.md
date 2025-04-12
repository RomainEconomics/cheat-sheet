# DuckDB PSQL

## Connect to a Postgres DB using DuckDB

See [DuckDB PSQL Extension](https://duckdb.org/docs/extensions/postgres.html)

```sql
INSTALL postgres;
LOAD postgres;

ATTACH 'dbname= user= host=127.0.0.1' AS db (TYPE POSTGRES, READ_ONLY);

SHOW;            # same
SHOW ALL TABLES; # same

SHOW db.tbl;     # same
DESCRIBE db.tbl; # same
```
