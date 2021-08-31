This document is the TcaplusDB RESTful API v1.0 User Manual.

## Overview
TcaplusDB RESTful API enables you to remotely interact with TcaplusDB through HTTP requests. After sending an HTTP request where data is transferred in JSON format by calling the RESTful API, you will receive a response package in JSON format. You can send RESTful API requests in any programming language or tool to perform CRUD operations on data.

## Preparations

Make sure that you have created a cluster in the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/app) and obtained the corresponding cluster information, including `AppId` (cluster access ID), `ZoneId` (table group ID), and `AppKey` (cluster access password). Currently, TcaplusDB RESTful API only supports tables defined through protobuf.

## Current Version

By default, the version of TcaplusDB RESTful API is v1.0.

## Request

All API call requests are sent over HTTP, and all data is transferred in JSON format. Below is a typical format for access request URI:

```
http://{Tcaplus_REST_URL}/{Version}/apps/{AppId}/zones/{ZoneId}/tables/{TableName}/records
```
* Tcaplus_REST_URL: TcaplusDB RESTful URL access point
* Version: TcaplusDB RESTful API version number, which is "ver1.0" by default
* AppId: cluster **access ID**
* ZoneId: table group **ID**
* TableName: table name

Sample code:
```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_rest_test/records
```

### HTTP header

Setting HTTP headers allows you to transfer additional information through requests and responses at the HTTP client.

#### Authentication

`x-tcaplus-pwd-md5`
Fill in this field with the calculated MD5 of your `app key`, which is used to authenticate the client's access to the data.
Calculate the MD5 of the string by running the `bash` command:
```
# echo -n "c3eda5f013f92c81dda7afcdc273cf82" | md5sum
879423b88d153cace7b31773a7f46039  -
```

#### Operation check 

- `x-tcaplus-target` specifies TcaplusDB RESTful API request operations, including:
 * Tcaplus.GetRecord   Gets record
 * Tcaplus.AddRecord   Inserts record
 * Tcaplus.SetRecord   Sets record
 * Tcaplus.DeleteRecord   Deletes record
 * Tcaplus.FieldGetRecord   Reads specified fields
 * Tcaplus.FieldSetRecord   Sets specified fields
 * Tcaplus.FieldIncRecord   Auto-increments specified fields
 * Tcaplus.PartkeyGetRecord   Batch reads indexes
- `x-tcaplus-idl-type` specifies the TcaplusDB table type. Currently, only the protobuf (pb) type is supported.


#### Setting tag 

- `x-tcaplus-data-version-check` Specifies TcaplusDB data version check policy use with `x-tcaplus-data-version`. It can be set as:
`x-tcaplus-data-version-check` specifies the TcaplusDB data version check policy to implement the optimistic locking feature, which is to be used with `x-tcaplus-data-version` tagging. Valid values include:

 * `1`: write operations can be performed only if the data version number at the client is identical to that at the storage layer. The version number will be increased by 1 each time this operation is performed.
 * `2`: the relationship between the client version number and the server version number is ignored. The client version number will be forcibly set at the storage layer.
 * `3`: the relationship between the client version number and the server version number is ignored. The version number at the storage layer will be increased by 1 each time the write operation is performed.

 These tags are only applicable to `Tcaplus.AddRecord` and `Tcaplus.SetRecord`.

- `x-tcaplus-data-version` is used with `x-tcaplus-data-version-check` to set the data version number of the client. Valid values include:
 * version <= 0 means to ignore the version check policy.
 * version > 0 means to specify the version number of the data record at the client.
- `x-tcaplus-result-flag` sets whether the response contains the complete data policy. Valid values include:
 * `0`: the response only contains whether the request succeeded or failed.
 * `1`: the response contains the same values as the request does.
 * `2`: the response contains the latest values of all fields of the data that has been modified.
 * `3`: the response contains the value before the record is modified.


### JSON request data 

```
Request Data:
{
 "ReturnValues": "...", // The data you configure to be retained, which will arrive at TcaplusDB with the request and be sent back as-is
 "Record": {
     ... // For the format of data records, please see "API Samples".
 }
}
```

## Response

### JSON response data

The `GetRecord/SetRecord/AddRecord/DeleteRecord/FieldGetRecord/FieldSetRecord/FieldIncRecord` operation returns a single data entry. The JSON response data is as below:

```
Response Data
{
 "ErrorCode": 0, // Return code
 "ErrorMsg": "Succeed", // Return message
 "RecordVersion": 1, // Data version number
 "ReturnValues": "...", // The data you configure to be retained, which will arrive at TcaplusDB with the request and be sent back as-is
 "Record": { // For the format of data records, please see "API Samples".
     ...
 }
}
```

The `PartkeyGetRecord` operation may return multiple data entries. The JSON response data is as below:

```
Response Data
{
 "ErrorCode": 0, // Return code
 "ErrorMsg": "Succeed", // Return message
 "MultiRecords": [ // Array of multiple data entries
  {"RecordVersion": 1,  // Version number of each data entry
   "Record": {...}  // For the format of data records, please see "API Samples".
  },
  ...
  ],
 "RemainNum": 0, // Number of data entries not accessed yet
 "TotalNum": 5   // Total number of eligible data entries
}
```

### Return codes 

|HTTP Status Code       | Return Code    | Return Message |
| -----------------|-------------- | ------------ |
| 200 | 0 | Successful |
| 400 | -2579 | Data deserialization error |
| 401 | -279 | Authentication error |
| 400 | -11539 | Invalid request <br>For the detailed reason, please see the return message field. |
| 400 | -2067 | Operation type mismatch |
| 400 | -1811 | Invalid parameter |
| 400 | -5395 | No primary key is set |
| 400 | -2323 | Data serialization error |
| 400 | -7949 | Invalid data version number <br>This error generally occurs when the data version check policy is used in a write operation |
| 400 | -1293 | The record already exists |
| 404 | 261 | The record does not exist |
| 404 | -34565 | The index does not exist |
| 500 | - | Internal system error <br>Please see the return message field |

## API Samples 

### Tcaplus.GetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```
This API is used to query a record by specifying its `key` information in a TcaplusDB PB table. You will get the entire record by performing this operation. However, you can set the `select` variable to specify the fields to be returned in the response; otherwise, the information of all fields will be displayed. If no data records exist, an error will be returned.

The `keys` variable must be specified in the URI, which indicates the values of all primary keys. The optional `select` variable indicates the name of the field whose value you want to display. You can specify the fields in the nested structure by separating the path with a dot, such as `pay.total_money`.

>! The variables in the request must be URL-encoded. Please encode the space in the URL as `%20` instead of `+`.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.GetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |


#### Sample

##### URL
- If URL is not URL-encoded:
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'region': 101, 'name': 'calvinshao', 'uin': 100}
```
- If URL is URL-encoded:
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22region%22%3A%20101%2C%20%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D
```

##### HTTP request header
```
[
 "x-tcaplus-target:Tcaplus.GetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-idl-type:protobuf"
]
```

##### Response data

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

This API is used to set a record by specifying its `key` information. If the record already exists, an overwrite operation will be performed; otherwise, an insert operation will be performed.

The `SetRecord` operation supports setting the following values for `resultflag`:

* `0`: the response only contains whether the request succeeded or failed
* `1`: the response contains the same values as the request does
* `2`: the response contains the latest values of all fields of the data that has been modified
* `3`: the response contains the value before the record is modified

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Sample
##### URL
```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### HTTP request header
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

### Tcaplus.AddRecord 
```
POST /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```
This API is used to insert a record by specifying its `key` information. If the record already exists, an error will be returned.

The `AddRecord` operation supports setting the following values for `resultflag`:

* `0`: the response only contains whether the request succeeded or failed
* `1`: the response contains the same values as the request does
* `2`: the response contains the latest values of all fields of the data that has been modified
* `3`: the response contains the value before the record is modified

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Sample

##### URL
```
 http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records
```
##### HTTP request header

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



### Tcaplus.DeleteRecord 

```
DELETE /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records

```

This API is used to delete a record by specifying its `key` information. If the data does not exist, an error will be returned.

The `DeleteRecord` operation supports setting the following values for `resultflag`:

* `0`: the response only contains whether the request succeeded or failed
* `1`: the response contains the same values as the request does
* `2`: the response contains the latest values of all fields of the data that has been modified
* `3`: the response contains the value before the record is modified

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Sample

##### URI
```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### HTTP request header

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

##### JSON response data
```
{
 "ErrorCode": 0,
 "Record": {},
 "RecordVersion": -1,
 "ReturnValues": "Send to tcaplus by calvinshao"
}
```



### Tcaplus.FieldGetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```

This API is used to query a record by specifying its `key` information in a TcaplusDB pb table. This operation only queries and transfers the values of the field you specify through the `select` variable, which will reduce the network transfer traffic usage and is the biggest difference from the `GetRecord` operation. If the data record does not exist, an error will be returned.
The `keys` and` select` variables must be specified in the URI. `keys` specifies the values of all primary keys. `select` specifies the name of the field whose value you want to display. You can specify the fields in the nested structure by separating the path with a dot, such as `pay.total_money`.

>! The variables in the request must be URL-encoded. Please encode the space in the URL as `%20` instead of `+`.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.FieldGetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |

#### Sample

##### If URL is not URL-encoded

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'region': 101, 'name': 'calvinshao', 'uin': 100}&select=['gamesvrid', 'lockid', 'pay.auth.pay_keys', 'pay.total_money']
```

##### If URL is URL-encoded

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22region%22%3A%20101%2C%20%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D&select=%5B%22gamesvrid%22%2C%20%22lockid%22%2C%20%22pay.auth.pay_keys%22%2C%20%22pay.total_money%22%5D
```

##### HTTP request header

```
[
 "x-tcaplus-target:Tcaplus.FieldGetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-idl-type:protobuf"
]
```

##### JSON response data

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

### Tcaplus.FieldSetRecord  

```
PUT /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```


This API is used to modify a record by specifying its `key` information. Different from the `SetRecord` operation, it transfers and sets the values of only the specified fields instead of all fields, which reduces the network traffic usage. If the data record already exists, an update operation will be performed; otherwise, an error will be returned.

The `FieldSetRecord` operation supports setting the following values for `resultflag`:

* `0`: the response only contains whether the request succeeded or failed
* `1`: the response contains the same values as the request does


| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Sample

##### URL

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records

```

##### HTTP request header

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
 "FieldPath": [ // Explicitly specify the path of the field to be updated
    "gamesvrid",
    "logintime",
    "pay.total_money",
    "pay.auth.pay_keys"
 ],
 "Record": { // Set the new value of the field to be updated
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

##### JSON response data

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


This API is used to auto-increment the specified fields by specifying the `key` information of a record. It supports fields in `int32`, `int64`, `uint32`, and `uint64` fields and has similar characteristics as `FieldSetRecord`.

The `SetRecord` operation supports setting the following values for `resultflag`:

* `0`: the response only contains whether the request succeeded or failed
* `1`: the response contains the modified value of the specified field


| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### Sample

##### URL

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### HTTP request header

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

##### JSON response data

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


### Tcaplus.PartkeyGetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```

This API is used to query multiple records by specifying the values of certain primary keys. This operation will return multiple data entries and display them by the field name specified by the `select` variable. The premise of this operation is that the specified primary key set must have an index created when the table is created; otherwise, an error will be returned.

The `keys` variable must be specified in the URI, which specifies the values of all primary keys. The optional `select` variable specifies the name of the field whose value you want to display. You can specify the fields in the nested structure by separating the path with a dot, such as `pay.total_money`.

`limit` and `offset` are the parameters used to control partial record return.

>! The variables in the request must be URL-encoded. Please encode the space in the URL as `%20` instead of `+`. Please specify the index name to be accessed through `x-tcaplus-index-name` in the HEADER. The index name can be found in the table definition file.

| Name | Type | Value |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.GetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |
|x-tcaplus-index-name  |String| {index_name}|


#### Sample

##### If URL is not URL-encoded

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'name': 'calvinshao', 'uin': 100}&select=['gamesvrid', 'lockid', 'pay.total_money', 'pay.auth.pay_keys']
```

##### If URL is URL-encoded
```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D&select=%5B%22gamesvrid%22%2C%20%22lockid%22%2C%20%22pay.total_money%22%2C%20%22pay.auth.pay_keys%22%5D
```

##### HTTP request header
```
[
"x-tcaplus-target:Tcaplus.PartkeyGetRecord",
"x-tcaplus-version:Tcaplus3.32.0",
"x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
"x-tcaplus-idl-type:protobuf"
"x-tcaplus-index-name:index_name"
]
```



##### Response data

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
