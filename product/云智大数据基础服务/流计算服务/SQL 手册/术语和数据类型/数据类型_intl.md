SCS employs the type definition conforming to ANSI SQL standards. The types allowed when you define a Stream Connector or a CKafka source or sink are limited, while those allowed when you define a CDB or a view can be all supported types.

## Types Allowed When Defining a Stream Connector or a CKafka Source or Sink Table
If Stream Connector or CKafka is used as source and sink tables, SCS supports the following data types:

| Type Name	| Description for Java Users |
| ------- | --------- |
| BIGINT |	It is equivalent to Java's Long type, which takes up 8 bytes. |
| DOUBLE	|	It is equivalent to Java's Double type, which takes up 8 bytes. |
| BOOLEAN	| It is equivalent to Java's Boolean type, which can be True or False. |
| TIMESTAMP	| Supports standard SQL timestamps in the format of YYYY-MM-DD HH:MM:SS<br>Also supports Unix timestamps (in ms), such as 1527501994642. |
| VARCHAR	| Indicates a string. It is equivalent to Java's String ring type with unlimited length. Size is not required.<br> It is compatible with VARCHAR (size), but the size can be set to any positive number, which has no actual meaning. |

## Types Allowed When Defining a CBD Source or Creating a VIEW
When you define a source with CDB (a relational database) or create a view (CREATE VIEW), and use CAST() for type conversion, this system supports the following data types:

| Type Name	| Description for Java Users |
| ------- | --------- |
| VARCHAR	| Indicates a string. It is equivalent to Java's String ring type with unlimited length. Size is not required. |
| BOOLEAN	| It is equivalent to Java's Boolean type, which can be True or False. |
| TINYINT	|	It is equivalent to Java's Byte type, which takes up 1 bytes. |
| SMALLINT |	It is equivalent to Java's Short type, which takes up 2 bytes. |
| INTEGER or INT	| It is equivalent to Java's Integer type, which takes up 4 bytes. |
| BIGINT	|	It is equivalent to Java's Long type, which takes up 8 bytes. |
| REAL or FLOAT |	It is equivalent to Java's Float type, which takes up 4 bytes. |
| DOUBLE |	It is equivalent to Java's Double type, which takes up 8 bytes. |
| DECIMAL	| It is equivalent to Java's BigDecimal, which represents large numbers and decimals with any precision. |
| DATE	| It is equivalent to java.sql.Date, which indicates the specified year, month and day (YYYY-MM-DD). |
| TIME	| It is equivalent to java.sql.Time, which indicates the specified hour, minute and second (YYYY-MM-DD). |
| TIMESTAMP	| Supports standard SQL timestamps in the format of YYYY-MM-DD HH:MM:SS, such as 2018-06-13 16:58:10.<br> Also supports Unix timestamps (in ms), such as 1527501994642. |
| INTERVAL YEAR TO MONTH	| Indicates the time period calculated by month. Data is stored internally in Integer type, which takes up 4 bytes. For more information, see [Time-related Functions](/document/product/849/18075). |
| INTERVAL DAY TO SECOND	| Indicates the time period calculated in ms. Data is stored internally in Long type, which takes up 8 bytes. For more information, see [Time-related Functions](/document/product/849/18075). |
| ARRAY	| Indicates an array, which corresponds to Java's array. For more information, see [Array Functions](https://cloud.tencent.com/document/product/849/18074?lang=cn#.E6.95.B0.E7.BB.84.E5.87.BD.E6.95.B0). |
| MAP	| Indicates map, which corresponds to Java's HashMap. For more information, see [Mapping Functions](https://cloud.tencent.com/document/product/849/18074?lang=cn#map-.E6.98.A0.E5.B0.84.E6.93.8D.E4.BD.9C.E5.87.BD.E6.95.B0). |
| MULTISET	| Indicates a collection of duplicate values allowed to be saved. |



























