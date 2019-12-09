>If you want to view or download the full set of development documents, see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).

The Percona 5.7 kernel of TDSQL supports storing JSON-formatted data, making JSON processing more efficient and enabling early detection of errors. If you want to use JSON types and enjoy the capabilities of traditional databases such as data consistency, transactions, and joins, TDSQL will be a good choice.
The JSON of TDSQL is based on MySQL and has some differences from MongoDB in terms of use. For more information, see [TDSQL vs MongoDB (JSON Capabilities)](https://intl.cloud.tencent.com/document/product/1042/33357) .
```
	mysql>  CREATE TABLE t1 (jdoc JSON,a int) shardkey=a;
	Query OK, 0 rows affected (0.30 sec)

	mysql> INSERT INTO t1 (jdoc,a)VALUES('{"key1": "value1", "key2": "value2"}',1);
	Query OK, 1 row affected (0.07 sec)

	mysql> INSERT INTO t1 (jdoc,a)VALUES('[1, 2,',5);
	ERROR 3140 (22032): Invalid JSON text: "Invalid value." at position 6 in value for column 't1.jdoc'.
	mysql> select * from t1;
	+--------------------------------------+------+
	| jdoc                                 | a    |
	+--------------------------------------+------+
	| {"key1": "value1", "key2": "value2"} |    1 |
	+--------------------------------------+------+
	1 row in set (0.03 sec)
```

Mixed-type sorting is not supported for `orderby` of JSON type, for example, you cannot compare string type with int type. Same-type sorting is supported only for value and string types and sorting for other types will not be processed.
