## Overview
This command is used to insert a data entry into a table by explicitly declaring parameters or importing files.

## Syntax
```
## Explicitly Declaring Parameters to Insert Data
insert into table (key1, key2, value1, vlaue2) values (1, "abc", 2, "def") [after -1] [shift none/head/tail];

## Importing a CSV File to Insert Data
insert into table infile result.csv [after -1] [shift none/head/tail];

## Importing an XML File to Insert Data Provided that the TDR File Is Provided at the Client’s Startup
insert into table infile result.xml [after -1] [shift none/head/tail] using tdr;
```

## Parameters

|  Parameter          | Protobuf and TDR                                    | Required       |
| --------- | ------------------------------------------------------------ | ------------ |
| table     | Table name                                                  | Yes           |
| key       | Primary key field name                                                   | Yes           |
| value     | Non-primary key field name                                                 | Yes, at least one |
| after     | LIST table: <br> n>0 indicates that the data will be inserted after the first n data<br>n=-2 indicates that the data will be inserted at the head of the queue<br>n=-1 indicates that the data will be inserted at the tail of the queue<br>n<-2: unsupported <br>GENERIC table: this field is unsupported. | No          |
| shift     | If the table size exceeds the maximum value, you can specify how to clear data automatically. Valid values: <br>`none`: no data will be cleared<br>`head`: data at the head of the queue will be cleared<br>tail: data at the tail of the queue will be cleared. | No |
| using tdr | The Protobuf table does not support this parameter. To insert data into the TDR table, import an XML file whose structure must strictly comply with the XML syntax. In addition, a TDR file must be provided when the client is started. | No           |
| infile    | Read data from the file                                             | No           |


## Errors
For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sample
Download the sample file [result.xml](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/result.xml) and [result.csv](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/result.csv).

```
tcaplus>insert into game_players (player_id,player_name,player_email,game_server_id) values (2,name,email,2);
insert success
 
insert time: 45322 us
 
tcaplus> Insert into table_list (uin, name, key1) values (99,99,99) after -1 shift tail;
 
insert success
 
insert time: 22464 us
 
tcaplus> Insert into table_list infile result.xml  using tdr;
 
 
insert success
 
insert time: 9493 us
 
tcaplus> Insert into table_list infile result.csv;
 
 
insert success
 
insert time: 22368 us
```

