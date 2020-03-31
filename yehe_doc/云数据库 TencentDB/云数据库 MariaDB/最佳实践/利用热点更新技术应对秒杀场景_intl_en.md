## 1. Introduction
### 1.1. Background
In scenarios such as flash sales and limited-time offers, a large number of users send access requests for a large number of items in a very short period of time. In a MySQL database, an item is stored in one data row; therefore, many threads will compete for the InnoDB row lock, and the higher the concurrence, the more the waiting threads. In this case, TPS will decrease, RT will increase, and the throughput of the database will be severely affected. This document describes the special optimization made by TencentDB for MariaDB for such scenarios: hotspot update technology.

### 1.2. How to use
Hotspot update: the statement as shown below is used to frequently update a data object.
Currently, this feature is only supported in TencentDB for MariaDB 5.7.17, which can be purchased on the [TencentDB for MariaDB instance purchase page](https://buy.cloud.tencent.com/tdsql).
```
UPDATE COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL QUEUE_ON_PK 88 TARGET_AFFECT_ROW 1 table_name  SET k=k+1 WHERE id=88
```

## 2. Change of UPDATE and INSERT Syntax
The `UPDATE` and `INSERT` SQL statements can be used to add new keywords to indicate hotspot update. The words in red are newly added.

### 2.1. UPDATE syntax
```
UPDATE [LOW_PRIORITY]

       [COMMIT_ON_SUCCESS] [ROLLBACK_ON_FAIL] [QUEUE_ON_PK expr1] [TARGET_AFFECT_ROW expr2]

       [IGNORE] table_reference

SET col_name1={expr1|DEFAULT} [, col_name2={expr2|DEFAULT}] ...

[WHERE where_condition]

[ORDER BY ...]

[LIMIT row_count]
```

### 2.2. INSERT syntax
```
INSERT [LOW_PRIORITY | DELAYED | HIGH_PRIORITY]

       [COMMIT_ON_SUCCESS] [ROLLBACK_ON_FAIL] [QUEUE_ON_PK expr]

       [IGNORE]

[INTO] tbl_name

[PARTITION (partition_name,...)]

[(col_name,...)]

{VALUES | VALUE} ({expr | DEFAULT},...),(...),...

[ ON DUPLICATE KEY UPDATE

col_name=expr

[, col_name=expr] ... ]
```

### 2.3. Description
1. `UPDATE` only supports updating a single object, i.e., &quot;single-table-syntax&quot; but not &quot;multiple-table-syntax&quot;.
2. Only single-server scenarios are supported. Iterative versions in the XA scenario are implemented by proxy.
3. Three types of `INSERT` syntax are supported, and only one is described below.
4. For the standard syntax, please see the official documentation: [UPDATE Syntax](https://dev.mysql.com/doc/refman/5.7/en/update.html) and [INSERT Syntax](https://dev.mysql.com/doc/refman/5.7/en/insert.html).
1. Hotspot update is implemented on the object with the `expr` value specified by `QUEUE_ON_PK`. Generally, the `expr` value is a positive integer.
2. Parameter description:
   * `COMMIT_ON_SUCCESS`: immediately commits a successful update, which is applicable to a single statement as a transaction.
   * `ROLLBACK_ON_FAIL`: immediately performs rollback if update fails, which is applicable to a single statement as a transaction.
   * `QUEUE_ON_PK expr`: specifies the hotspot update object and locks/unlocks the updated object. The total number of updated objects cannot exceed `hot_commodity_query_size`, i.e., the number of `exprs` with different values cannot exceed `hot_commodity_query_size`. The value of `expr` is arbitrary, but it is recommended to keep it the same as the primary key (a different value is also acceptable though).
   * `TARGET_AFFECT_ROW expr`: specifies the data row affected by hotspot update, where `expr` is a positive integer ([1, MAX] with MAX being the maximum 8-digit number). Generally, `expr` is 1, indicating that only one row will be affected.

### 2.4. Suggestions
When using hotspot update, add all newly added parameters only to single-statement transactions. You are recommended to match the values in blue (this is not mandatory though).
```
UPDATE COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL QUEUE_ON_PK 88 TARGET_AFFECT_ROW 1 table_name  SET k=k+1 WHERE id=88
```

### 2.5. Sample code
```
CREATE DATABASE hc_db;

CREATE TABLE hc_tbl(a INT PRIMARY KEY, b INT, c INT);

CREATE TABLE hc_tbl_2(a INT PRIMARY KEY, b INT, c INT);
```

#### 2.5.1. Sample code of INSERT
```

INSERT COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL QUEUE_ON_PK 1 INTO hc_tbl VALUES(1, 1, 1);

INSERT COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL QUEUE_ON_PK 1 INTO hc_tbl SET a= 2;

INSERT COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL QUEUE_ON_PK 1 INTO hc_tbl_2 SELECT * FROM hc_tbl;
```

#### 2.5.2. Sample code of UPDATE
```
UPDATE COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL QUEUE_ON_PK 1 TARGET_AFFECT_ROW 1 hc_tbl SET b= b+1 WHERE a = 1;

`expr` in `QUEUE_ON_PK expr` is not necessarily the same as that in the WHERE clause.

UPDATE COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL QUEUE_ON_PK 2 TARGET_AFFECT_ROW 1 hc_tbl SET b= b+1 WHERE a = 1;
```

## 3. Newly Added Parameter Description
| Parameter Name | Feature | Type | Default Value | Remarks |
| --- | --- | --- | --- | --- |
|` hot_commodity`<br/>`_enable `| Enables/Disables hotspot update | Boolean | true: enables hotspot update | If this parameter is disabled during execution, hotspot update will no longer apply to new transactions. You are recommended to set it before the system starts instead of changing it during execution |
|` hot_commodity`<br/>`_trace` | Enables/Disables trace | Boolean | false: disables trace | When it is enabled, trace information will be exported to standard output |
| `hot_commodity`<br/>`_query_size` | Controls the number of hotspot objects that can be updated/inserted | Numeric | 10000 | It is used for throttling |
|` hot_commodity`<br/>`_query_size_modify_enable` | Controls whether <br/>`hot_commodity_query_size ` can be modified | Boolean | false: <br/>`hot_commodity`<br/>`_query_size ` cannot be modified | It facilitates the modification of <br/>`hot_commodity_query_size ` in unit test |

Note: when the MySQL server is started, if the `hot_commodity_enable` parameter is disabled, you need to enable it and restart the server before you can initialize the global data object table. However, if `hot_commodity_query_size` is 0, even after the `hot_commodity_enable` parameter is enabled, hotspot update will still be unavailable. Therefore, it is also necessary to set the following:

- `hot_commodity_enable`=ON
- `hot_commodity_query_size`=10000. This is a value greater than 0, which is recommended to be kept in the range of 10,000–20,000 and properly determined based on the hardware environment and application pressure.
- Start the server.

