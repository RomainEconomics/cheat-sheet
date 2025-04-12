# Constraint in Postgres

| Constraint Type | Syntax                                                          | Description                                                                                                                    |
| --------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| NOT NULL        | `column_name data_type NOT NULL`                                | Ensures a column cannot have NULL value                                                                                        |
| UNIQUE          | `UNIQUE (column_name)` or `UNIQUE (column1, column2)`           | Ensures all values in a column or group of columns are unique                                                                  |
| PRIMARY KEY     | `PRIMARY KEY (column_name)` or `PRIMARY KEY (column1, column2)` | Combines NOT NULL and UNIQUE. Identifies each row uniquely                                                                     |
| FOREIGN KEY     | `FOREIGN KEY (column_name) REFERENCES other_table(column_name)` | Ensures values in a column match values in another table's column                                                              |
| CHECK           | `CHECK (condition)`                                             | Ensures all values in a column satisfy certain conditions                                                                      |
| DEFAULT         | `column_name data_type DEFAULT value`                           | Sets a default value for a column when no value is specified                                                                   |
| EXCLUDE         | `EXCLUDE USING index_method (element WITH operator)`            | Ensures that if any two rows are compared on specified columns using specified operators, not all comparisons will return TRUE |

Examples of usage:

```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) CHECK (price > 0),
    category_id INTEGER REFERENCES categories(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    sku VARCHAR(50) UNIQUE,
    CONSTRAINT price_discount_check CHECK (discount_price < price)
);
```

Additional notes:

- Multiple constraints can be combined for a single column
- Constraints can be named using `CONSTRAINT constraint_name`
- Constraints can be added at column level or table level
- Some constraints can span multiple columns (composite constraints)
