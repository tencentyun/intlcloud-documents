## Preparations
### 1. Create a TcaplusDB table
Create a sample TcaplusDB table [`game_players.proto`](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto). For more information, please see [Creating Table](https://intl.cloud.tencent.com/document/product/1016/32715).

### 2. Create a CVM instance
- Create a CVM instance to run the SDK demo. We recommend the following configuration: 1 CPU core, 2 GB memory, and CentOS 7. The CVM instance needs to be in the same VPC as that of the TcaplusDB instance.
- Download the installation package of the RESTful API SDK for PHP [here](https://intl.cloud.tencent.com/document/product/1016/30285).

### 3. Prepare the PHP environment
PHP is not installed on the new instance. You need to run `yum install php` to install it on the default version (PHP 5.4.16). The PHP version must be above 5.3.

## Directions
### 1. Configuration modification
All basic configuration items are in `config.php` in the SDK installation directory, and you need to modify them based on the information of the table applied for.
- Connection configuration: modify parameters such as `url`, `endpoint`, `table_group_id`, `access_id`, and `access_passwd` to the corresponding values. For more information on how to get the connection information, please see [Getting Access Point Information](https://intl.cloud.tencent.com/zh/document/product/1016/30276).
- Default data source: all variables in this section are in uppercase. It can be used as the data source of specific API functions in [demo.php](#dsyff), so the source information can be modified here in a unified manner.

### 2. Call method
To facilitate the feature testing of individual APIs, all SDK API functions are built as separate programs in TcaplusDB, which correspond to the eight API functions in the demo, and their data sources are managed separately from the program code.
The data sources of all API functions are from two places: default data sources are uniformly stored in `config.php`, and the own data sources of each API function are stored in the `data` subdirectory. You can modify a data file to run the corresponding API function, which helps eliminate your need to define data sources in the program code during batch operations. If the data file does not exist, the default data source will be loaded, where all data is organized in the form of list and can be loaded in batches.
Program files in `sample` can be executed by running a command similar to the one below:
```
php -f <Specific API function file>
```

### 3. API functions
All APIs are encapsulated as functions in `demo.php`. There are eight API functions in total, all of which can load the data source from the configuration for batch operations. The specific functions are as detailed below:

| API Function Name | Feature |
| ---------------- | ----------------------------------------------- |
| GetRecord | Gets table record |
| AddRecord | Inserts table record |
| SetRecord | Updates table record |
| DeleteRecord | Deletes record |
| FieldGetRecord | Gets an attribute field of specified record |
| FieldSetRecord | Updates an attribute field value of specified record |
| FieldIncRecord | Updates the numeric value of an attribute field of specified record, such as increasing/decreasing a value in numeric type |
| PartKeyGetRecord | Gets an attribute field value of specified record based on specified index |


## SDK API List
### add
This API is used to insert a record into a table. If the record already exists, an error will be reported.
```
@param $table_group_id   `table_group_id` of target table, which is required
@param $table_name   `table_name` of target table, which is required
@param $record   Array of target records to be inserted, which is required
@param $ReturnValues   Custom value to be returned, which is optional
@param $resultflag   Content to be returned in response packet, which is optional. Valid values:
            0: the response only contains whether the request succeeded or failed
            1: the response contains the same values as the request does
            2: the response contains the latest values of all fields of the data that has been modified
            3: the response contains the value before the record is modified

public function add($table_group_id, $table_name, array $record, $ReturnValues = 'TcaplusDB', $resultflag = 1)
```

### get
This API is used to query a record based on the primary key. It allows you to specify the list of attributes fields to be returned as detailed in `$params["select"]`.
 ```
@param $table_group_id   Game region ID, which is required
@param $table_name   Table name, which is required
@param $params   Required
    $params\["select"\]   Array of the fields to be queried, which is optional
    $params \["keys"\]   Primary key field for querying target record, which is required
    $params \["limit"\]   Limit on the number of records to be returned, which is optional
    $params \["offset"\]   Offset of the number of records to be returned, which is optional
		
public function get($table_group_id, $table_name, $params)
 ```

### fieldGet
This API is used to query and return the value of a specified field based on the primary key. You can specify the list of fields as detailed in `$param["select"]`, which cannot be empty.
```
@param $table_group_id   Game region ID, which is required
@param $table_name   Table name, which is required
@param  $params   Required
    $params\["select"\]   Array of the fields to be queried, which is required
    $params\["keys"\]   Primary key field for querying target record, which is required
    $params\["limit"\]   Limit on the number of records to be returned, which is optional
    $params\["offset"\]   Offset of the number of records to be returned, which is optional

public function fieldGet($table_group_id, $table_name, $params)
```

### partKeyGet
This API is used to query and return one or multiple records based on the index defined in the table. It can return the list of specified fields and allow you to use the `limit` and `offset` parameters to control the number of records in the returned packet.
```
@param $table_group_id   Game region ID, which is required
@param $table_name   Table name, which is required
@param  $params   Required
    $params\["select"\]   Array of the fields to be queried, which is optional
    $params\["index"\]    Name of the index for query, which is required
    $params\["keys"\]   Primary key field for querying target record, which is required
    $params\["limit"\]   Limit on the number of records to be returned, which is optional. Default value: -1
    $params\["offset"\]   Offset of the number of records to be returned, which is optional

public function partKeyGet($table_group_id, $table_name, $params)
```

For the `partkeyGet` API, the maximum size of a packet returned by one request is `256 KB`, and the `limit` value is subject to the size of one single record. We recommend you set it as follows:
- If the size of one single record is smaller than 256 KB, you can set `limit` to 256 KB / **record size**; for example, if the record size is 10 KB, we recommend you set `limit` to a value between 20 and 25.
- If the size of one single record is greater than or equal to 256 KB, set `limit` to 1, i.e., only one record will be returned by one request.

The following are sample responses for different `limit` and `offset` settings:
```
# If `limit=-1, offset=0` is set in the request
{"MultiRecords":[{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@test.com","player_id":1,"player_name":"kosh"}},{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@163.com","player_id":1,"player_name":"kosh"}},{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@gmail.com","player_id":1,"player_name":"kosh"}},{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@126.com","player_id":1,"player_name":"kosh"}}],"TotalNum":4,"RemainNum":0,"ErrorCode":0,"ErrorMsg":"Succeed"}

# If `limit=2, offset=0` is set in the request
{"MultiRecords":[{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@test.com","player_id":1,"player_name":"kosh"}},{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@163.com","player_id":1,"player_name":"kosh"}}],"TotalNum":4,"RemainNum":2,"ErrorCode":0,"ErrorMsg":"Succeed"}
```
As shown above, if `limit` and `offset` are set, the number of entries in the returned result will be the same as that set in `limit`.
To get the full index data, you can judge whether the obtained data is complete based on the `RemainNum` and `TotalNum` flags returned in the response packet.

### set
This API is used to update or insert a record. If the record already exists, it will be updated; otherwise, it will be inserted.
```
@param $table_group_id   Game region ID, which is required
@param $table_name   Table name, which is required
@param $record   Target record to be set, which is required. This operation involves insertion and modification semantics
@param $ReturnValues   Check string, which is optional. The server will return the same string
@param $resultflag   Content mode in response package, which is optional. Default value: 1. Valid values:
            0: the response only contains whether the request succeeded or failed
            1: the response contains the same values as the request does
            2: the response contains the latest values of all fields of the data that has been modified
            3: the response contains the value before the record is modified

public function set($table_group_id, $table_name, array $record, $ReturnValues = 'TcaplusDB', $resultflag = 1)
```

### fieldSet
This API is used to update the value of a specified field based on the primary key. You can specify the field to be updated as detailed in `$field_path`.
```
@param $table_group_id   Game region ID, which is required
@param $table_name   Table name, which is required
@param $record   Target record to be set, which is required. This operation involves insertion and modification semantics
@param $field_path   Array of field names (paths) to be set, which is required. You can use a dotted path to specify nested fields
@param $ReturnValues   Check string, which is optional. The server will return the same string
@param $resultflag   Content mode in response package, which is optional. Default value: 1. Valid values:
            0: the response only contains whether the request succeeded or failed
            1: the response contains the same values as the request does
            2: the response contains the latest values of all fields of the data that has been modified
            3: the response contains the value before the record is modified

public function fieldSet($table_group_id, $table_name, array $record, $field_path, $ReturnValues = 'TcaplusDB', $resultflag = 1)

```

### fieldInc
This API is used to update (auto-increment/decrement) the value of a specified numeric field based on the primary key. For example, if the original value of `pay.method` is 200, the requested value is 50, then the final value will be 250; if the requested value is -50, then the final value will be 150.
>!Auto-decrement only takes effect for signed type such as `int32` and `int64`.
>
```
@param $table_group_id   Game region ID, which is required
@param $table_name   Table name, which is required
@param $record   Record to be auto-incremented/decremented, which is required. It must contain the primary key, and the target record must be in integer type
@param $ReturnValues   Check string, which is optional. The server will return the same string
@param $resultflag   Content mode in response package, which is optional. Default value: 1. Valid values:
            0: the response only contains whether the request succeeded or failed
            1: the response contains the same values as the request does
            2: the response contains the latest values of all fields of the data that has been modified
            3: the response contains the value before the record is modified
@param $dataVersion   Version number, which is optional
@param $dataVersionCheck   Data version check policy, which is optional. Valid values:
    1: data will be written only if the version numbers are the same
    2: the version number will not be checked. The client version number will be forcibly set at the storage layer.
    3: the version number will not be checked. The version number at the storage layer will be increased by 1 each time the write operation is performed. This is the default value

public function fieldInc($table_group_id, $table_name, array $record, $ReturnValues = 'TcaplusDB', $resultflag = 2, $dataVersion = -1, $dataVersionCheck = 3)

```

### delete
This API is used to delete a record of a specified primary key.
```
@param $table_group_id   Game region ID, which is required
@param $table_name   Table name, which is required
@param $record   Array of target records to be deleted, which is required. You only need to set a primary key field
@param  $ReturnValues   Check string, which is optional. The server will return the same string
@param $resultflag   Content mode in response package, which is optional. Default value: 1. Valid values:
            0: the response only contains whether the request succeeded or failed
            1: the response contains the same values as the request does
            2: the response contains the latest values of all fields of the data that has been modified
            3: the response contains the value before the record is modified

public function delete($table_group_id, $table_name, array $record, $ReturnValues = 'TcaplusDB', $resultflag = 1)
```


<span id = "dsyff"></span>
## demo.php Usage
To help you quickly try out TcaplusDB SDK features, all APIs have been encapsulated as eight functions in `demo.php`. You can run the corresponding function as needed and comment out unneeded ones by running the following command:
```
php -f  "demo.php"
```

