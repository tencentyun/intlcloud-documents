[//]: # (chinagitpath:XXXXX)

This document is the Tcaplus RESTful API v1.0 User Manual.

## Overview

Tcaplus RESTful API allows developers to remotely interact with the Tcaplus database through HTTP requests. After sending an HTTP request where data is transferred in JSON format by calling the RESTful API, you will receive a response package in JSON format. Developers can send RESTful API requests using any language or tool to add, delete, update and query data.

## Preparations

Make sure that you have created a game App on [Tencent Cloud TcaplusDB](https://intl.cloud.tencent.com/product/tcaplus), and obtained the App information (including AppID, ZoneID, and AppKey). Tcaplus RESTful API only supports tables that are defined using protobuf.
Here is an example of a Tcaplus protobuf table definition file:

```
syntax = "proto2";
package myTcaplusTable;

import "tcaplusservice.optionv1.proto"; // Defines some common information of the Tcaplus table, which should be imported in your table definition.

message tb_example {  // If a message is explicitly specified with a primary key field, then it is a Tcaplus table definition. The table name is the name of the message. The names of table creation files that are uploaded in the same batch must be different.

    // tcaplusservice.tcaplus_primary_key specifies the list of primary key field names that are separated by commas. Up to four primary keys can be specified.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // The tcaplusservice.tcaplus_index option specifies the Tcaplus index.
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // The following shows the definition of table fields.
    // A Tcaplus table supports the following data types:
    // Non-nested: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Nested: message
    // Tcaplus supports three field modifiers: REQUIRED, OPTIONAL and REPEATED.

    // Primary key fields (4 at most)
    required int64 uin = 1;  // The primary key fields must be declared with the modifier REQUIRED. Nested data types are not supported.
    required string name = 2;  // A table can contain up to four primary key fields.
    required int32 region = 3;

    // Common value field.
    required int32 gamesvrid = 4; // Common fields can be declared as either REQUIRED, OPTIONAL and REPEATED modifiers. 
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // The packed=true option should be specified for the fields declared with the modifier REPEATED.
    optional bool is_available = 7 [default = false]; // A default value can be specified for optional-type fields.
    optional pay_info pay = 8; // The type of the value field can be a custom structure type.
}

message pay_info { //If a message is not explicitly specified with a primary key field, it is only a common custom structure and cannot be recognized as a Tcaplus table.
    required int64 pay_id = 1;
    optional uint64 total_money = 2;
    optional uint64 pay_times = 3;
    optional pay_auth_info auth = 4;

    message pay_auth_info { // The structure type supports nested definitions.
        required string pay_keys = 1;
        optional int64 update_time = 2;
    }
}
```

>
* If a message is explicitly specified with a primary key field, then it is a Tcaplus table definition. The table name is the name of the message. The names of table creation files that are uploaded in the same batch must be different.
* If a message is not explicitly specified with a primary key field, it is only a common custom structure and cannot be recognized as a Tcaplus table.
* The `tcaplusservice.optionv1.proto` file defines some common information of the Tcaplus table, which should be imported in your table definition.
* Tcaplus tables support both nested and non-nested type fields.
* Tcaplus supports three field modifiers: REQUIRED, OPTIONAL and REPEATED.
* The primary key fields must be declared with the modifier REQUIRED. Nested data types are not supported.
* Common fields can be declared as either REQUIRED, OPTIONAL and REPEATED modifiers. 
* The packed=true option should be specified for the fields declared with the modifier REPEATED.
* The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty.

## Current Version

By default, the version of Tcaplus RESTful API is ver1.0.

## Request

All API access requests are sent via HTTP, and all data is transferred in JSON format. Here is a typical format for access request URI:

```
http://{Tcaplus_REST_URL}/{Version}/apps/{AppId}/zones/{ZoneId}/tables/{TableName}/records
```
* Tcaplus_REST_URL: Tcaplus RESTful URL Access point
* Version: Tcaplus RESTful API Version number, which defaults to "ver1.0".
* AppID: App ID
* ZoneID: Zone ID
* TableName: Table name

Example:
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_rest_test/records
```

### HTTP header

Set HTTP headers to allow users to transfer additional information through requests and responses at the HTTP client.

#### Authentication

`x-tcaplus-pwd-md5`
Fill in this field with the calculated MD5 of the user's app key, which is used to authenticate the client's access to the data.
Calculate the MD5 of the string using the bash command:
```
# echo -n "c3eda5f013f92c81dda7afcdc273cf82" | md5sum
879423b88d153cace7b31773a7f46039  -
```

#### Operation check 

- `x-tcaplus-target` specifies Tcaplus RESTful API request operations, including:
 * Tcaplus.GetRecord : Gets records
 * Tcaplus.AddRecord : Inserts records
 * Tcaplus.SetRecord : Sets records
 * Tcaplus.DeleteRecord : Deletes records
 * Tcaplus.FieldGetRecord : Reads partial fields
 * Tcaplus.FieldSetRecord : Sets partial fields
 * Tcaplus.FieldIncRecord : Auto-increment of partial fields
 * Tcaplus.PartkeyGetRecord : Batch reading of indexes
- `x-tcaplus-idl-type`  specifies Tcaplus table types. Only protobuf (pb) is supported.


#### Labeling 

- `x-tcaplus-data-version-check` specifies the Tcaplus data version check policy to implement the optimistic locking feature, which is to be used with `x-tcaplus-data-version` labeling. Selectable values include:

* `1`: Write operations can be performed only when the data version number at the client is identical to that at the storage layer. The version number will be increased by 1 each time when this operation is performed.
 * `2`: The relationship between the client version number and the server version number is ignored. The client version number is forcibly set to the storage layer.
* `3`: The relationship between the client version number and the server version number is ignored. The version number at the storage layer will be increased by 1 each time when the write operation is performed.

 These labels are only applicable to Tcaplus.AddRecord and Tcaplus.SetRecord.

- `x-tcaplus-data-version` is used with `x-tcaplus-data-version-check` to set the data version number of the client. Selectable values include:
 * version <= 0 means to ignore the version check policy.
 * version > 0 means to specify the version number of the data record at the client.
- `x-tcaplus-result-flag` sets whether the response contains the complete data policy. Selectable values include:
 * `0`: The response only contains whether the request succeeded or failed.
 * `1`: The response only contains the updated values of the fields that have been modified.
 * `2`: The response contains the updated values of the fields that have been modified and all other values of this record.
 * `3`: The response contains the value before the record is modified.


### JSON request data 

```
Request Data:
{
 "ReturnValues": "...", // The retention data set by the user, which arrives at tcaplus along with the request and is returned as is in the response.
 "Record": {
     ... // For the format of data records, see "API Example".
 }
}
```

## Respond

### JSON response data

The GetRecord/SetRecord/AddRecord/DeleteRecord/FieldGetRecord/FieldSetRecord/FieldIncRecord operation returns a single data entry. The JSON response data is as below:

```
Response Data
{
 "ErrorCode": 0, // Error code
 "ErrorMsg": "Succeed", // Return message
 "RecordVersion": 1, // Data version number
 "ReturnValues": "...", // The retention data set by the user, which arrives at tcaplus along with the request and is returned as is in the response.
 "Record": { // For the format of data records, see "API Example".
     ...
 }
}
```

The PartkeyGetRecord operation may return multiple data entries. The JSON response data is as below:

```
Response Data
{
 "ErrorCode": 0, // Error code
 "ErrorMsg": "Succeed", // Return message
 "MultiRecords": [ // An array consisting of multiple data entries
  {"RecordVersion": 1,  // The version number of each data entry
   "Record": {...}  // For the format of data records, see "API Example".
  },
  ...
  ],
 "RemainNum": 0, // Number of data entries not arrived yet
 "TotalNum": 5   // Total number of data entries that meet the condition
}
```

### Error code 

| HTTP Status Code | Error Code | Return Message |
| -----------------|-------------- | ------------ |
| 200 | 0 | Successful |
| 400 | -2579 | Data deserialization error |
| 401 | -279 | Authentication error |
| 400 | -11539 | Invalid request<br>For the detailed reason, see the return message field. |
| 400 | -2067 | Operation type mismatch |
| 400 | -1811 | Invalid parameter |
| 400 | -5395 | No primary key is set |
| 400 | -2323 | Data serialization error |
| 400 | -7949 | Invalid data version number<br>This error generally occurs when the data version check policy is used in a write operation. |
| 400 | -1293 | The record already exists. |
| 404 | 261 | The record does not exist. |
| 404 | -34565 | The index does not exist. |
| 500 | - | Internal system error<br>See the return message field. |

## API Examples 

### Tcaplus.GetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```
This API is used to specify the key information of a record to query this record from a Tcaplus pb table. You will get the entire record by performing this operation. However, you can set the select variable to specify the fields to be returned in the response; otherwise, the information of all fields is displayed. If no data record exists, an error is returned.

The `keys` variable must be specified in the URI, which indicates the values of all primary keys. The select variable, which is optional, indicates the name of the field whose value you want displayed. You can specify the fields in the nested structure by separating the path with a dot, such as "pay.total_money".

> The request variables must be URL-encoded.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.GetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |


#### Example:

##### URL:
- URL encoding is not used:
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'region': 101, 'name': 'calvinshao', 'uin': 100}
```
- URL encoding is used:
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22region%22%3A%20101%2C%20%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D
```

##### HTTP request header:
```
[
 "x-tcaplus-target:Tcaplus.GetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-idl-type:protobuf"
]
```

##### Response data:

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "ErrorMsg": "Succeed",
 "RecordVersion": 1,
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70
  ],
  "pay": {
   "pay_times": 2,
   "total_money": 10000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": true,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```

### Tcaplus.SetRecord 
```
PUT /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```

This API is used to specify the key information of a record to set this record. If the record exists, an overwrite operation will be performed, otherwise an insert operation will be performed. |

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Example:
##### URL:
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### HTTP request header:
```
[
 "x-tcaplus-target:Tcaplus.SetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:2",
 "x-tcaplus-data-version-check:2",
 "x-tcaplus-data-version:-1",
 "x-tcaplus-idl-type:Protobuf"
]
```
##### JSON request data
```
{
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70,
   80,
   90,
   100
  ],
  "pay": {
   "pay_times": 3,
   "total_money": 12000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": false,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```

##### JSON response data
```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 1,
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70,
   80,
   90,
   100
  ],
  "pay": {
   "pay_times": 3,
   "total_money": 12000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": false,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```

###  Tcaplus.AddRecord 
```
POST /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```
This API is used to specify the key information of a record to insert this record. If the record exists, an error is returned.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Example:

##### URL:
```
 http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records
```
##### HTTP request header:

```
[
 "x-tcaplus-target:Tcaplus.AddRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:1",
 "x-tcaplus-idl-type:protobuf"
]
```

##### JSON request data

```
{
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70
  ],
  "pay": {
   "pay_times": 2,
   "total_money": 10000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": true,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```

##### JSON response data:

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 1,
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70
  ],
  "pay": {
   "pay_times": 2,
   "total_money": 10000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": true,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```



###  Tcaplus.DeleteRecord 

```
DELETE /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records

```

This API is used to specify the key information of a record to delete this record. If the data does not exist, an error is returned.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Example:

##### URI:
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### HTTP request header:

```
[
 "x-tcaplus-target:Tcaplus.DeleteRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:1",
 "x-tcaplus-idl-type:protobuf"
]
```

##### JSON request data

```
{
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "region": 101,
  "name": "calvinshao",
  "uin": 100
 }
}
```

##### JSON response data:
```
{
 "ErrorCode": 0,
 "Record": {},
 "RecordVersion": -1,
 "ReturnValues": "Send to tcaplus by calvinshao"
}
```



###  Tcaplus.FieldGetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```

This API is used to specify the key information of a record to query this record from a Tcaplus pb table. This operation only supports querying and transferring the values of the fields specified via the select variable to minimize the traffic in network transmission, which is the biggest difference from the GetRecord operation. If no record exists, an error is returned.
Both `keys` and `select` variables must be specified in the URI. The former indicates the values of all primary keys, and the latter indicates the name of the field whose value you want displayed. You can also specify the fields in the nested structure by separating the path with a dot, such as "pay.total_money".

>! The request variables must be URL-encoded.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.FieldGetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |

#### Example:

##### URL encoding is not used:

```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'region': 101, 'name': 'calvinshao', 'uin': 100}&select=['gamesvrid', 'lockid', 'pay.auth.pay_keys', 'pay.total_money']
```

##### URL encoding is used:

```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22region%22%3A%20101%2C%20%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D&select=%5B%22gamesvrid%22%2C%20%22lockid%22%2C%20%22pay.auth.pay_keys%22%2C%20%22pay.total_money%22%5D
```

##### HTTP request header:

```
[
 "x-tcaplus-target:Tcaplus.FieldGetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-idl-type:protobuf"
]
```

##### JSON response data:

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 1,
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70
  ],
  "pay": {
   "total_money": 10000,
   "auth": {
    "pay_keys": "adqwacsasafasda"
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 4099
 }
}
```

###  Tcaplus.FieldSetRecord  

```
PUT /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```


This API is used to specify the key information of a record to modify this record. Different from SetRecord, this operation only supports transferring and setting the values of specified fields rather than all fields, which can minimize the network traffic. If the data record exists, it will be updated; otherwise, an error is returned.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Example:

##### URL:

```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records

```

##### HTTP request header:

```
[
 "x-tcaplus-target:Tcaplus.FieldSetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:1",
 "x-tcaplus-data-version-check:1",
 "x-tcaplus-data-version:-1",
 "x-tcaplus-idl-type:Protobuf"
]

```
##### JSON request data

```
{
 "ReturnValues": "aaaaaaaaaa",
 "Record": {
  "name": "calvinshao",
  "pay": {
   "total_money": 17190,
   "auth": {
    "pay_keys": "bingo"
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 1719,
  "logintime": 1719
 }
}
```

##### JSON response data:

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 3,
 "ReturnValues": "aaaaaaaaaa",
 "Record": {
  "name": "calvinshao",
  "pay": {
   "total_money": 17190,
   "auth": {
    "pay_keys": "bingo"
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 1719,
  "logintime": 1719
 }
}
```


### Tcaplus.FieldIncRecord 

```
PUT /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```


This API is used to specify the key information of a record to perform auto-increment on specified fields. This command word only supports `int32`, `int64`, `uint32` and `uint64` fields. It has the same feature as FieldSetRecord.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Example:

##### URL:

```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### HTTP request header:

```
[
 "x-tcaplus-target:Tcaplus.FieldIncRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:1",
 "x-tcaplus-data-version-check:1",
 "x-tcaplus-data-version:-1",
 "x-tcaplus-idl-type:Protobuf"
]
```

##### JSON request data

```
{
 "ReturnValues": "aaaaaaaaaa",
 "Record": {
  "name": "calvinshao",
  "pay": {
   "total_money": -1, 
   "auth": {
    "update_time": -1
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 2,
  "logintime": -2
 }
}
```

##### JSON response data:

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 9,
 "ReturnValues": "aaaaaaaaaa",
 "Record": {
  "name": "calvinshao",
  "pay": {
   "total_money": 11999,
   "auth": {
    "update_time": 921
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 4101,
  "logintime": 98
 }
}
```


###  Tcaplus.PartkeyGetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```

This API is used to specify the values of partial primary keys to query multiple records. Multiple data entries will be returned and displayed with the names of the fields specified using the select variable. An index must be created for the primary key set when you create a table; otherwise, an error is returned.

The `keys` variable must be specified in the URI, which specifies the values of all primary keys. The select variable, which is optional, specifies the name of the field whose value is displayed. You can specify the fields in the nested structure by separating the path with a dot, such as "pay.total_money".

> The request variables must be URL-encoded.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.GetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |


#### Example:

##### URL encoding is not used:

```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'name': 'calvinshao', 'uin': 100}&select=['gamesvrid', 'lockid', 'pay.total_money', 'pay.auth.pay_keys']
```

##### URL encoding is used:
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D&select=%5B%22gamesvrid%22%2C%20%22lockid%22%2C%20%22pay.total_money%22%2C%20%22pay.auth.pay_keys%22%5D
```

##### HTTP request header:
```
[
"x-tcaplus-target:Tcaplus.PartkeyGetRecord",
"x-tcaplus-version:Tcaplus3.32.0",
"x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
"x-tcaplus-idl-type:protobuf"
]
```



##### Response data:

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "MultiRecords": [
  {
   "RecordVersion": 9,
   "Record": {
    "name": "calvinshao",
    "lockid": [
     50,
     60,
     70,
     80,
     90,
     100
    ],
    "pay": {
     "total_money": 11999,
     "auth": {
      "pay_keys": "adqwacsasafasda"
     }
    },
    "region": 101,
    "uin": 100,
    "gamesvrid": 4101
   }
  },
  {
   "RecordVersion": 1,
   "Record": {
    "name": "calvinshao",
    "lockid": [
     50,
     60,
     70,
     80
    ],
    "pay": {
     "total_money": 10000,
     "auth": {
      "pay_keys": "adqwacsasafasda"
     }
    },
    "region": 102,
    "uin": 100,
    "gamesvrid": 4100
   }
  },
  {
   "RecordVersion": 1,
   "Record": {
    "name": "calvinshao",
    "lockid": [
     60,
     70,
     80,
     90
    ],
    "pay": {
     "total_money": 10000,
     "auth": {
      "pay_keys": "adqwacsasafasda"
     }
    },
    "region": 103,
    "uin": 100,
    "gamesvrid": 4101
   }
  }
 ],
 "RemainNum": 0,
 "TotalNum": 3
}
```

