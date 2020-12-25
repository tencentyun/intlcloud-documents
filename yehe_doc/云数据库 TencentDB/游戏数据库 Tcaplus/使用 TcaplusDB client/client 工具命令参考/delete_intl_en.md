## Overview
This command is used to delete a record from a table by the specified key. If the `-index` parameter is not specified, all records that meet the condition will be deleted from the table.

## Syntax
```
delete from table where key1 = 1 and key2 = "abc" [and -index = 1] [by partkey];
```

## Parameters

|  Parameter          | Protobuf                                      | TDR                             | Required       |
| ---------- | ------------------------------------- | -------------------------------- | ------------ |
| table      | Table name                                        | Table name                                  | Yes           |
| key       | Primary key field name. All key values are required.             | Primary key field name. All key values are required.               | Yes       |
| value     | Non-primary key field name                  | Non-primary key field name                                 | Yes, at least one field name is required. |
| \-index   | LIST table: you must specify `\-index`. Only the specified record will be replaced.<br>GENERIC table: not supported | LIST table: if `\-index` is specified, the index-th record with the same key will be returned; if `\-index` is not specified, all records will be returned.<br>GENERIC table: not supported | No           |
| by partkey | Not supported         | LIST table: not supported <br> GENERIC table: delete records by partial keys      | No           |


## Errors
For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sample
```
tcaplus> delete from table_list where  uin=99 and name = "99" and key1=99 and -index=0;
 
delete success
 
delete time: 10263 us
 
tcaplus> delete from table_generic_xiahuaxian  where _uin=99 and name = "danmi_test_1" and _key3=4 by partkey;
 
delete success
 
delete time: 14405 us
```
