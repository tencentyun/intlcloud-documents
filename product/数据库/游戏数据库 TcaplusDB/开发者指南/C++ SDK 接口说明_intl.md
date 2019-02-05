[//]: # (chinagitpath:XXXXX)

## Overview
TcaplusDB service APIs are used by apps to access TcaplusDB for data access and to store and acquire TcaplusDB App data for programming access. TcaplusDB mainly uses Google Protocol Buffer (Protobuf) as the communication and data element definition protocol.

## Process
After you activate the service and create a table in the console, you will see AppId, AppKey and private network access address on the configuration information page, as well as name of the created table and deployment unit ID (ZoneId) on the Protobuf table management page. The first three items are obtained after successful access to TcaplusDB, and the last two items are defined when the service creates a table structure on the TcaplusDB management page. With TcaplusDB service API, apps can operate multiple tables with an AppId.

## Module
You can define a table that meets TcaplusDB specifications with the Protobuf protocol and submit the metafile specific to the table to the TcaplusDB console to create a new table or modify an existing table. Then, you can read and write table data records through TcaplusDB Protobuf API. TcaplusDB Protobuf API supports the following operations:

| Operation | Description |
|---------|---------|
| GET | Get a Value based on a specific Key |
| BATCHGET | Get multiple Values based on multiple Keys |
| ADD | Add a data record. If a Key-related record already exists, an error will occur. |
| SET | If a Key-related record already exists, it will be updated. Otherwise, a new record will be added. |
| DEL| Delete a record based on a Key |
| FIELDINC | Add a value of a specified field (integer) |
| FIELDSET | Update (one or more) value(s) of a specific field |
| FIELDGET | Get (one or more) value(s) of a specific field |
| INDEXGET | Specify an index and field for query |
| TRAVERSE | Specify the table name for full table traversal |

## TcaplusDB SDK Conventions
TcaplusDB must define primarykey and other information for the table. The extension tcaplusservice.optionv1.proto is built in the TcaplusDB system. When customizing a table, you just need to import a custom table to create a new table or modify an existing table without uploading a new one. Details are shown below:
```
extend google.protobuf.MessageOptions
{
    optional string tcaplus_primary_key             = 60000; //Define the primary key of the table
    repeated string tcaplus_index                   = 60001; //Define the index of the table
    optional string tcaplus_field_cipher_suite      = 60002; //Define encryption algorithm for table fields
    optional string tcaplus_record_cipher_suite     = 60003; //Define encryption algorithm for table fields. Not available.
    optional string tcaplus_cipher_md5              = 60004; //It is used to return a cipher key message digest.
    optional string tcaplus_sharding_key            = 60005; //Tcaplus sharding key
}

extend google.protobuf.FieldOptions
{
    optional uint32 tcaplus_size                    = 60000; //Field size. Not available.
    optional string tcaplus_desc                    = 60001; //Field description
    optional bool tcaplus_crypto                    = 60002; //Indicates whether to encrypt the field. Encryption algorithm is defined by tcaplus_field_cipher_suite.
}
```
The complete file can be found in the directory release\x86_64\include\tcaplus_pb_api\tcaplusservice.optionv1.proto.
1. The table name must start with letters or underscores (_), and cannot exceed 31 characters. Special characters other than numbers, letters and underscores (_) are not supported.
2. The field names should contain letters or underscores (_), which are further restricted by protobuf.
3. A table can contain up to 4 primary key fields and the field type must be required. The length after packaging cannot exceed 1,022 bytes.
4. The packaged value size should not exceed 256 KB, and the complete packaged records should not exceed 256 KB.
5. Except for the key field, there is at least one value field. The upper limit of the value fields is specified by protobuf.
6. By default, the table type is generic. But the generic type is not displayed externally.
7. The key field can only be scalar value type specified by protobuf, and cannot contain any composite types, custom types, etc.

## Common API Description
```
 @brief Obtain multiple record values by indexes based on the index name, msg value, offset and limit in the entered req, fill them into the vec structure of res, and return the total and remaining number of records.
 @param [INOUT] req   The entered req
 @param [INOUT] res   The entered res
 @retval <0   Failed. The corresponding error code is returned.
 @retval 0    Succeeded.
```
**int Get(::google::protobuf::Message &msg);**
```
  @brief Get field values in msg in batches based on the entered key values in msgs, and fill them into msgs.
  @param [INOUT] msgs List of the entered key values, which will be returned to the specified field and filled into msgs.
  @retval <0   Failed. The corresponding error code is returned.
  @retval 0    Succeeded. 0 is returned when at least one field query is successful.
```
**int BatchGet(std::vector< ::google::protobuf::Message * > &msgs);**

```
 @brief Add a msg data record according to the entered key in msg. Exit with an error if the key already exists.
 @param [INOUT] msg   The entered key value and the data record msg to be added.
 @retval <0   Failed. The corresponding error code is returned.
 @retval 0    Succeeded.
```
**int Add(::google::protobuf::Message \*msg);**

```
 @brief Based on the entered key in msg, update the value of the specified record if the key already exists. Otherwise, add a specified record.
 @param [INOUT] msg   The entered key value and the data record msg to be set.
 @retval <0   Failed. The corresponding error code is returned.
 @retval 0    Succeeded.
```
**int Set(const ::google::protobuf::Message &msg);**

```
  @brief Delete msg based on the entered key value in msg.       
  @param [IN] msg The entered key value, which will be returned to the specified field and filled into msg.
  @retval <0   Failed. The corresponding error code is returned.
  @retval 0    Succeeded. 0 is returned when at least one field query is successful.
```
**int Del(const ::google::protobuf::Message &msg);**
```
 @brief Based on the entered key values and increment of values in msg, and the field name specified in dottedpaths, increase the value of the field specified in msg. The field should be a numeric variable.
 @param [INOUT] msg   Data record msg. It contains the entered key value. The returned result value of the incremental field is updated to msg.
 @param [IN] dottedpaths Dotted nested string sets of the field name
 @retval <0   Failed. The corresponding error code is returned. Indicates that no field is updated.
 @retval 0    Succeeded. Indicates all fields have been updated.
```
**int FieldInc(::google::protobuf::Message &msg, const std::set &dottedpaths);**
```
 @brief Based on the entered key values in msg and the field name specified in dottedpaths, get the value of the specified field and fill it into msg.
 @param [INOUT] msg   Data record msg. It contains the entered key value. It will be returned to the specified field and filled into msg.
 @param [IN] dottedpaths Dotted nested string sets of the field name
 @param [OUT] failedpaths Dotted nested string sets where query failed
 @retval <0   Failed. The corresponding error code is returned.
 @retval 0    Succeeded. 0 is returned when at least one field query succeeds.
```
**int FieldGet(const std::set<std::string> &dottedpaths, ::google::protobuf::Message \*msg, std::set<std::string> \*failedpaths);**
```
 @brief Based on the entered key values in msg and the field name specified in dottedpaths, update the value of the specified field. Values that currently do not exist on the server will be added.
 @param [IN] msg The entered key value, which will be returned to the specified field and filled into msg.
 @param [IN] dottedpaths Dotted nested string sets of the field name
 @retval <0   Failed. The corresponding error code is returned. Indicates that no field is updated.
 @retval 0    Succeeded. Indicates all fields have been updated.
```
**int FieldSet(::google::protobuf::Message &msg, const std::set &dottedpaths);**
```
 @brief Obtain multiple record values by indexes based on the index name, msg value, offset and limit in the entered req, fill them into the vec structure of res, and return the total and remaining number of records.
 @param [INOUT] req   The entered req
 @param [INOUT] res   The entered res
 @retval <0   Failed. The corresponding error code is returned.
 @retval 0    Succeeded.
```
**int Get(NS_TCAPLUS_PROTOBUF_API::IndexGetRequest& req, NS_TCAPLUS_PROTOBUF_API::IndexGetResponse \*res);**
```
 @brief Traverse tables. Messages are filled into msg.
 @param [INOUT] msg  It will be returned to the specified field and filled into msg.
 @param [INOUT] cb   Callback function
 @retval <0   Failed. The corresponding error code is returned.
 @retval 0    Transversal succeeded.
```
**int Traverse(::google::protobuf::Message \*msg, TcaplusTraverseCallback \*cb);**

## Rules and Restrictions
### Get restrictions
1. It cannot query records of a specific version.
2. If the field to be queried does not exist in the original record, the default value of the field will be returned.

### BatchGet restrictions
1. Batch query must be processed using tcaproxy for message routing. The tcapsvr process does not support batch query.
2. Each batch query request returns a result, and timeout is 10 seconds.
3. The number of returned results is equal to number of requests. All failed or non-existent records are included in an empty recorded, and you can use FetchRecord to get these records.
4. Batch query result set cannot exceed 256 KB, otherwise an empty record will be returned.
5. Sequence of returned results may not be consistent with the request sequence.

### FieldInc restrictions
1. The record of the key specified in message must exist.
2. The field specified in dottedpaths must be numeric.
3. The maximum number of elements in the set of dottedpaths is 128.
4. The maximum length of each element in the set of dottedpaths is 1,023 bytes.
5. The maximum nesting depth of the field for each element in the set of dottedpaths is 32.

### FieldGet restrictions
3. The maximum number of elements in the set of dottedpaths is 128.
4. The maximum length of each element in the set of dottedpaths is 1,023 bytes.
5. The maximum nesting depth of the field for each element in the set of dottedpaths is 32.

### FieldSet restrictions
3. The maximum number of elements in the set of dottedpaths is 128.
4. The maximum length of each element in the set of dottedpaths is 1,023 bytes.
5. The maximum nesting depth of the field for each element in the set of dottedpaths is 32.


## Directory Structure of Source SDK Files

    `-- release
        `-- x86_64
            |-- docs                                   Document directory
            |   `-- tcaplus
            |       `-- readme.txt                     Instructions about how to use the C++ SDK
            |-- examples                               Example directory of the C++ SDK, which can be divided into two parts: synchronous and asynchronous. Examples can be used directly.
            |-- include                                Header file directory of the C++ SDK
            |   `-- tcaplus_pb_api                     Header file folder of TcaplusDB PB API
            |       |-- cipher_suite_base.h            Base of data encryption code algorithm suites
            |       |-- default_aes_cipher_suite.h     The default implementation class of data encryption code algorithm suites
            |       |-- tcaplus_async_pb_api.h         Header files in async mode. Use TcaplusAsyncPbApi class in async mode.
            |       |-- tcaplus_coroutine_pb_api.h         Header files in coroutine mode. Use TcaplusCoroutinePbApi class in coroutine mode.
            |       |-- tcaplus_error_code.h           Error code header files, where you can find the definitions and descriptions related to error codes.
            |       |-- tcaplus_protobuf_api.h         Summarized header files of API, including all header files. Simply import this file for easy development.
            |       |-- tcaplus_protobuf_define.h      Header files of basic structures and macro definitions, including ClientOptions structure and MESSAGE_OPTION_* macro definition
            |       |-- tcaplusservice.optionv1.pb.h   Protobuf header files of common definitions of Tcaplus tables
            |       `-- tcaplusservice.optionv1.proto  Proto source files of common definitions of Tcaplus tables. Required when customizing tables.
            |-- lib                                    Library file directory of the C++ SDK
            |   `-- libtcaplusprotobufapi.a             Library files of the C++ SDK. It shall be included in the link library of the final app.
            `-- version                                Record file of versions of the C++ SDK




