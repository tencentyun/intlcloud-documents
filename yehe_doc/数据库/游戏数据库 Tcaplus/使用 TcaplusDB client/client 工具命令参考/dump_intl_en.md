## Overview
This command is used to export all data from a table to the console or to a file.

## Syntax
```
## Exporting Partial Fields
dump key1, key2, value1, value2 [into result.csv] from table limit 10;
 
## Exporting as an XML File
dump * [into filename] from table limit 10 using tdr;
 
## Exporting as a CSV File
dump * [into filename] from table limit 10;
```

## Parameters

|  Parameter          | Protobuf                                      | TDR                             | Required       |
| ----- | --------------------------------------------------- | ------------------------------------------------------- | ------ |
| table | Table name                                                   | Table name                                                   | Yes     |
| key   | Primary key field name. All key values are required.                                | Primary key field name. All key values are required.         | Yes     |
| value | Non-primary key field name                                                 | Non-primary key field name                                                 | No     |
| limit | LIST table: the number of exported keys. One key to multiple records.<br>GENERIC table: the number of exported records. One key to one record. | LIST table: the number of exported keys. One key to multiple records.<br>GENERIC table: the number of exported records. One key to one record. | No     |
| using | Not supported                                                       | When data is output in XML format, the file structure must strictly comply with the XML syntax. A TDR file must be provided when the client is launched.  | No     |
| into  | Export as a file.                                               | Export as a file.                                               | No     |


## Errors
For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sample

```
tcaplus> dump * from table_list limit 0;
uin,name,key1,level,count,array_count,items,c_int8,c_uint8,c_int16,c_uint16,c_int32,c_uint32,c_int64,c_uint64,c_float,c_double,c_string,c_string_128K,c_string_256K,c_binary,binary,selector,single_struct,simple_struct,single_union_selector,single_union,array,c_union,union_array,c_struct,struct_array
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
 
dump 4 records successful
 
dump time: 121671 us
 
tcaplus> dump * into table_list.txt from table_list limit 0;
 
dumped 4 records successful
 
tcaplus> dump * into table_list.xml from table_list limit 0 using tdr;
 
dumped 4 records successful
```
