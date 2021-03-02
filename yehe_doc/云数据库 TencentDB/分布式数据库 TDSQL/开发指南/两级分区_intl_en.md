TDSQL for MySQL only uses the HASH method to shard data, which is not convenient for deleting legacy data of specific conditions, such as transactional data. In order to solve this problem, subpartitioning can be used.

TDSQL for MySQL supports RANGE and LIST subpartitioning, where the table creating syntax is similar to the partitioning syntax in MySQL.

## Data Types Supported by RANGE
- DATE, DATETIME, TIMESTAMP: the `year`, `month`, and `day` functions are supported. If the function is left empty, the `day` function is used.
- TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), BIGINT: the `year`, `month`, and `day` functions are supported. A passed-in value will be converted into the format of year, month, or day, and compared against values in partitioned tables. If the function is left empty, INT values are used to compare against values in partitioned tables.

Example:
If `hired` is of DATE type, the values queried or inserted should be in the format of `20160101 10:20:20` or `20160101`.
```
	CREATE TABLE employees_int (
	    id INT key NOT NULL,
	    fname VARCHAR(30),
	    lname VARCHAR(30),
	    hired date,
	    separated DATE NOT NULL DEFAULT '9999-12-31',
	    job_code INT,
	    store_id INT
	)
	shardkey=id 
	PARTITION BY RANGE ( month(hired) ) (
	    PARTITION p0 VALUES LESS THAN (199102),
	    PARTITION p1 VALUES LESS THAN (199603),
	    PARTITION p2 VALUES LESS THAN (200101)
	);
```

If `hired` is of INT type, the values queried or inserted should be in the format of `1474961034`. The proxy first converts such a value into the DATE format (such as `20160927`) and then compares it against values in partitioned tables.
```
	CREATE TABLE employees_int (
	    id INT key NOT NULL,
	    fname VARCHAR(30),
	    lname VARCHAR(30),
	    hired int,
	    separated DATE NOT NULL DEFAULT '9999-12-31',
	    job_code INT,
	    store_id INT
	)
	shardkey=id 
	PARTITION BY RANGE ( month(hired) ) (
	    PARTITION p0 VALUES LESS THAN (199102),
	    PARTITION p1 VALUES LESS THAN (199603),
	    PARTITION p2 VALUES LESS THAN (200101)
	);
```


## Data Types Supported by LIST
- DATE, DATETIME, TIMESTAMP: the `year`, `month`, and `day` functions are supported.
- TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), BIGINT, CHAR, VARCHAR, BINARY, VARBINARY.

```
	CREATE TABLE customers_1 (
	    first_name VARCHAR(25),
	    last_name VARCHAR(25),
	    street_1 VARCHAR(30),
	    street_2 VARCHAR(30),
	    city VARCHAR(15),
	    renewal DATE
	) shardkey=first_name
	PARTITION BY LIST (city) (
	    PARTITION pRegion_1 VALUES IN('1', '2', '3'),
	    PARTITION pRegion_2 VALUES IN('4', '5', '6'),
	    PARTITION pRegion_3 VALUES IN('7', '8', '9'),
	    PARTITION pRegion_4 VALUES IN('10', '11', '12')
	);
```

>!Partitioning uses the less than `<` symbol. If you want to store the data of the current year (e.g., 2017), you need to create a `<2018` partition. You only need to create partitions up to the current time, and TDSQL will immediately and automatically add subsequent partitions (3 by default). In subpartitioning, only YEAR/MONTH/DAY partitions are supported for auto-creation. Taking YEAR as an example, TDSQL will automatically create partitions of 2018, 2019, and 2020, and add more afterwards.
