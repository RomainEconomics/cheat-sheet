# DuckDB Unpivot and Pivot

```sql
CREATE TABLE Cities (
    Country VARCHAR, Name VARCHAR, Year INTEGER, Population INTEGER
);
INSERT INTO Cities VALUES
    ('NL', 'Amsterdam', 2000, 1005),
    ('NL', 'Amsterdam', 2010, 1065),
    ('NL', 'Amsterdam', 2020, 1158),
    ('US', 'Seattle', 2000, 564),
    ('US', 'Seattle', 2010, 608),
    ('US', 'Seattle', 2020, 738),
    ('US', 'New York City', 2000, 8015),
    ('US', 'New York City', 2010, 8175),
    ('US', 'New York City', 2020, 8772);

FROM Cities;
```

## Pivot

```sql
PIVOT Cities
ON Year
USING SUM(Population);
```

## Unpivot

```sql
UNPIVOT pivot_cities
ON 2000, 2010, 2020
INTO
     NAME year VALUE population;
```

Or

```sql
UNPIVOT pivot_cities
ON COLUMNS (* EXCLUDE (Country, Name))
INTO
     NAME year VALUE population;
```
