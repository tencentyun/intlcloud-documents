Identifiers uniquely indicate table names or column names. The naming rules of identifiers in SCS are as follows:
-  The reserved words specified in [Data Type](/document/product/849/18119) cannot be used. If you must use a reserved word as table name or column name, enclose it in back quotes (\` \`), for example \`time\`.
-  Do not use PROCTIME as column name to avoid conflicts with system-generated timestamps.
-  Do not start with \_DataStreamTable\_.
-  If a table name or column name contains spaces or special characters, enclose it in back quotes, for example \`HELLO WORLD\`.
-  The length must be less than or equal to 128 characters (half-angle).

