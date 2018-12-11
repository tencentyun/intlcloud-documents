The CREATE TABLE statement is used to describe a source or a sink table.

**Syntax:**
```
CREATE TABLE `Table name` (
	`Field Name` Field Type
	[, `Field Name` Field Type ]*
	[, WATERMARK FOR BOUNDED (Name of the timestamp field, the maximum time allowed for out-of-order arrival) ]
	[, WATERMARK FOR ROWS (how many rows that can generate a Watermark) ]
	[, PRIMARY KEY (Primary key 1, ...) ]
) WITH (
	`Parameter Name` = 'Parameter Value'
	[, `Parameter Name` = 'Parameter Value' ]*
)
```
BOUNDED and ROWS belongs to Event Time mode, i.e., the source comes with a timestamp field. Both types of WATERMARK of ROWS are mutually exclusive, so only either of which can be selected.
The maximum time allowed for out-of-order arrival is meaningful in the Event Time mode, while the processing order cannot be guaranteed in the Processing Time mode because the source data comes with no timestamp.

**Example:**
```
CREATE TABLE KafkaSource1 (
  `time_` VARCHAR,
  `client_ip` VARCHAR,
  `method` VARCHAR(20),
) WITH (
  `type`='ckafka',
  `instanceId` = 'ckafka-cky18642',
  `encoding` = 'json',
  `topic` = 'test-input'
);
```

## Source and Sink
SCS can automatically determine the source and sink tables according to the subsequent INSERT INTO and SELECT FROM statements, so you don't need to explicitly specify the types of both tables, but should note that CDB (MySQL) can only be used as the source and applied to the right table in JOIN operations.

You can specify the type of source or sink in the WITH parameter of CREATE TABLE. For example, if type = 'cdp', Stream Connector is used, and if type = 'ckakfa', CKafka is used as the source.

>**Note:**
>The parameter after the equal sign must be enclosed in half-angle single quotation marks. Double quotation marks or full-angle quotation marks are not allowed. Generally, field names are not case-sensitive (e.g., `type` and `TYPE` are equivalent), but the string inside the single quotes is case-sensitive when referenced as an external value (e.g., `root` and `ROOT` are different as user names).

The following parameters are required for various types of source and sink:

### Stream Connector
| Parameter | Description |
| ----- | ----- |
| type	| "cdp" should be specified if source or sink is Stream Connector. |
| project	| The name of a Stream Connector project. |
| topic	| The topic of the project specified by Stream Connector. |
| startMode	| (Optional) Available values: EARLIEST (read from the earliest offset) and LATEST (read from the latest offset). |
| timestampMode | (Optional) It is used to specify the timestamp format for a source or sink table. It is "AUTO" by default. For a source table, the timestamp is determined depending on the format of input data (a value larger than 99999999999 is regarded as MILLISECOND, and that less than 99999999999 is regarded as SECOND). For a sink table, the timestamp is output as MILLISECOND format.<br> If it is explicitly specified as "MILLISECOND", a Unix timestamp in milliseconds is used. "SECOND" indicates a Unix timestamp in seconds.**<br> Note: **Since "AUTO" mode will judge each piece of data, which may slow the performance. In a low-latency and high-throughput environment, explicitly specify the timestampMode parameter for better performance. |

>**Note:**
> Stream Connector tables include Tuple and Upsert tables. A Tuple table does not have a primary key (i.e., it comes with no PRIMARY KEY statement), only supports the Append (data are only appended and those previously written are not updated) operation, and can receive the results of most queries (i.e. Append streams).

An Upsert table has a primary key (i.e., PRIMARY KEY is used to define the primary key), supports INSERT INTO and Upsert operations, and can receive Upsert streams (Upsert is short for Update OR Insert, that is, if a record with the same primary key as a piece of data has been previously output, the record is updated, otherwise new data is inserted) generated from DISTINCT, non-window-based JOIN, non-window-based GROUP BY and other operations. These Upsert streams can only be written into Stream Connector sink tables of Upsert type that cannot be used as source tables, and they should not be mixed.

**Example: Stream Connector source and sink tables of Tuple type in the Processing Time mode**
For more information on time modes and WATERMARK, see the [WATERMARK](https://cloud.tencent.com/document/product/849/18034#watermark) section below.
```
CREATE TABLE `traffic_output` (
  `f1` VARCHAR,
  `f2` BIGINT
) WITH (
  `type` = 'cdp',
  `project` = 'test',
  `topic` = 'Output',
  `startMode` = 'EARLIEST'
);
```
If the Processing Time mode is used, a Stream Connector Tuple table that contains f1, f2 and PROCTIME (automatically generated to indicate the timestamp of each record when it is processed, which can be used to describe the time window) columns is defined, which can be source or sink.

**Example: Stream Connector source and sink tables of Tuple type in the Event Time mode**
```
CREATE TABLE `public_traffic_output` (
  `rowtime` TIMESTAMP,
  `f1` VARCHAR,
  `f2` BIGINT,
  WATERMARK FOR BOUNDED(`rowtime`, 5000)    -- The timestamp field and the maximum allowable time range for out-of-order arrival of data used to define the Event Time mode.
) WITH (
  `type` = 'cdp',
  `project` = 'test',
  `topic` = 'Output'
);
```
If the Event Time mode is used for the table defined above, a Stream Connector Tuple table that contains f1 and f2 columns is defined, which can be a source or sink table.

**Example: Stream Connector sink table of Upsert type**
```
CREATE TABLE `public_traffic_output` (
  `f1` VARCHAR,
  `f2` BIGINT,
  PRIMARY KEY(`f1`)  -- The type of Stream Connector table used to define the primary key is Upsert
) WITH (
  `type` = 'cdp',
  `project` = 'test',
  `topic` = 'Output'
);
```
If the Processing Time mode is used for the table defined above, a Stream Connector Upsert table that contains f1 and f2 columns is defined, which can only be a sink table.

### CKakfa

| Parameter | Description |
| ----- | ----- |
| type	| "ckafka" should be specified if source or sink is CKafka. |
| instanceId	| The instanceId of CKafka. |
| encoding	| It can be json or csv. In case of csv, fieldDelimiter must also be specified. |
| topic	| The topic under the instanceId specified by Ckafka. |
| timestampMode | (Optional) It is used to specify the timestamp format for a source or sink table. It is "AUTO" by default. For a source table, the timestamp is determined depending on the format of input data (a value larger than 99999999999 is regarded as MILLISECOND, that less than 99999999999 is regarded as SECOND, and a string is regarded as SQL). For a sink table, the timestamp is output as MILLISECOND format.<br> If it is explicitly specified as "MILLISECOND", a Unix timestamp in milliseconds is used. "SECOND" indicates a Unix timestamp in seconds.** "SQL" means a string timestamp in the format of yyyy-MM-dd HH:mm:SS.<br>** Note: **Since "AUTO" mode will judge each piece of data, which may slow the performance. In a low-latency and high-throughput environment, explicitly specify the timestampMode parameter for better performance. |
| fieldDelimiter	| This is optional when encoding is CSV, which specifies the delimiter for each field of CSV. It is a comma (',') by default. |
| startMode	| (Optional) Available values: EARLIEST (read from the earliest offset), LATEST (read from the latest offset), and GROUP (read from the specified groupId that must be used). |
| groupId	| Specifies the groupId to be read (only for startMode = 'GROUP' mode). |
| ignoreErrors | (Optional) It is true by default, which means to skip wrong rows. If it is set to false, the program will be terminated directly in case of data error. |

>**Notes:**
>- If data contains the same character as the delimiter, it will be enclosed in double quotation marks to avoid ambiguity. If data itself contains double quotation marks, each double quote will be replaced with two double quotes ("").
>- CKafka only supports writing Append streams instead of Upsert streams. Use Stream Connector to write Upsert streams.

### CDB (only used as the right table in a JOIN condition)
| Field | Meaning |
| ----- | ----- |
| instanceId	| ID of the CDB instance (case-sensitive). |
| database |	Database name (case-sensitive). |
| table	| Table name (case-sensitive). |
| user |	Username (case-sensitive). |
| password	| Password (case-sensitive). |

## WATERMARK
### Event Time / Processing Time
For window-based operations (such as the assignment of time periods in GROUP BY, OVER, and JOIN conditions), SCS supports two time processing modes: Event Time and Processing Time.
![](https://main.qcloudimg.com/raw/18f11b8588bc8951b9215892d2982579.svg)
The Event Time mode uses the timestamp of the input data to tolerate a certain degree of out-of-order data input (for example, the earlier data arrived later due to unpredictable reasons such as the processing capacity of each node and network fluctuations), and this parameter can be specified by BOUNDED's second parameter (in milliseconds). It is the most accurate processing mode, but requires the input data to have a timestamp. Only fields defined by the timestamp type in the source are supported. Virtual columns will be supported in the future, and other types of columns can be converted into timestamps accepted by the system by applying processing functions.
The Processing Time mode does not require the input data to have a timestamp, but automatically adds the timestamp of the data when it is processed to the data and names it with the PROCTIME (uppercase) field. This column is hidden and will not appear when you perform SELECT *. It is read only when you use it manually.
>**Note:**
>Only one time mode is allowed for all sources of the same task. If the Event Time mode is used in a task, a timestamp must be defined for all defined Table Sources, and WATERMARK timestamp field must be declared.

### ROWS / BOUNDED
To process window-based data that contains timestamp information (columns are represented by timestamps in SQL format or UNIX timestamps), it is recommended to use Event Time mode. For example, if the data contains a generation_time field, and the maximum error allowed for out-of-order arrival is 1,000 milliseconds, then you can declare `WATERMARK FOR BOUNDED(`generation_time`, 1000)` to enable the Event Time mode.

**Example:**
If the data contains a generation_time field, and the maximum error allowed for out-of-order arrival is 1,000 milliseconds, you can declare:
WATERMARK FOR BOUNDED(`generation_time`, 1000) 

If you want Watermark to be generated once every 100 pieces of data, then you can declare:
WATERMARK FOR ROWS(`generation_time`, 100) 

The Event Time mode can be enabled for both declarations.

If you do not declare Watermark to specify a timestamp, the Processing Time mode is used. In this mode, Watermark is generated with the timestamp of the data when it is processed and will be used later, which cannot guarantee the order and accuracy. This mode is applicable to scenarios that do not require high time accuracy.




