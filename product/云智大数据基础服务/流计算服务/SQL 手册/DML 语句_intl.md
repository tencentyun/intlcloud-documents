## INSERT INTO
The INSERT INTO statement must be used in conjunction with SELECT subqueries.

#### Syntax
```
INSERT INTO Sink
SELECT Clause
```

#### Example
Insert the result of a SELECT query into the sink named KafkaSink1:
```
INSERT INTO KafkaSink1
SELECT s1.time_, s1.client_ip, s1.uri, s1.protocol_version, s2.status_code, s2.date_
FROM KafkaSource1 AS s1, KafkaSource2 AS s2
WHERE s1.time_ = s2.time_ AND s1.client_ip = s2.client_ip;
```

## SELECT FROM
#### Syntax
```
SELECT Comma-separated fields to be selected
FROM Source or view
WHERE Filter condition
Other subqueries
```

#### Example
```
SELECT s1.time_, s1.client_ip, s1.uri, s1.protocol_version, s2.status_code, s2.date_
FROM KafkaSource1 AS s1, KafkaSource2 AS s2
WHERE s1.time_ = s2.time_ AND s1.client_ip = s2.client_ip;
```
>**Note:**
>SELECT cannot be used alone. It must be used with CREATE VIEW … AS or INSERT INTO, otherwise a prompt saying that no suitable operator exists will appear.

## WHERE
WHERE is used to filter query conditions (predicates). Multiple parallel conditions can be joined by AND/OR.
>**Note:**
>To JOIN with a table of an external CDB, only AND is used to join conditions. To use OR, see UNION ALL to achieve the same purpose.

## HAVING
HAVING is used to filter the results after GROUP BY. Note that WHERE is used before GROUP BY, and HAVING is used after GROUP BY.
#### Example
```
SELECT SUM(amount)
FROM Orders
WHERE price > 10
GROUP BY users
HAVING SUM(amount) > 50
```

## GROUP BY
In SCS, GROUP BY is used to group and aggregate results, including time window-based GROUP BY, and non-window-based GROUP BY (also known as persistent query). Since the former will not update the previous results, a data stream of Append type is generated, which can only be written into the Stream Connector sink of Tuple type or CKafka. However, the latter will update the previous records, so a data stream of Upsert type is generated, which can only be written into the Stream Connector sink of Upsert type.

#### Time window-based GROUP BY
This example defines the GROUP BY query statement containing a time window. For more information on how to use time window functions, see [Time-related Functions](/document/product/849/18075).
```
SELECT user, SUM(amount)
FROM Orders
GROUP BY TUMBLE(rowtime, INTERVAL '1' DAY), user
```
>**Note:**
>In the Event Time mode (where WATERMARK FOR BOUNDED is used to define the timestamp field), the first parameter of the TUMBLE window function must be this field. In the Processing Time mode, the first parameter of the TUMBLE window function must be PROCTIME (uppercase). This applies to both HOP and SESSION.

#### Non-window-based GROUP BY (persistent query)
This example defines the GROUP BY query statement that does not contain a time window, which is called persistent query. Because it calculates and determines whether to update the results issued previously based on each piece of new data, an Upsert stream is generated.
```
SELECT a, SUM(b) as d
FROM Orders
GROUP BY a
```
>**Note:**
>This method may cause memory overflow due to too many keys or too much data. So, be careful when setting the object timeout. Do not set this value too large.

## JOIN
SCS only supports Equi-JOIN (where the JOIN condition contains at least a filter condition that makes a field in the left table equivalent to that in the right table) and Inner JOIN. Outer JOIN will be available in future versions. 

### Inner Equi-JOIN between streams
There are two types of stream-stream JOIN: those with and without a time range. The former generates streams of Append type, while the latter generates streams of UP SERT type.
#### Stream-stream JOIN with a time range
The WEHERE condition of a JOIN with a time range contains at least an Equi-JOIN condition and a specified time range. The time range can be represented by <, <=, >=, >, or BETWEEN ... AND.

**Example of a time range:**
ltime = rtime
ltime >= rtime AND ltime < rtime + INTERVAL '10' MINUTE
ltime BETWEEN rtime - INTERVAL '10' SECOND AND rtime + INTERVAL '5' SECOND

**Exampe:**
```
SELECT *
FROM Orders o, Shipments s
WHERE o.id = s.orderId AND
o.ordertime BETWEEN s.shiptime - INTERVAL '4' HOUR AND s.shiptime
```
#### Stream-stream JOIN without a time range
It only needs at least one Equi-JOIN, and the time range is optional. That is, it calculates all active data in the history (inactive elements can be removed by specifying a timeout).
>**Notes:**
>It may take up too much memory and should be used with caution. Generally, an appropriate object timeout should be set to remove inactive objects in a timely manner.
>This query will generate an Upsert stream, and only a Stream Connector sink of Upsert type can be used to receive data.

**Example:**
```
SELECT *
FROM Orders INNER JOIN Product ON Orders.productId = Product.id
```

### JOIN between a stream and a CDB table
SCS also supports JOIN between a stream and a data table of CDB for MySQL. The syntax is the same as described above, but the CDB table must be the right table in a JOIN condition.
Note that a JOIN query condition should include all the defined keys of the table, otherwise the task will fail due to excessive query results and memory usage.

**Example:**
```
SELECT d.client_agent AS time_, d.client_ip, d.numbers AS request_body_length
FROM StreamSource AS s, DimSource AS d
WHERE s.client_ip = d.client_ip AND d.`month` LIKE  '20180%' AND ABS(d.numbers) BETWEEN 0 AND 2000
```

### JOIN with an array
Joining a defined array object (the value constructor in the section 4.10.4 can be used to construct an array object ARRAY) is also allowed by SCS.

**Example:** (if tags is a defined array)

```
SELECT users, tag
FROM Orders CROSS JOIN UNNEST(tags) AS t (tag)
```

## UNION ALL
UNION ALL is used to merge the results of two queries. Besides, since joining query conditions with OR is not supported in case of a JOIN between a stream and a CDB table, UNION ALL can also be used to achieve the same query result.

#### Example
```
SELECT *
FROM (
    (SELECT user FROM Orders WHERE a % 2 = 0)
  UNION ALL
    (SELECT user FROM Orders WHERE b = 0)
)
```

>**Note:**
>SCS only supports UNION ALL instead of UNION, which means de-duplication is not implemented in a row. To perform de-duplication to implement UNION, use it with DISTINCT. Note that DISTINCT will change the result from Append stream to Upsert stream, so only a Stream Connector sink of Upsert type can be used.

## OVER Window Aggregation
Use OVER to perform sliding-window aggregation (instead of GROUP BY aggregation) on data streams. You can specify PARTITION, ORDER, window range and other parameters in OVER.

#### Example
The following example defines a sliding-window aggregation query to calculate the amount of a sliding window with a size of 3. Perform PRECEDING on the previous rows, but FOLLOWING is not supported.
In addition, only one timestamp filed can be placed after ORDER BY. In this example, the PROCTIME column is automatically added by the system in the Processing Time mode.
```
SELECT SUM(amount) OVER (
  PARTITION BY user
  ORDER BY PROCTIME
  ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)
FROM Orders
```

## ORDER BY
ORDER BY is used to sort the results of a query. The default value is ASC (ascending order), or you can also explicitly specify DESC (descending order).
>**Note:**
>The first sorting item must be the time-based column (Event Time timestamp, or Processing Time timestamp, i.e. PROCTIME) in ascending order, and other sorting items can be freely specified.

#### Example
```
SELECT *
FROM Orders
ORDER BY `orderTime`, `username` DESC, `userId` ASC 
```

## DISTINCT
DISTINCT is used to de-duplicate query results, which must be placed after SELECT.
#### Example
```
SELECT DISTINCT users FROM Orders
```
>**Notes:**
>DISTINCT will generate an Upsert stream, so only a sink of Upsert type can receive its results. Moreover, queries that take a long time may lead to excessive memory usage. Please use it with caution.
>Set an appropriate object timeout to remove inactive objects in time to save memory.

## Syntax Structures Not Yet Supported
The following SQL syntax structures are not supported:
GROUPING SETS, ROLLUP, CUBE, IN, UNION (which can be implement using UNION ALL and DISTINCK), LIMIT, etc. More syntaxes will be available in future versions, such as real-time query of Top data.


