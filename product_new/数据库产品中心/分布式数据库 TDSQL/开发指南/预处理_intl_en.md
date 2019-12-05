
> If you want to view or download the full set of development documents, see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).

### Preprocessing

**TDSQL supports preprocessing, which are used in the same way as in standalone MySQL. Below are some examples:**

- PREPARE Syntax
- EXECUTE Syntax

Supported binary protocols:

- COM_STMT_PREPARE
- COM_STMT_EXECUTE

Example:
```
	mysql> select * from test1;
	+---+------+
	| a | b    |
	+---+------+
	| 5 |    6 |
	| 3 |    4 |
	| 1 |    2 |
	+---+------+
	3 rows in set (0.03 sec)

	mysql> prepare ff from "select * from test1 where a=?";
	Query OK, 0 rows affected (0.00 sec)
	Statement prepared

	mysql> set @aa=3;
	Query OK, 0 rows affected (0.00 sec)

	mysql> execute ff using @aa;
	+---+------+
	| a | b    |
	+---+------+
	| 3 |    4 |
	+---+------+
	1 row in set (0.06 sec)
```
