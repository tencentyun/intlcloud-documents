Tables in CDWPG are similar to those in other relational databases. The difference is that the rows of a CDWPG table are distributed on different segments as determined by the distribution policy of the table.

### Creating common table
The `CREATE TABLE` command is used to create a table. The following can be defined during table creation:
- Table column and [data type](https://intl.cloud.tencent.com/document/product/1138/45120)
- Table constraint definition
- [Table distribution definition](https://intl.cloud.tencent.com/document/product/1138/47248)
- [Table storage format](https://intl.cloud.tencent.com/document/product/1138/47249)
- [Table partition definition](https://intl.cloud.tencent.com/document/product/1138/45025)

Use the `CREATE TABLE` command to create a table in the following format:
```
CREATE TABLE table_name ( 
[ { column_name data_type [ DEFAULT default_expr ]   -- Table column definition
   [column_constraint [ ... ]                        -- Column constraint definition
] 
   | table_constraint                                -- Table constraint definition                            
   ])
   [ WITH ( storage_parameter=value [, ... ] )       -- Table storage format definition
   [ DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY ]  -- Table distribution key definition          
   [ partition clause]                               -- Table partition definition
```

**Example:**
The table creation statement in the following example creates a table with **trans_id** as the distribution key and sets `RANGE` partitioning based on **date**.
```
CREATE TABLE sales (
  trans_id int,
  date date, 
  amount decimal(9,2), 
  region text)
  DISTRIBUTED BY (trans_id)  
  PARTITION BY RANGE(date)    
  (start (date '2018-01-01') inclusive
   end (date '2019-01-01') exclusive every (interval '1 month'),
   default partition outlying_dates);
```

## Creating Temporary Table
A temporary table stores temporary intermediate results and is deleted automatically at the end of the session or selectively at the end of the current transaction. The command to create a temporary table is as follows:
```
CREATE TEMPORARY TABLE table_name(…)
    [ON COMMIT {PRESERVE ROWS | DELETE ROWS | DROP}]
```

**Description:** The temporary table behavior at the end of a transaction block can be controlled by `ON COMMIT` in the above statement.

- PRESERVE ROWS: The data will be retained at the end of the transaction. This is the default behavior.
- DELETE ROWS: All rows in the temporary table will be deleted at the end of each transaction block.
- DROP: The temporary table will be dropped at the end of the current transaction block.

**Example:**
Create a temporary table and drop it at the end of the transaction.
```
CREATE TEMPORARY TABLE temp_foo (a int, b text) ON COMMIT DROP;
```

## Table Constraint Definition
You can define constraints on columns and tables to restrict the data, but there are some limitations:
- Columns referenced by a check constraint can only be in the same table.
- Unique and primary key constraints must contain the distribution key column. They are not supported for append-optimized and column-oriented tables.
- Foreign key constraints are allowed to be invalid in CDWPG.

The actual commands to use constraints are as follows:
```
UNIQUE ( column_name [, ... ] )
   | PRIMARY KEY ( column_name [, ... ] ) 
   | CHECK ( expression )
```

### Check constraint
A check constraint specifies that the values in the column must satisfy a Boolean expression; for example:
```
CREATE TABLE products
            ( product_no integer,
              name text,
              price numeric CHECK (price > 0) );
```

### Not-null constraint
A not-null constraint specifies that columns cannot have null values; for example:
```
CREATE TABLE products
       ( product_no integer NOT NULL,
         name text NOT NULL,
         price numeric );
```



### Unique constraint
A unique constraint ensures that the data contained in a column or a group of columns is unique for all rows in a table. A table containing a unique constraint must be hash distributed, and the constraint column must contain the distribution key column; for example:
```
CREATE TABLE products
       ( product_no integer UNIQUE,
         name text,
         price numeric)
      DISTRIBUTED BY (product_no);
```
>! Primary key constraints are supported only for row-oriented heap tables but not append-only tables.

### Primary key constraint
A primary key constraint is a combination of a unique constraint and a not-null constraint. A table containing a primary key constraint must be hash distributed, and the constraint column must contain the distribution key column. If the table has a primary key, this column (or group of columns) will be selected as the distribution key for the table by default; for example:
```
CREATE TABLE products
       ( product_no integer PRIMARY KEY,
         name text,
         price numeric)
      DISTRIBUTED BY (product_no);
```
>! Primary key constraints are supported only for row-oriented heap tables but not append-only tables.



