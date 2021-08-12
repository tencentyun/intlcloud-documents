

TDSQL for MySQL currently supports two-level sharding in range and list formats, where the specific table creation syntax is similar to the sharding syntax in MySQL.

## Two-Level Sharding Syntax
The syntax for creating a sharded table with a hash at level 1 and a list at level 2 is as follows:
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
   
The syntax for creating a sharded table with a range at level 1 and a list at level 2 is as follows:
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

#### Supported range types
- DATE, DATETIME, and TIMESTAMP.
- `year`, `month`, and `day` functions are supported. If the function is empty, it will be defaulted to the `day` function.
- TINYINT, SMALLINT, MEDIUMINT, INT, and BIGINT.
- `year`, `month`, and `day` functions are supported. The value entered is converted to year, month, and day and then compared against the sharded table information.

#### Supported list types
- DATE, DATETIME, and TIMESTAMP.
- `year`, `month`, and `day` functions are supported.
- TINYINT, SMALLINT, MEDIUMINT, INT, and BIGINT.

<dx-alert infotype="alarm" title="Alarm">
<li>Refrain from using the TIMESTAMP type as the shardkey, because it is subject to the time zone and can only specify a time value before the year of 2038.</li>
<li>If the shardkey is `char` or `varchar` type, its length is better to be below 255.</li>
</dx-alert>

## Use Cases and Suggestions
Use one-level sharded tables for businesses as much as possible.
- Before use, design the table structure reasonably according to the business scenario in the long run. Two-Level sharding is suitable for scenarios where DDL changes are not required for a long time after the table structure is created, while the sharded data needs to be cleaned and trimmed regularly, such as log transaction tables.
- Design the granularity of two-level sharding reasonably. We recommend you refrain from using too fine-grained two-level sharding; otherwise, too many subtables will be created. For example, you should shard transaction tables by month instead of by day or by hour, so that there will not be too many data files in the file system.
- When performing an SQL query on a level-2 sharded table, include the key values of level-1 and level-2 sharding in the query conditions as much as possible, so as to eliminate the need to open many data files for search during query execution.
- When performing a JOIN query on a level-2 sharded table, if the query conditions don't include the key values of level-1 and level-2 sharding, the operation performance will be low, which is not recommended.
- The primary key or unique index of the table should include the shardkey; otherwise, the data uniqueness cannot be guaranteed.
