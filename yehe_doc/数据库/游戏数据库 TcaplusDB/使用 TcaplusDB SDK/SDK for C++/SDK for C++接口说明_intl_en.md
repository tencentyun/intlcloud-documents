## Overview
TcaplusDB service API is the data access entry for your application to access TcaplusDB and the programming API for your application to access business data in TcaplusDB. Currently, TcaplusDB mainly uses Google Protocol Buffer (Protobuf) to implement communication and data element definition.

## Process
After you activate the service in the [console](https://console.cloud.tencent.com/tcaplusdb/table) and create a table, the details page will display the access ID, access password, and private IP address, and the Protobuf table management page will provide information such as the name of the created table and table group ID. You can use TcaplusDB API for C++ to enable your application to manipulate multiple tables in the cluster.

## Module
You can use the Protobuf protocol to define tables compliant with the TcaplusDB specifications. You can create a table or modify an existing table by transferring the metafile of the table definition to the TcaplusDB Console. After the operation succeeded, you can use TcaplusDB Protobuf API to read/write table data records. Currently, TcaplusDB Protobuf API supports the following operations:

| Operation | Feature Description |
|---------|---------|
| GET | Gets the information of one value based on one field |
| BATCHGET | Gets the information of multiple values based on multiple fields |
| ADD | Inserts a data entry. If the record of the corresponding field already exists, an error will be returned |
| SET | Updates data if the record corresponding to the field exists or inserts data request if the record does not exist |
| DEL| Deletes corresponding record based on field |
| FIELDINC | Adds specified value based on specified field value (integer) |
| FIELDSET | Updates the values of one or multiple specified fields |
| FIELDGET | Gets the values of one or multiple specified fields |
| INDEXGET | Queries index by specified index and field |
| TRAVERSE | Traverses full table by specified table name |

## TcaplusDB SDK Conventions
You need to define table information such as primary key fields for TcaplusDB. The extension `tcaplusservice.optionv1.proto` is embedded in the TcaplusDB system, so you only need to import it when customizing a table but do not need to upload it when creating a table or modifying an existing table. Its specific content is as shown below:
```
extend google.protobuf.MessageOptions
{
    optional string tcaplus_primary_key             = 60000; // Define the table primary key
    repeated string tcaplus_index                   = 60001; // Define the table index
    optional string tcaplus_field_cipher_suite      = 60002; // Define the encryption algorithm used by table fields
    optional string tcaplus_record_cipher_suite     = 60003; // Define the encryption algorithm used by table fields, which is reserved now
    optional string tcaplus_cipher_md5              = 60004; // Return the information summary of the `cipher` field
    optional string tcaplus_sharding_key            = 60005; // TcaplusDB sharding key
}

extend google.protobuf.FieldOptions
{
    optional uint32 tcaplus_size                    = 60000; // Field size, which is reserved now
    optional string tcaplus_desc                    = 60001; // Field description
    optional bool tcaplus_crypto                    = 60002; // Whether to encrypt the field. The encryption algorithm is defined by `tcaplus_field_cipher_suite`
}
```
The complete file can be found in the `release\x86_64\include\tcaplus_pb_api\tcaplusservice.optionv1.proto` directory.
1. The table name must start with a letter or underscore and can only contain up to 31 digits, letters, and underscores.
2. Protobuf has limited that the name of each field can contain only letters or underscores.
3. A primary key can have up to 4 fields, which must be in `required` type, and their length after packaging cannot exceed 1,022 bytes.
4. The size of a packaged field value cannot exceed 256 KB, and the whole packaged record cannot exceed 256 KB.
5. Besides the primary key fields, there must be at least one general key.
6. A table is in `generic` type by default, which is not displayed publicly.
7. Currently, the primary key fields can only be in scalar value types specified by Protobuf rather than other complex or custom types.

## Common API Description
- **int Get(::google::protobuf::Message &msg);**
```
 @brief   This API is used to get multiple record values and input them into the `vec` structure in `res` through the index based on the entered `index` name, `msg` value, `offset`, and `limit` in `req` and return the total number of records and number of remaining records
 @param [INOUT] req   Enteredd `req`
 @param [INOUT] res   Entered `res`
 @retval <0   Failure. The corresponding error code will be returned
 @retval 0    Success
```

- **int BatchGet(std::vector< ::google::protobuf::Message * > &msgs);**
```
  @brief   This API is used to get the `msg` field values in batches based on the entered `msgs` field values and input them into `msgs`
  @param [INOUT] msgs   Entered field list, which will return the specified fields and input them into `msgs`
  @retval <0   Failure. The corresponding error code will be returned
  @retval 0    Success. 0 will be returned only if at least one field is successfully queried.
```

- **int Add(::google::protobuf::Message \*msg);**
```
 @brief   This API is used to insert the `msg` data record based on the field entered in `msg`. If the field already exists, an error will be reported, and the operation will exit
 @param [INOUT] msg   Entered field value and data record `msg` to be inserted
 @retval <0   Failure. The corresponding error code will be returned
 @retval 0    Success
```

- **int Set(const ::google::protobuf::Message &msg);**
```
 @brief    This API is used to update the specified record value based on the field entered in `msg`. If the record already exists, it will be updated to the specified value; otherwise, the specified record will be inserted
 @param [INOUT] msg   Entered field value and data record `msg` to be set
 @retval <0   Failure. The corresponding error code will be returned
 @retval 0    Success
```

- **int Del(const ::google::protobuf::Message &msg);**
```
  @brief   This API is used to delete `msg` based on the field value entered in `msg`       
  @param [IN] msg   Entered field value, which will return the specified fields and input them into `msg`
  @retval <0   Failure. The corresponding error code will be returned
  @retval 0    Success. 0 will be returned only if at least one field is successfully queried.
```

- **int FieldInc(::google::protobuf::Message &msg, const std::set &dottedpaths);**
```
 @brief   This API is used to add a field value in `msg` based on the field value entered in `msg`, `values` incremental value, and field name specified by `dottedpaths`. The field is a numeric variable
 @param [INOUT] msg   Data record `msg`, which contains the entered field value and will return the result value of the incremental field and update it into `msg`
 @param [IN] dottedpaths   Dotted and nested string set of field names
 @retval <0   Failure. The corresponding error code will be returned, which indicates that no fields are updated
 @retval 0    All fields are updated successfully
```

- **int FieldGet(const std::set<std\::string> &dottedpaths, ::google::protobuf::Message \*msg, std::set<std\::string> \*failedpaths);**
```
 @brief   This API is used to get the value of a specified field and input it into `msg` based on the field value entered in `msg` and field name specified by `dottedpaths`
 @param [INOUT] msg   Data record `msg`, which contains the entered field value and will return the specified field and input it into `msg`
 @param [IN] dottedpaths   Dotted and nested string set of field names
 @param [OUT] failedpaths   Dotted and nested string set of field names which failed to be found will be returned
 @retval <0   Failure. The corresponding error code will be returned
 @retval 0    Success. 0 will be returned only if at least one field is successfully queried
```

- **int FieldSet(::google::protobuf::Message &msg, const std::set &dottedpaths);**
```
 @brief   This API is used to update the value of a specified field based on the field value entered in `msg` and field name specified by `dottedpaths`. If the value does not exist on the server, it will be inserted
 @param [IN] msg   Entered field value, which will return the specified fields and input them into `msg`
 @param [IN] dottedpaths   Dotted and nested string set of field names
 @retval <0   Failure. The corresponding error code will be returned, which indicates that no fields are updated
 @retval 0    All fields are updated successfully
```

- **int Get(NS_TCAPLUS_PROTOBUF_API::IndexGetRequest& req, NS_TCAPLUS_PROTOBUF_API::IndexGetResponse \*res);**
```
 @brief   This API is used to get multiple record values and input them into the `vec` structure in `res` through the index based on the entered `index` name, `msg` value, `offset`, and `limit` in `req` and return the total number of records and number of remaining records
 @param [INOUT] req   Enteredd `req`
 @param [INOUT] res   Entered `res`
 @retval <0   Failure. The corresponding error code will be returned
 @retval 0    Success
```

- **int Traverse(::google::protobuf::Message \*msg, TcaplusTraverseCallback \*cb);**
```
 @brief   This API is used to traverse the table. The message will be input into `msg`
 @param [INOUT] msg   The specified field will be returned and input into `msg`
 @param [INOUT] cb   Callback function
 @retval <0   Failure. The corresponding error code will be returned
 @retval 0    Traversal succeeded
```


## Rules and Limits
### Get operation limits
- You cannot query a record on a specified version.
- If the original record of the field to be queried does not exist, the field's default value will be returned.

### BatchGet operation limits
- One batch query result will be returned for one batch query request, and the batch query timeout period is 10 seconds.
- The number of records in a batch query result is the same as that of the records in the request. Even if a record does not exist or failed to be queried, an empty record will still be output in the result set. Therefore, you need to use `FetchRecord` to get the records.
- The total size of a batch query result set cannot exceed 256 KB; otherwise, only empty records will be returned.
- The sequence of the records returned in the batch query result set may be different from that of the records in the request.

### FieldInc operation limits
- Field records specified in `message` must exist.
- Fields specified in `dottedpaths` must be numeric.
- The total number of elements in the `set` where `dottedpaths` is cannot exceed 128.
- The length of each element in the `set` where `dottedpaths` is cannot exceed 1,023 bytes.
- The number of nesting levels of a field represented by each element in the `set` where `dottedpaths` is cannot exceed 32.

### FieldGet operation limits
- The total number of elements in the `set` where `dottedpaths` is cannot exceed 128.
- The length of each element in the `set` where `dottedpaths` is cannot exceed 1,023 bytes.
- The number of nesting levels of a field represented by each element in the `set` where `dottedpaths` is cannot exceed 32.

### FieldSet operation limits
- The total number of elements in the `set` where `dottedpaths` is cannot exceed 128.
- The length of each element in the `set` where `dottedpaths` is cannot exceed 1,023 bytes.
- The number of nesting levels of a field represented by each element in the `set` where `dottedpaths` is cannot exceed 32.


## SDK Source File Directory Structure

    `-- release
        `-- x86_64
            |-- docs                                   Documentation directory
            |   `-- tcaplus
            |       `-- readme.txt                     User guide file of SDK for C++
            |-- examples                               Directory of SDK for C++ samples, which include sync and async samples and can be modified and used directly
            |-- include                                Header file directory of SDK for C++
            |   `-- tcaplus_pb_api                     Header folder of TcaplusDB PB API
            |       |-- cipher_suite_base.h            Base class of data encryption algorithm suite
            |       |-- default_aes_cipher_suite.h     Default implementation class of data encryption algorithm suite
            |       |-- tcaplus_async_pb_api.h         Async mode header file, which uses the `TcaplusAsyncPbApi` class in async mode
            |       |-- tcaplus_coroutine_pb_api.h     Coroutine mode header file, which uses the `TcaplusCoroutinePbApi` class in coroutine mode
            |       |-- tcaplus_error_code.h           Error code header file, where the corresponding definitions and descriptions of all involved error codes can be found
            |       |-- tcaplus_protobuf_api.h         Aggregated API header file, which contains other header files. You can simply import this file for easy development
            |       |-- tcaplus_protobuf_define.h      Basic structure and macro definition header file, which contains the `ClientOptions` structure and `MESSAGE_OPTION_*` macro definition
            |       |-- tcaplusservice.optionv1.pb.h   Protobuf header file for common TcaplusDB table definition
            |       `-- tcaplusservice.optionv1.proto  .proto source file for common TcaplusDB table definition. This file is required when you customize a table
            |-- lib                                    Library file directory of SDK for C++
            |   `-- libtcaplusprotobufapi.a            Library file of SDK for C++, which must be contained in the program's final link library
            `-- version                                Version record file of SDK for C++
