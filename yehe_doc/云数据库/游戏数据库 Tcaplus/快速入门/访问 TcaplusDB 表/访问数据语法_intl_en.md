This document describes the syntax for using the client tool `tcaplus_client` to access data.
All data operation statements must carry the `WHERE` clause, which should contain at least a primary key field. If there are multiple primary keys, separate them with `and`.

### Inserting Data
Currently, the `INSERT` statement cannot be used; instead, you can run the `UPDATE` statement to insert a record.

### Modifying Data
You can run the `UPDATE` statement to write a record. If there are no records matching the primary key field value in the `WHERE` clause, the record will be added as a new one.
The syntax is `update table set field=value[,field 2=value 2…] where primary key field=value [and primary key field 2=value 2…];`
```
tcaplus>update tb_online set gamesvrid=4099, logintime=101 where uin=1024 and name="tcaplus_user" and region=10;
--------------------------------------------------------------------------------
        success. 
--------------------------------------------------------------------------------
update time: 5593 us
```

### Reading Data
You can run the `SELECT` statement to read some field data.
The syntax is `select field[,field 2…] from table where primary key field=value [and primary key field 2=value];`
The `recDataVersion` column in the input data indicates the version number of the current record.
```
tcaplus>select gamesvrid, logintime from tb_online where uin=1024 and name="tcaplus_user" and region=10;
+------+--------------+--------+------------------+--------------+-----------+
| uin  | name         | region | recDataVersion   | gamesvrid    | logintime |
+------+--------------+--------+------------------+--------------+-----------+
| 1024 | tcaplus_user | 10     | 2                | 4099         | 101       |
+------+--------------+--------+------------------+--------------+-----------+
totally 1 record(s) responded.
query time 8686 us
```
The syntax `select * from table where primary key field=value` is supported. Below is an example:
```
tcaplus>select * from test where id=1 and name=1;
+----+------+------------------+----+
| id | name | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
totally 1 record(s) responded.
query time 7537 us
```
The `\G` and `\P` formatted output modes are supported. `\G` indicates horizontal output by field, while `\P` indicates that data will be output as a table. Fields that are not configured with formatted output will be output in `\P` mode by default.
```
tcaplus>select * from hehe where id=1 and name=1 \G;
----------------------------------------1.row----------------------------------------
id: 1
name: 1
recDataVersion: 1
em: 1
responding record total:1
query time 3285 us
```

You can run the `SELECT` statement to export data into a file.
The syntax is `select * into [outfile] filename from table name where primary key=value [and primary key 2=value];`
```
tcaplus>select * into outfile test2.xml from hehe where id=1 and name=1;
+----+------+------------------+----+
| id | name | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
totally 1 record(s) responded.
query time 5399 us
```

### Deleting Data
You can run the `DELETE` statement to delete a written record.
The syntax is `delete from table name where primary key=value [and primary key 2=value];`
```
tcaplus>delete from hehe where id=4 and name=4;
--------------------------------------------------------------------------------
        success
--------------------------------------------------------------------------------
delete time 4280 us
```
