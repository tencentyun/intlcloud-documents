
To help you use Java to manipulate TcaplusDB tables, we encapsulated the SDK for Java based on RESTful APIs. This document describes how to use RESTful APIs for Java to manipulate TcaplusDB PB tables (based on the protobuf protocol).

## Preparations
### 1. Create a TcaplusDB table
Create a sample TcaplusDB table [`game_players.proto`](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto). For more information, please see [Creating Table](https://intl.cloud.tencent.com/document/product/1016/32715).

### 2. Create a CVM instance
- Create a CVM instance to run the SDK demo. We recommend the following configuration: 1 CPU core, 2 GB memory, and CentOS 7. The CVM instance needs to be in the same VPC as that of the TcaplusDB instance.
- Download the installation package of the RESTful API SDK for Java [here](https://intl.cloud.tencent.com/document/product/1016/30285).

### 3. Prepare the Java environment
The SDK is dependent on Java 1.8 or above. If the OS of the CVM instance is CentOS 7 or above, you can simply run `yum install -y java`.

### 4. API description
Currently, the SDK supports eight APIs, which are as detailed below:

| API Name | Description |
| ---------------- | ------------------------------------------------------------ |
| addRecord | Adds TcaplusDB record, which must contain the values of all primary key fields |
| getRecord | Queries TcaplusDB record. A primary key field must be specified |
| setRecord | Updates TcaplusDB record. A primary key field must be specified for the update. If the record does not exist, a new one will be inserted |
| deleteRecord | Deletes TcaplusDB record. A primary key field must be specified |
| fieldSetRecord | Updates specified field. A primary key field must be specified |
| fieldGetRecord | Gets specified field. A primary key field must be specified |
| fieldIncRecord | Updates specified field, which can be used only to auto-increment/decrement numeric fields. A primary key field must be specified |
| partkeyGetRecord | Gets one or more TcaplusDB records based on specified index name and corresponding index field value. The corresponding index field value must be specified |


## Directions
Upload the entire SDK package `tcaplusdb-restapi-java-sdk-1.0-assembly.zip` to the CVM instance directory. For more information, please see [Copying Local File to CVM](https://intl.cloud.tencent.com/document/product/213/34821). After decompression, the directory name will be `tcaplusdb-restapi-java-sdk-1.0`.

### 1. Prepare configuration
The configuration file is in `tcaplusdb-restapi-java-sdk-1.0/conf/config.properties`, and its content is as follows:
```
#replace with your table endpoint
endpoint=http://10.xx.xx.16

#replace with your table access id
access_id=60

#replace with your table access password
access_password=Tcaxxx19

#replace with your table group id
table_group_id=1

#replace with your table name
table_name=game_players

#optional, configure the returning fields for GetRecord API, multiple fields with comma delimeter
get_select_fields=

#required, configure the returing fields for FieldGetRecord API
field_get_select_fields=game_server_id,is_online

#optional, configure the returning fields for PartkeyGetRecord API
part_key_get_select_fields=game_server_id,is_online

#required, configure the updating fields for FieldSetRecord API
field_set_fields=game_server_id,pay.amount

#required, configure the index keys for PartkeyGetRecord API
part_key_index_keys=player_id,player_name

#required, configure the index name for PartkeyGetRecord API
part_key_index_name=index_1

#optional, configure the limit number of records per request to return for PartkeyGetRecord API, value range: >0
part_key_limit = 10

#optional, configure the offset position to return for PartkeyGetRecord API, value range: >=0
part_key_offset = 0
```

### 2. Prepare data
The demo provides separately prepared testing data for each RESTful API, which is stored in the `tcaplusdb-restapi-java-sdk-1.0/conf` directory as JSON files.

| Filename | File Description |
| --------------------- | ------------------------------------------------------------ |
| add_data.json | Data for `addRecord` API, which is used to add a record |
| set_data.json | Data for `updateRecord` API, which is used to update a record value |
| delete_data.json | Data for `deleteRecord` API, which is used to delete the primary key value of a record |
| get_data.json | Data for `getRecord` API, which is used to get the primary key value of a record |
| field_get_data.json | Data for `fieldGetRecord` API, which is used to get the values of specified fields |
| field_set_data.json | Data for `fieldSetRecord` API, which is used to update the values of specified fields |
| field_inc_data.json | Data for `fieldIncRecord` API, which is used to increase the values of specified numeric fields |
| partkey_get_data.json | Data for `partkeyGetRecord` API, which is used to get a record value based on the index |

### 3. Execute the script
The main execution scripts are in `tcaplusdb-restapi-java-sdk-1.0/bin/run.sh` and can be run as follows:
```
# Add a record
sh bin/run.sh add
# Get a record
sh bin/run.sh get
# Update a record
sh bin/run.sh set
# Delete a record
sh bin/run.sh delete
# Update specified fields
sh bin/run.sh field_set
# Get specified fields
sh bin/run.sh field_get
# Update the values of specified fields (in numeric type)
sh bin/run.sh field_inc
# Get a record based on the index
sh bin/run.sh partkey_get

```

## API Data Description
### addRecord
This API is used to add a record. The inserted data is in JSON format as shown below:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com", "game_server_id":2,"login_timestamp":[],"logout_timestamp":[],"is_online":true,"pay":{"pay_id":1,"amount":20,"method":3}}
```

### getRecord
This API is used to query a record by specifying the primary key field. The data is in JSON format as shown below:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com"}
```
The query API also allows you to specify the list of fields to be returned. The `get_select_fields` configuration item defined in the `config.properties` configuration file is used to specify the names of the fields to be returned. If it is left empty, all fields of the record will be returned by default; otherwise, the values of the specified fields will be returned.

### setRecord
This API is used to update a record, and the record to be updated must contain a primary key field. The data is in JSON format as shown below:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com", "game_server_id":2,"login_timestamp":[],"logout_timestamp":[],"is_online":false,"pay":{"pay_id":1,"amount":30,"method":3}}
```

### deleteRecord
This API is used to delete a record. The entered data must contain a primary key field. The data is in JSON format as shown below:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com"}
```

### fieldSetRecord
This API is used to update the values of specified fields. The entered data must contain a primary key field. The data is in JSON format as shown below:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com", "game_server_id":3,"is_online":false, "login_timestamp":[],"logout_timestamp":[],"pay":{"pay_id":1,"amount":40,"method":3}}
```
At the same time, you need to specify the names of the fields to be updated in the `field_set_fields` configuration item defined in the `config.properties` configuration file. Multiple fields should be separated with commas, and the value **cannot be empty**.

### fieldGetRecord
This API is used to get the values of specified fields. The entered data must contain a primary key field. The data is in JSON format as shown below:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com"}
```
At the same time, you need to specify the names of the fields to be obtained in the `field_get_select_fields` configuration item defined in the `config.properties` configuration file, and the value **cannot be empty**.

### fieldIncRecord
This API is used to update the values of specified fields. Different from the `fieldSetRecord` API, it can update field values only in numeric type, such as increasing or decreasing a value. The entered data must contain a primary key field and the numeric fields to be updated. The data is in JSON format as shown below:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com", "pay":{"amount":50}}
```
Suppose the initial value of `pay.amount` is 100, and the value of the input parameter in the request is 50, then the final value will be 150.

### partkeyGetRecord
This API is used to get the corresponding record based on the specified index. Multiple records may be matched, and you can specify the fields to be returned. The entered data must contain an index field. The data is in JSON format as shown below:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com"}
```
At the same time, you need to specify the corresponding index name and index field names in the `part_key_index_name` and `part_key_index_keys` configuration items defined in the `config.properties` configuration file, respectively. **The two configuration items cannot be empty.**

To return specified fields, you can configure `part_key_get_select_fields` in the configuration file; otherwise, leave it empty.

For this API, the maximum size of a packet returned by one request is `256 KB`, and the `limit` value is subject to the size of one single record. We recommend you set it as follows:

- If the size of one single record is smaller than 256 KB, you can set `limit` to 256 KB / **record size**; for example, if the record size is 10 KB, we recommend you set `limit` to a value between 20 and 25.
- If the size of one single record is greater than or equal to 256 KB, set `limit` to 1, i.e., only one record will be returned by one request.

In scenarios where `limit` and `offset` are set, to get the full data based on the index key, you need to judge whether the obtained data is complete based on the `TotalNum` and `RemainNum` flags returned in the response packet.

You can set `limit` and `offset` in the following steps:
```
# Step 1. Prepare batch demo data and set the values of `limit` and `offset` as instructed in `conf/batch_add_data.json`.
part_key_limit = 2
part_key_offset = 0

# Step 2. Add demo data in batches. Run the `batch_add` command to add three records.
sh bin/run.sh batch_add

# Step 3. Call the `partkey_get` command, and `partkeyGetRecord` will be executed twice: in the first execution, `limit` and `offset` are not set; in the second execution, `limit` and `offset` are set. Check the differences between the two execution results.
sh bin/run.sh partkey_get

# Step 4. The response data with `limit` and `offset` not set is as follows, which contains four data entries in total:
{"MultiRecords":[{"RecordVersion":3,"Record":{"game_server_id":3,"is_online":true,"player_email":"test@email.com","player_id":1,"player_name":"test"}},{"RecordVersion":1,"Record":{"game_server_id":3,"is_online":true,"player_email":"test1@email.com","player_id":1,"player_name":"test"}},{"RecordVersion":1,"Record":{"game_server_id":4,"is_online":true,"player_email":"test2@email.com","player_id":1,"player_name":"test"}},{"RecordVersion":1,"Record":{"game_server_id":5,"is_online":true,"player_email":"test3@email.com","player_id":1,"player_name":"test"}}],"TotalNum":4,"RemainNum":0,"ErrorCode":0,"ErrorMsg":"Succeed"}

# Step 5. The response data with `limit` and `offset` set is as follows, which contains only two data entries subject to the `limit` value:
{"MultiRecords":[{"RecordVersion":3,"Record":{"game_server_id":3,"is_online":true,"player_email":"test@email.com","player_id":1,"player_name":"test"}},{"RecordVersion":1,"Record":{"game_server_id":3,"is_online":true,"player_email":"test1@email.com","player_id":1,"player_name":"test"}}],"TotalNum":4,"RemainNum":2,"ErrorCode":0,"ErrorMsg":"Succeed"}

```

