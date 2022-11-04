

TDSQL for MySQL allows you to subpartition tables by RANGE or LIST, with subpartitioning syntax similar to that in MySQL.

## Subpartitioning Syntax
Subpartitioning by HASH at level 1 and by LIST at level 2 is as follows:
```
MySQL [test]> CREATE TABLE customers_1 (
  first_name VARCHAR(25) key,
  last_name VARCHAR(25),
  street_1 VARCHAR(30),
  street_2 VARCHAR(30),
  city VARCHAR(15),
  renewal DATE
) shardkey=first_name

PARTITION BY LIST (city) (
  PARTITION pRegion_1 VALUES IN('Beijing', 'Tianjin', 'Shanghai'),
  PARTITION pRegion_2 VALUES IN('Chongqing', 'Wulumuqi', 'Dalian'),
  PARTITION pRegion_3 VALUES IN('Suzhou', 'Hangzhou', 'Xiamen'),
  PARTITION pRegion_4 VALUES IN('Shenzhen', 'Guangzhou', 'Chengdu')
);
```
   
Subpartitioning by RANGE at level 1 and by LIST at level 2 is as follows:
```
MySQL [test]> CREATE TABLE tb_sub_r_l (
   id int(11) NOT NULL,
   order_id bigint NOT NULL,
   PRIMARY KEY (id,order_id)) 
   PARTITION BY list(order_id)
   (PARTITION p0 VALUES in (2121122),
   PARTITION p1 VALUES in (38937383))
   TDSQL_DISTRIBUTED BY RANGE(id) (s1 values less than (100),s2 values less than (1000));
Query OK, 0 rows affected, 1 warning (0.35 sec)
```

#### Supported RANGE types
- DATE, DATETIME, and TIMESTAMP.
- `year`, `month`, and `day` functions are supported. If the function is empty, it will be defaulted to the `day` function.
- TINYINT, SMALLINT, MEDIUMINT, INT, and BIGINT.
- `year`, `month`, and `day` functions are supported. The value entered is converted to year, month, and day and then compared against the sharded table information.

#### Supported LIST types
- DATE, DATETIME, and TIMESTAMP.
- `year`, `month`, and `day` functions are supported.
- TINYINT, SMALLINT, MEDIUMINT, INT, and BIGINT.

<dx-alert infotype="alarm" title="Alarm">
<li>Do not use the TIMESTAMP type as the subpartitioning key, because it is subject to the time zone and can only specify a time value before the year of 2038.</li>
<li>If the subpartitioning key is `char` or `varchar` type, its length is better to be below 255.</li>
</dx-alert>

## Use Cases and Suggestions
Use level-1 subpartitioned tables for your business.
- Before use, design your table structure reasonably according to the business scenario in the long run. Subpartitioning is suitable for scenarios where DDL changes are not required for a long time after the table structure is created, while the subpartitioned data needs to be cleared and trimmed regularly, such as log transaction tables.
- Design the granularity of subpartitioning reasonably. We recommend that you do not design it in a finer-grained manne to avoid creating too many subtables. For example, you should subpartition transaction tables by month instead of by day or by hour, so that there will not be too many data files in the file system.
- When performing a SQL query on a level-2 subpartitioned table, you need to include the key values of level-1 and level-2 subpartitioning in the query conditions as much as possible, so you can eliminate the need to open many data files for search during query execution.
- When performing a JOIN query on a level-2 subpartitioned table, if you don't include the key values of level-1 and level-2 subpartitioning in the query conditions, the operation performance will be lowered, which is not recommended.
- The primary key or unique index of the table should include the subpartitioning key; otherwise, the data uniqueness cannot be guaranteed.
