You can use the CREATE VIEW statement to create a view. A view is a virtual table based on the SELECT statement. Views can be used to define new virtual sources (type conversion, column conversion, virtual column, etc.), split long code, and so on.

#### Syntax
```
CREATE VIEW View name AS
SELECT Clause
```
#### Example 1
Create a view named MyView:
```
CREATE VIEW MyView AS
SELECT s1.time_, s1.client_ip, s1.uri, s1.protocol_version, s2.status_code, s2.date_
FROM KafkaSource1 AS s1, KafkaSource2 AS s2
WHERE s1.time_ = s2.time_ AND s1.client_ip = s2.client_ip;
```

#### Example 2
In calculations, due to a large amount of data and the matching requirements of function method types, TINYINT, SMALLINT, REAL and other types must be used. However, when a Stream Connector input type does not meet the requirements, a virtual view can be defined as a new source using the CREATE VIEW statement in conjunction with CAST() type conversion function (see [Type Conversion Function](/document/product/849/18079)).

In the following example, a view named KafkaSource2 is defined to convert a status_code column in the KafkaSource1 source from BIGINT type to VARCHAR type:
```
CREATE VIEW KafkaSource2 AS 
SELECT 
  `time_`,
  `client_ip`,
  `method`,
  CAST(`status_code` AS VARCHAR) AS status_code,
FROM KafkaSource1;
```
>**Notes:**
>Improper use of the CAST() data conversion function may result in accuracy loss, for example, from BIGINT to INTEGER or TINYINT. Please use it with caution.
>For the type conversion between a string (VARCHAR) and a timestamp (TIMESTAMP), see functions such as TO_TIMESTAMP, DATE_FORMAT_SIMPLE and DATE_FORMAT in [Time-related Functions](/document/product/849/18075).

