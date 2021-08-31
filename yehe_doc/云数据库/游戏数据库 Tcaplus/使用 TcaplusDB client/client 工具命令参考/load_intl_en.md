## Overview
This command is used to import data in CSV or XML format to update or add records.

## Syntax
```
## Importing an XML File
load table infile filename using tdr;
 
## Importing a CSV File
load table infile filename;
```

## Parameters

|  Parameter          | Protobuf                                      | TDR                             | Required       |
| --------- | -------------- | ------------------------------------------------------------ | ------ |
| table     | Table name         | Table name                                                      | Yes     |
| using tdr | Not supported                 | When data in XML format is imported, the file structure must strictly comply with the XML syntax. A TDR file must be provided when the client is started. | No           |
| infile    | Read data from the file.                          | Read data from the file.                          | Yes           |

## Errors
For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sample
```
tcaplus> load table_list infile table_list_dump.xml using tdr;
loaded 49 records successful
 
tcaplus> load table_list infile table_list-dump.txt;
loaded 98 records successful
```
