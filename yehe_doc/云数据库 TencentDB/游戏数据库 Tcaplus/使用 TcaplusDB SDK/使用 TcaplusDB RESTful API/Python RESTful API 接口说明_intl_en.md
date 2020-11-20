This SDK is encapsulated for Python based on RESTful APIs and used to perform CRUD operations on TcaplusDB PB tables.

## Preparations
### 1. Create a TcaplusDB table
Create a sample TcaplusDB table [`game_players.proto`](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto). For more information, please see [Creating Table](https://intl.cloud.tencent.com/document/product/1016/32715).

### 2. Create a CVM instance
- Create a CVM instance to run the SDK demo. We recommend the following configuration: 2 CPU cores, 4 GB memory, and 50 GB disk space. The CVM instance needs to be in the same VPC as that of the TcaplusDB instance.
- Download the installation package of the RESTful API SDK for Python [here](https://intl.cloud.tencent.com/document/product/1016/30285).


## Directions
1. Specify the `endpoint`, `access_id`, and `access_passwd` parameters to create `client`, which is a `TcaplusRestClient` object.
2. Use the `SetTargetTable` method of the `client` object to specify the table to be accessed.
3. Call an API function to send a data access request.
```
# Create a `TcaplusRestClient` object
#endpoint: restful API, such as http://x.x.x.x:80
client = TcaplusRestClient(endpoint, access_id, access_passwd) 
# Use `SetTargetTable` to specify the table to be accessed
client.SetTargetTable(table_group_id=1, table_name='game_players') 
# Send a data access request. The following uses `AddRecord` as an example:
record = {'player_id': 10805514, 'player_name': 'Calvin', 'player_email': 'calvin@test.com', 'game_server_id': 10,
   					'login_timestamp': ['2019-12-12 15:00:00'], 'logout_timestamp': ['2019-12-12 16:00:00'], 'is_online': False, 'pay': {'pay_id': 10101, 'amount': 1000, 'method': 1}}
   	status, resp = client.AddRecord(record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```
4. After using the `SetTargetTable` method to specify the target table, you can use the `GetTargetTable` method to get it.
```
table_group_id, table_name = client.GetTargetTable()
```
You can also use the `table_group_id` and `table_name` parameters of the API to directly specify the target table. This method will not change the target table set in the `SetTargetTable` function.
```
status, resp = client.AddRecord(record, custom_headers=None, return_values=None, table_group_id=1, table_name='game_players')
```

## API List
### GetRecord
This API is used to query a table record based on a primary key field. One record will be returned at a time.
```
@param keys   Dictionary of primary key fields for querying target record, which is required
@param select_fields   Array of non-primary key field names to be returned, which is optional. You can use a dotted path to specify nested fields
@param custom_headers   HTTP header to be specified, which is optional
@param table_group_id   ID of the cluster table group where the table resides, which is optional
@param table_name   `table_name` of target table, which is optional

def GetRecord(self, keys, select_fields=[], custom_headers=None, table_group_id=None, table_name=None)
```

### AddRecord
This API is used to insert a record into a table. If the record already exists, an error will be reported.
```
@param record   JSON object of the target record to be inserted, which is required
@param custom_headers   HTTP header to be specified, which is optional
@param table_group_id   ID of the cluster table group where the table resides, which is optional
@param table_name   `table_name` of target table, which is optional

def AddRecord(self, record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```

### SetRecord
This API is used to update or insert a record based on the primary key. If the record already exists, its value will be updated; otherwise, it will be inserted.
```
@param record   JSON object of the target record to be set, which is required. This operation involves insertion and modification semantics
@param custom_headers   HTTP header to be specified, which is optional
@param table_group_id   ID of the cluster table group where the table resides, which is optional
@param table_name   `table_name` of target table, which is optional

def SetRecord(self, record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```

### DeleteRecord
This API is used to delete a record based on the primary key.
```
@param record   JSON object of the target record to be deleted, which is required. You only need to set a primary key field
@param custom_headers   HTTP header to be specified, which is optional
@param table_group_id   ID of the cluster table group where the table resides, which is optional
@param table_name   `table_name` of target table, which is optional

def DeleteRecord(self, record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```

### FieldGetRecord
This API is used to get the values of specified fields based on the primary key. You need to specify the list of the fields to be returned (which must be non-primary key fields). You can use a dotted value to represent nested fields, i.e., `pay.amount`.
```
@param keys   Dictionary of primary key fields for querying target record, which is required
@param select_fields   Array of non-primary key field names to be returned, which is required. You can use a dotted path to specify nested fields
@param custom_headers   HTTP header to be specified, which is optional
@param table_group_id   ID of the cluster table group where the table resides, which is optional
@param table_name   `table_name` of target table, which is optional

def FieldGetRecord(self, keys, select_fields, custom_headers=None, table_group_id=None, table_name=None)
```

### FieldSetRecord
This API is used to update the values of specified fields based on the primary key. You need to specify the list of the fields to be updated (which must be non-primary key fields). You can use a dotted value to represent nested fields, i.e., `pay.amount`.
```
@param record   JSON object of the target record to be set, which is required. This operation involves insertion and modification semantics
@param field_path   Array of field names (paths) to be set, which is required. You can use a dotted path to specify nested fields
@param custom_headers   HTTP header to be specified, which is optional
@param table_group_id   ID of the cluster table group where the table resides, which is optional
@param table_name   `table_name` of target table, which is optional

def FieldSetRecord(self, record, field_path, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```

### FieldIncRecord
This API is used to update (auto-increment/decrement) the value of a specified numeric field based on the primary key. For example, if the original value of `pay.method` is 200, the requested value is 50, then the final value will be 250; if the requested value is -50, then the final value will be 150.
>!To auto-decrement, the type of the target field passed into the request must be a signed numeric, such as `int32` or `int64`.

```
@param record   Record to be auto-incremented/decremented, which is required. It must contain the primary key, and the target record must be in integer type
@param custom_headers   HTTP header to be specified, which is optional
@param table_group_id   ID of the cluster table group where the table resides, which is optional
@param table_name   `table_name` of target table, which is optional

def FieldIncRecord(self, record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```

### PartkeyGetRecord
This API is used to query data based on the index defined in the table and return one or multiple records matching the index keys. It can return the list of specified fields and allow you to specify `limit` and `offset` to control the size of the packet returned by each request.
```
@param index_keys   Dictionary of index keys for querying target record, which is required
@param index_name   Name of the index for query, which is required
@param select_fields   Array of non-primary key field names to be returned, which is optional. You can use a dotted path to specify nested fields
@param custom_headers   HTTP header to be specified, which is optional
@param table_group_id   ID of the cluster table group where the table resides, which is optional
@param table_name   `table_name` of target table, which is optional
@param limit   Maximum number of records to be returned, which is optional
@param offset   Initial offset of the number of records to be returned, which is optional

def PartkeyGetRecord(self, index_keys, index_name, select_fields=[], custom_headers=None, table_group_id=None, table_name=None, limit=None, offset=None)
```

For this API, the maximum size of a packet returned by one request is `256 KB`, and the `limit` value is subject to the size of one single record. We recommend you set it as follows:
- If the size of one single record is smaller than 256 KB, you can set `limit` to 256 KB / **record size**; for example, if the record size is 10 KB, we recommend you set `limit` to a value between 20 and 25.
- If the size of one single record is greater than or equal to 256 KB, set `limit` to 1, i.e., only one record will be returned by one request.

The following are the response packets returned with and without `limit` and `offset` parameters set, respectively:

```
# Index key settings
{'player_id': 39775502, 'player_name': 'Sara'}

# The response packet will be as follows if `limit` and `offset` are not set in the request:
{u'ErrorCode': 0, u'ErrorMsg': u'Succeed', u'MultiRecords': [{u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:00:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:00:00'], u'pay': {u'amount': 100, u'pay_id': 1, u'method': 1}, u'game_server_id': 1, u'player_email': u'sara@test.com', u'is_online': True, u'player_id': 39775502}}, {u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:10:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:10:00'], u'pay': {u'amount': 200, u'pay_id': 2}, u'game_server_id': 2, u'player_email': u'sara@163.com', u'is_online': True, u'player_id': 39775502}}, {u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:20:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:20:00'], u'pay': {u'amount': 300, u'pay_id': 3, u'method': 1}, u'game_server_id': 3, u'player_email': u'sara@gmail.com', u'is_online': True, u'player_id': 39775502}}], u'RemainNum': 0, u'TotalNum': 3}

# The response packet will be as follows if `limit` and `offset` are set in the request and `limit` is set to 2:
{u'ErrorCode': 0, u'ErrorMsg': u'Succeed', u'MultiRecords': [{u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:00:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:00:00'], u'pay': {u'amount': 100, u'pay_id': 1, u'method': 1}, u'game_server_id': 1, u'player_email': u'sara@test.com', u'is_online': True, u'player_id': 39775502}}, {u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:10:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:10:00'], u'pay': {u'amount': 200, u'pay_id': 2}, u'game_server_id': 2, u'player_email': u'sara@163.com', u'is_online': True, u'player_id': 39775502}}], u'RemainNum': 1, u'TotalNum': 3}
```
As shown above, if `limit` and `offset` are set, the number of entries in the returned result will be the same as that set in `limit`.
To get the full index data, you can judge whether the obtained data is complete based on the `RemainNum` and `TotalNum` flags returned in the response packet.



