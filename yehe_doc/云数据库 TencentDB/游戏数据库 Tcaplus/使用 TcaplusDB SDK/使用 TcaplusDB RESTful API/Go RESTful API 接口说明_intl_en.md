To help you use Go to manipulate TcaplusDB tables, we encapsulated TcaplusDB table operation APIs based on RESTful APIs, which support CRUD operations. This document describes how to use such APIs to manipulate TcaplusDB PB tables.

## Preparations
### 1. Create a TcaplusDB table
Create a sample TcaplusDB table [`game_players.proto`](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto). For more information, please see [Creating Table](https://intl.cloud.tencent.com/document/product/1016/32715).

### 2. Create a CVM instance
- Create a CVM instance to run the SDK demo. We recommend the following configuration: 2 CPU cores, 4 GB memory, and 50 GB disk space. The CVM instance needs to be in the same VPC as that of the TcaplusDB instance.
- Download the installation package of the RESTful API SDK for Go [here](https://intl.cloud.tencent.com/document/product/1016/30285).

### 3. Prepare the Go environment
Run the following command to install the Go environment:
```
yum install -y golang
```

### 4. Compile the program
The SDK demo is complied by using the `make` command. you can directly run `make build` in the `Makefile` file in the `src` directory. After the compilation, an executable file `example` will be generated. You can try out all sample APIs by directly running the file.

## Directions
### 1. Configure table parameters
View the relevant information of the table created in the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/app) and configure the demo as follows:
```
// TcaplusDB RESTful API connection parameters
const (
        // Service access point, which is also the RESTful API connection address of the cluster where the table resides. The default port is 80
        EndPoint = "http://172.xx.xx.12/"
        // Application access ID, which is also the access ID of the cluster where the table resides
        AccessID = 310
        // Application password, which is also the access password of the cluster where the table resides
        AccessPassword = "Tcaplus2020"
        // Table group ID
        TableGroupID = 1
        // Table name
        TableName = "game_players"
)
```

### 2. Create a table connection
Use `NewTcaplusClient` to specify the `EndPoint`, `AccessID`, and `AccessPassword` parameters to create `client`, which is a `TcaplusRestClient` object.
```
// Specify the `EndPoint`, `AccessID`, and `AccessPassword` parameters to create `client`, which is a `TcaplusClient` object
client, err := tcaplus_client.NewTcaplusClient(EndPoint, AccessID, AccessPassword)
if err != nil {
    fmt.Println(err.Error())
    return
}
```

### 3. Prepare sample table data
Insert data in JSON format. The definition is as follows:
```
// Call `AddRecord` to insert a record
// You can define `record` as a structure, map, or slice, which must be convertible to JSON format
record := map[string]interface{}{
    "player_id": 10805514,
    "player_name": "Calvin",
    "player_email": "calvin@test.com",
    "game_server_id": 10,
    "login_timestamp": []string{"2019-12-12 15:00:00"},
    "logout_timestamp": []string{"2019-12-12 16:00:00"},
    "is_online": false,
    "pay": map[string]interface{}{
        "pay_id": 10101,
        "amount": 1000,
        "method": 1,
    },
}
status, resp, err := client.AddRecord(record, tcaplus_client.RetAllLatestField, "userBuffer", TableGroupID, TableName)
if err != nil {
    fmt.Println(err.Error())
    return
}
```

## API List
### GetRecord
```
/**
	@brief   This API is used to query a record based on the `Key` field. You can filter fields by `selectFiled`
	@param [IN] key   `key` field information of the record to be queried. It can be a structure, map, or slice, so that it can be converted to JSON. It needs to be in the same type as that defined in `proto`
	@param [IN] selectFiled   List of fields in the record to be queried. If you want to enter a nested structure, use a dotted value. `nil` indicates that all fields will be queried
	@param [IN] groupID   Table group ID
	@param [IN] tableName   Table name
	@retval(3)   HTTP response code, HTTP response content, and error message
**/
func (c *TcaplusClient) GetRecord(key interface{}, selectFiled []string, groupID int, tableName string) (string, []byte, error)
```

### AddRecord
```
/**
	@brief   This API is used to add a record to the table. If the record already exists, an error will be reported
	@param [IN] record   Record to be added, which can be a structure, map, or slice, so that it can be converted to JSON. It needs to be in the same type as that defined in `proto`
	@param [IN] resultFlag   Position flag of the returned value. Valid values:
                                        RetOnlySucOrFail: the response only contains whether the request succeeded or failed
                                        RetEqualReq: the response contains the same values as the request does
                                        RetAllLatestField: the response contains the latest values of all fields of the data that has been modified
                                        RetAllOldField: the response contains the value before the record is modified
	@param [IN] userBuffer   Custom information, which will be returned as-is in the response message. If you do not need it, enter ""
	@param [IN] groupID   Table group ID
	@param [IN] tableName   Table name
	@retval(3)   HTTP response code, HTTP response content, and error message
**/
func (c *TcaplusClient) AddRecord(record interface{}, resultFlag int, userBuffer string, groupID int, tableName string) (string, []byte, error)
 
```

### SetRecord
```
/**
	@brief   This API is used to update/insert a record in the table. If the record already exists, it will be updated; otherwise, it will be inserted
	@param [IN] record   Record to be added, which can be a structure, map, or slice, so that it can be converted to JSON. It needs to be in the same type as that defined in `proto`
	@param [IN] resultFlag   Position flag of the returned value. Valid values:
                                        RetOnlySucOrFail: the response only contains whether the request succeeded or failed
                                        RetEqualReq: the response contains the same values as the request does
                                        RetAllLatestField: the response contains the latest values of all fields of the data that has been modified
                                        RetAllOldField: the response contains the value before the record is modified
	@param [IN] versionPolicy   Policy for checking the record version number, which is to be used with `version` to implement optimistic locking. If you do not need it, set it to `NoCheckDataVersionAutoIncrease`
                                        CheckDataVersionAutoIncrease: the record version number will be checked. The operation will succeed, and the version number will auto-increment only if `version` is the same as the version number on the server
                                        NoCheckDataVersionOverwrite: the record version number will not be checked, and it (`version`) will be forcibly written to the server
                                        NoCheckDataVersionAutoIncrease: the record version number will not be checked, and the version number on the server will auto-increment
	@param [IN] version   Record version number, which is used for version number check. If you do not need the check, set it to `-1`
	@param [IN] userBuffer   Custom information, which will be returned as-is in the response message. If you do not need it, enter ""
	@param [IN] groupID   Table group ID
	@param [IN] tableName   Table name
	@retval(3)   HTTP response code, HTTP response content, and error message
**/
func (c *TcaplusClient) SetRecord(record interface{}, resultFlag int, versionPolicy int, version int, userBuffer string, groupID int, tableName string) (string, []byte, error) 

```

### DeleteRecord
```
/**
	@brief   This API is used to delete a record. If the record does not exist, an error will be reported.
	@param [IN] record   Record to be deleted, which only needs to contain the `key` field. It can be a structure, map, or slice, so that it can be converted to JSON. It needs to be in the same type as that defined in `proto`
	@param [IN] resultFlag   Position flag of the returned value. Valid values:
                                        RetOnlySucOrFail: the response only contains whether the request succeeded or failed
                                        RetEqualReq: the response contains the same values as the request does
                                        RetAllLatestField: the response contains the latest values of all fields of the data that has been modified
                                        RetAllOldField: the response contains the value before the record is modified
	@param [IN] userBuffer   Custom information, which will be returned as-is in the response message. If you do not need it, enter ""
	@param [IN] groupID   Table group ID
	@param [IN] tableName   Table name
	@retval(3)   HTTP response code, HTTP response content, and error message
**/
func (c *TcaplusClient) DeleteRecord(record interface{}, resultFlag int, userBuffer string, groupID int, tableName string) (string, []byte, error)

```

### FieldGetRecord

```
/**
	@brief   This API is used to query a record based on specified fields. The `key` field is used to query the record, and `selectFiled` is used to filter fields
	@note   The difference between this API and `GetRecord` lies in that `GetRecord` queries the entire record first and then filters the fields by `selectFiled`, while `FieldGetRecord` filters the fields on the server, which has a lower traffic load
	@param [IN] key   `key` field information of the record to be queried. It can be a structure, map, or slice, so that it can be converted to JSON. It needs to be in the same type as that defined in `proto`
	@param [IN] selectFiled   List of fields in the record to be queried, which cannot be empty. If you want to enter a nested structure, use a dotted value
	@param [IN] groupID   Table group ID
	@param [IN] tableName   Table name
	@retval(3)   HTTP response code, HTTP response content, and error message
**/
func (c *TcaplusClient) FieldGetRecord(key interface{}, selectFiled []string, groupID int, tableName string) (string, []byte, error)

```

### FieldSetRecord
```
/**
	@brief   This API is used to update a record. If the record does not exist, an error will be reported
	@param [IN] record   Record to be added, which can be a structure, map, or slice, so that it can be converted to JSON. It needs to be in the same type as that defined in `proto`
	@param [IN] setField   List of fields to be updated, which cannot be empty. If you want to enter a nested structure, use a dotted value
	@param [IN] resultFlag   Position flag of the returned value. Valid values:
                                        RetOnlySucOrFail: the response only contains whether the request succeeded or failed
                                        RetEqualReq: the response contains the same values as the request does
	@param [IN] versionPolicy   Policy for checking the record version number, which is to be used with `version` to implement optimistic locking. If you do not need it, set it to `NoCheckDataVersionAutoIncrease`
                                        CheckDataVersionAutoIncrease: the record version number will be checked. The operation will succeed, and the version number will auto-increment only if `version` is the same as the version number on the server
                                        NoCheckDataVersionOverwrite: the record version number will not be checked, and it (`version`) will be forcibly written to the server
                                        NoCheckDataVersionAutoIncrease: the record version number will not be checked, and the version number on the server will auto-increment
	@param [IN] version   Record version number, which is used for version number check. If you do not need the check, set it to `-1`
	@param [IN] userBuffer   Custom information, which will be returned as-is in the response message. If you do not need it, enter ""
	@param [IN] groupID   Table group ID
	@param [IN] tableName   Table name
	@retval(3)   HTTP response code, HTTP response content, and error message
**/
func (c *TcaplusClient) FieldSetRecord(record interface{}, setField []string, resultFlag int, versionPolicy int, version int, userBuffer string, groupID int, tableName string) (string, []byte, error)
 
```

### FieldIncRecord
```
/**
	@brief   This API is used to auto-increment/decrement an integer field in a record. This command word supports fields only in `int32`, `int64`, `uint32`, or `uint64` type
	@param [IN] record   Record to be updated. If the field value in the record is positive, it indicates auto-increment, and this field will be incremented; if the field value in the record is negative, it indicates auto-decrement, and this field will be decremented
	@param [IN] resultFlag   Position flag of the returned value. Valid values:
                                        RetOnlySucOrFail: the response only contains whether the request succeeded or failed
                                        RetEqualReq: the response contains the same values as the request does
	@param [IN] versionPolicy   Policy for checking the record version number, which is to be used with `version` to implement optimistic locking. If you do not need it, set it to `NoCheckDataVersionAutoIncrease`
                                        CheckDataVersionAutoIncrease: the record version number will be checked. The operation will succeed, and the version number will auto-increment only if `version` is the same as the version number on the server
                                        NoCheckDataVersionOverwrite: the record version number will not be checked, and it (`version`) will be forcibly written to the server
                                        NoCheckDataVersionAutoIncrease: the record version number will not be checked, and the version number on the server will auto-increment
	@param [IN] version   Record version number, which is used for version number check. If you do not need the check, set it to `-1`
	@param [IN] userBuffer   Custom information, which will be returned as-is in the response message. If you do not need it, enter ""
	@param [IN] groupID   Table group ID
	@param [IN] tableName   Table name
	@retval(3)   HTTP response code, HTTP response content, and error message
**/
func (c *TcaplusClient) FieldIncRecord(record interface{}, resultFlag int, versionPolicy int, version int, userBuffer string, groupID int, tableName string) (string, []byte, error)
 
```

### PartkeyGetRecord
```
/**
	@brief   This API is used to query records in batches with an index
	@param [IN] key   Record to be queried, which needs to be set to the `key` field in the index. It can be a structure, map, or slice, so that it can be converted to JSON. It needs to be in the same type as that defined in `proto`
	@param [IN] indexName   Index name
	@param [IN] selectFiled   List of fields in the record to be queried. If you want to enter a nested structure, use a dotted value. `nil` indicates that all fields will be queried
	@param [IN] limit   Maximum number of records to be returned in batches, which will be valid if the value is greater than 0
	@param [IN] offset   Offset of the records to be returned in batches, which will be valid if the value is greater than or equal to 0
	@param [IN] groupID   Table group ID
	@param [IN] tableName   Table name
	@retval(3)   HTTP response code, HTTP response content, and error message
**/
func (c *TcaplusClient) PartKeyGetRecord(key interface{}, indexName string, selectFiled []string, limit int, offset int, groupID int, tableName string) (string, []byte, error)
```

For the `PartKeyGetRecord` API, the maximum size of a packet returned by one request is `256 KB`, and the `limit` value is subject to the size of one single record. We recommend you set it as follows:
- If the size of one single record is smaller than 256 KB, you can set `limit` to 256 KB / **record size**; for example, if the record size is 10 KB, we recommend you set `limit` to a value between 20 and 25.
- If the size of one single record is greater than or equal to 256 KB, set `limit` to 1, i.e., only one record will be returned by one request.

In scenarios where `limit` and `offset` are set, to get the full data based on the index key, you need to judge whether the obtained data is complete based on the `TotalNum` and `RemainNum` flags returned in the response packet.

