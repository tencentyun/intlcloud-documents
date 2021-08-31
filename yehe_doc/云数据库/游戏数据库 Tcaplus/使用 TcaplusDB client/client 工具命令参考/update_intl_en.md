## Overview
This command is used to update a record in a table by explicitly declaring parameters or importing files.

## Syntax
```
## Explicitly Declaring Fields to Update Records
update table set value1 = 1, value2 = "abc", value3 = 0x123456 where key1 = 1 and key2 = "abc" and [-index = 1];
 
## Importing CSV Files to Replace Records
update table infile file name [where -index = 0];
 
## Importing XML Files to Replace Records
update table infile file name [where -index = 0] using tdr;
```

## Parameters

|  Parameter          | ProtoBuf                                      | TDR                             | Required       |
| --------- | ------------------------------------- | ------------------------------------------- | ------------ |
| table     | Table name                                   | Table name                                  | Yes           |
| key       | Primary key field name. All key values are required.             | Primary key field name. All key values are required.               | Yes       |
| value     | Non-primary key field name                  | Non-primary key field name                                 | At least one or \* |
| \-index   | LIST table: you must specify `\-index`. Only the specified record will be replaced.<br>GENERIC table: not supported | LIST table: if `\-index` is specified, the index-th record with the same key will be returned; if `\-index` is not specified, all records will be returned.<br>GENERIC table: not supported | No           |
| using tdr | Not supported                 | When data is output in XML format, the file structure must strictly comply with the XML syntax. A TDR file must be provided when client is launched. | No           |
| infile    | Read data from the file.                          | Read data from the file.                          | No           |


## Errors
Please refer to [Error Codes](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sample
```
tcaplus> update table_list set level=99 and count= 88 where uin=99 and name = "99" and key1=99 and -index=0;
 
update success
 
update time: 117086 us
```
