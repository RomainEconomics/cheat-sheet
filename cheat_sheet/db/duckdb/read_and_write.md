# DuckDB

## Read from

```sql
FROM read_json('file.json');
FROM read_json_auto('file.json');
CREATE TABLE df AS FROM read_json_auto('file.json');
CREATE OR REPLACE TABLE df AS FROM read_json_auto('file.json');
```

## Write to

```sql
COPY table_name TO 's3://bucket/file.extension';

-- parquet with partitioning
COPY table TO 's3://my-bucket/partitioned' (
    FORMAT PARQUET,
    PARTITION_BY (part_col_a, part_col_b)
);
```
