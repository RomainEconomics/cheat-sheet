see: https://support.us.ovhcloud.com/hc/en-us/articles/4603838122643-Getting-Started-with-Object-Storage

## Load from DuckDB

Note that when using special endpoint, you also need to set the region inside the endpoint

```sql
load httpfs;
CREATE SECRET secret1 (
    TYPE S3,
    KEY_ID '',
    SECRET '',
    REGION 'gra',
    ENDPOINT 's3.gra.io.cloud.ovh.net'
);
FROM read_csv('s3://airflow-logs-staging/penguins.csv');
```

```sql
DROP SECRET secret1;
```
