
> If you want to view or download the full set of development documents, see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).

#### Two-level Partitioning
TDSQL only uses the HASH method to shard data, which is not convenient for deleting old data of specific conditions, such as transactional data. In order to solve this problem, two-level partitioning can be used.
TDSQL supports two-level partitioning in range and list formats where the specific table creating syntax is similar to the partitioning syntax in MySQL.

> Note: Partitioning uses the less than `<` symbol; therefore, if you want to store the data of the current year (e.g., 2017), you need to create a `<2018` partition. You only need to create partitions up to the current time, and TDSQL will automatically add subsequent partitions (3 by default). Taking YEAR as an example, TDSQL will automatically create partitions of 2018, 2019, and 2020 and increase or decrease them afterwards.

Supported range types:

- DATE, DATETIME, and TIMESTAMP
		`year`, `month`, and `day` functions are supported. If the function is empty, it will be defaulted to the `day` function

- TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), and BIGINT
		`year`, `month`, and `day` functions are supported. The value entered is converted to year, month, and day and then compared against the sharded table information.

If the function is empty, this `int` value will be compared against the sharded table information directly.

Example:
If `hired` is of `date` type, the query for the corresponding value inserted is in the format of `'20160101 10:20:20' ,20160101`
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
If `hired` is of `int` type, the query for the corresponding value inserted will be in the format of `1474961034`. The proxy will first convert it into the corresponding date format (20160927) and then compare it against the sharded table information
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

Supported list types:
DATE, DATETIME, TIMESTAMP. `year`, `month`, and `day` functions are supported;
TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), and BIGINT;
CHAR, VARCHAR, BINARY, and VARBINARY;
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
