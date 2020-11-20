TcaplusDB defines business data tables by using the Google Protobuf file format and supports the proto2 and proto3 syntax specifications. The following describes the specification for the proto table creation file.

## proto2 Table Creation File Specification

The following is a sample table creation file that meets the proto2 syntax specification:

```
syntax = "proto2";                      // Indicate compliance with the proto2 syntax specification
package myTcaplusTable;                 // Custom package name

import "tcaplusservice.optionv1.proto"; // This file defines some common information of the TcaplusDB table, which should be imported into your table definition

message tb_example {  // Use a message to define the table, and the message name is the table name

    // Only the message for which the primary key option (tcaplusservice.tcaplus_primary_key) is specified can be recognized as a TcaplusDB business data table; otherwise, the message is only a structure
    // The primary key option specifies the list of primary key field names that are separated by commas. Up to four fields can be specified as primary keys
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // The `tcaplusservice.tcaplus_index` option specifies the TcaplusDB index
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // `option(tcaplusservice.tcaplus_sharding_key) = "uin";` You can explicitly set the index shardkey. In principle, it must be a subset of the intersection of all index key fields. If you do not explicitly set it, the system will use the intersection of the index key sets as the shardkey by default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Use the default `DefaultAesCipherSuite` encryption function. This parameter is optional
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Set the MD5 value of the encryption password string. This parameter is optional

    // The following shows the definition of table fields
    // A TcaplusDB table supports the following data types:
    // Non-nested types: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Nested type: message
    // TcaplusDB supports three field modifiers: REQUIRED, OPTIONAL, and REPEATED

    // Primary key fields (4 at most)
    required int64 uin = 1;  // The primary key fields must be declared with the `REQUIRED` modifier. Nested data types are not supported
    required string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // The string-type and bytes-type fields in a message can be specified as encrypted fields. This parameter is optional
    required int32 region = 3;
    // A table can contain up to four primary key fields

    // Common value field
    required int32 gamesvrid = 4; // Common fields can be declared with `REQUIRED`, `OPTIONAL`, and `REPEATED` modifiers
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // The `packed=true` option should be specified for the fields declared with the `REPEATED` modifier
    optional bool is_available = 7 [default = false]; // Default values can be specified for fields in `optional` type
    optional pay_info pay = 8; // Value fields can be in custom structure types
}

message pay_info { // Use a message to define the structure

    required int64 pay_id = 1;
    optional uint64 total_money = 2;
    optional uint64 pay_times = 3;
    optional pay_auth_info auth = 4;

    message pay_auth_info { // Structure types support nested definition
        required string pay_keys = 1;
        optional int64 update_time = 2;
    }
}
```

### proto2 table creation file rule

| Number | Category | Rule |
| -----------------|-------------- | ------------ |
| 1 | Syntax | A proto table definition file must conform to the protobuf syntax specification and is identified with `syntax = "proto2";` in the file header. |
| 2 | Syntax | A table creation file must import the `tcaplusservice.optionv1.proto` common definition file. |
| 3 | Syntax | Use messages to define tables and general structures. If a message contains the `tcaplusservice.tcaplus_primary_key` option, this message is a TcaplusDB business data table definition; otherwise, it is only a structure definition. |
| 4 | Field rule | TcaplusDB tables support defining non-nested fields (int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes) and nested fields (message). |
| 5  | Field rule | TcaplusDB tables support `REQUIRED`, `OPTIONAL`, and `REPEATED` field modifiers. |
| 6 | Field rule | A TcaplusDB table can contain up to four primary key fields and up to 128 non-primary key fields. |
| 7 | Field rule | The primary keys of a TcaplusDB table are 1–4 ``REQUIRED non-nested` fields specified by the `tcaplusservice.tcaplus_primary_key` option. The value of this option is a list string of primary key field names separated by commas, such as `option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";`. |
| 8 | Field rule | `Non-primary key` fields in nested structure types can be defined, and the maximum nested depth can be 30 layers. Too large nesting depths will affect the data access performance. |
| 9 | Field rule | One single TcaplusDB table supports creating 0–4 indices specified by the `tcaplusservice.tcaplus_index` option, such as `option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";`, where `index_1` is a custom index name, and `uin,region` is a list of specified index key field names separated by commas. |
| 10 | Field rule | An index key of a TcaplusDB table must be a primary key. If multiple index keys are defined, the intersection of multiple index key sets cannot be empty. |
| 11 | Field rule | You can explicitly set the shardkey through `tcaplusservice.tcaplus_sharding_key`. In principle, it must be a subset of the intersection of all index key fields. If you do not explicitly set it, the system will use the intersection of the index key sets as the shardkey by default. The setting of the shardkey is subject to the backend data distribution. You need to evaluate whether the values of the field used as the shardkey are discrete. You are not recommended to set a field with limited values such as gender and weekday as the shardkey. |
| 12 | Field rule | `REPEATED` fields must have `[packed=true]` specified. |
| 13 | Field rule | In the TcaplusDB table definition, string-type and bytes-type fields can be specified as encrypted fields. TcaplusAPI will use the encryption tool specified by the `tcaplusservice.tcaplus_field_cipher_suite` option and the password pair specified by you to encrypt the transfer and storage of fields configured with the `[(tcaplusservice.tcaplus_crypto) = true]` option.
| 14 | Record rule | One single TcaplusDB data record can be up to 256 KB. |

## proto3 Table Creation File Specification

```
syntax = "proto3";                      // Indicate compliance with the proto3 syntax specification
package myTcaplusTable;                 // Custom package name

import "tcaplusservice.optionv1.proto"; // This file defines some common information of the TcaplusDB table, which should be imported into your table definition

message tb_example {  // Use a message to define the table, and the message name is the table name

    // Only the message for which the primary key option (tcaplusservice.tcaplus_primary_key) is specified can be recognized as a TcaplusDB business data table; otherwise, the message is only a structure
    // The primary key option specifies the list of primary key field names that are separated by commas. Up to four fields can be specified as primary keys
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // The `tcaplusservice.tcaplus_index` option specifies the TcaplusDB index
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // `option(tcaplusservice.tcaplus_sharding_key) = "uin";` You can explicitly set the index shardkey. In principle, it must be a subset of the intersection of all index key fields. If you do not explicitly set it, the system will use the intersection of the index key sets as the shardkey by default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Use the default `DefaultAesCipherSuite` encryption function. This parameter is optional
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Set the MD5 value of the encryption password string. This parameter is optional

    // The following shows the definition of table fields
    // A TcaplusDB table supports the following data types:
    // Non-nested types: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Nested type: message

    // Primary key fields (4 at most)
    int64 uin = 1;  // The primary key fields must be in non-nested types
    string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // The string-type and bytes-type fields in a message can be specified as encrypted fields. This parameter is optional
    int32 region = 3;
    // A table can contain up to four primary key fields

    // Common value field
    int32 gamesvrid = 4;
    int32 logintime = 5;
    int64 lockid = 6;
    bool is_available = 7;
    pay_info pay = 8; // Value fields can be in custom structure types
}

message pay_info { // Use a message to define the structure

    int64 pay_id = 1;
    uint64 total_money = 2;
    uint64 pay_times = 3;
    pay_auth_info auth = 4;

    message pay_auth_info { // Structure types support nested definition
        string pay_keys = 1;
        int64 update_time = 2;
    }
}
```

### proto3 table creation file rule


| Number | Category | Rule |
| -----------------|-------------- | ------------ |
| 1 | Syntax | A proto table definition file must conform to the protobuf syntax specification and is identified with `syntax = "proto3";` in the file header. |
| 2 | Syntax | A table creation file must import the `tcaplusservice.optionv1.proto` common definition file. |
| 3 | Syntax | Use messages to define tables and general structures. If a message contains the `tcaplusservice.tcaplus_primary_key` option, this message is a TcaplusDB business data table definition; otherwise, it is only a structure definition. |
| 4 | Field rule | TcaplusDB tables support defining non-nested fields (int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes) and nested fields (message). |
| 5 | Field rule | A TcaplusDB table can contain up to four primary key fields and up to 128 non-primary key fields. |
| 6 | Field rule | The primary keys of a TcaplusDB table are 1–4 `non-nested` fields specified by the `tcaplusservice.tcaplus_primary_key` option. The value of this option is a list string of primary key field names separated by commas, such as `option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";`. |
| 7 | Field rule | `Non-primary key` fields in nested structure types can be defined, and the maximum nested depth can be 30 layers. Too large nesting depths will affect the data access performance. |
| 8 | Field rule | One single TcaplusDB table supports creating 0–4 indices specified by the `tcaplusservice.tcaplus_index` option, such as `option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";`, where `index_1` is a custom index name, and `uin,region` is a list of specified index key field names separated by commas. |
| 9 | Field rule | An index key of a TcaplusDB table must be a primary key. If multiple index keys are defined, the intersection of multiple index key sets cannot be empty. |
| 10 | Field rule | You can explicitly set the shardkey through `tcaplusservice.tcaplus_sharding_key`. In principle, it must be a subset of the intersection of all index key fields. If you do not explicitly set it, the system will use the intersection of the index key sets as the shardkey by default. The setting of the shardkey is subject to the backend data distribution. You need to evaluate whether the values of the field used as the shardkey are discrete. You are not recommended to set a field with limited values such as gender and weekday as the shardkey. |
| 11 | Field rule | In the TcaplusDB table definition, string-type and bytes-type fields can be specified as encrypted fields. TcaplusAPI will use the encryption tool specified by the `tcaplusservice.tcaplus_field_cipher_suite` option and the password pair specified by you to encrypt the transfer and storage of fields configured with the `[(tcaplusservice.tcaplus_crypto) = true]` option.
| 12 | Record rule | One single TcaplusDB data record can be up to 256 KB. |

## tcaplusservice.tcaplus_* Option Description

A table definition file of TcaplusDB is extended by `option` on the basis of protobuf syntax, which can implement richer semantic features.

| Option Name | Feature Description | Example | Required |
| --- | --- | --- | --- |
| tcaplus_primary_key | This sets a primary key field for a TcaplusDB table | option(tcaplusservice.tcaplus_primary_key) = "uin,name,region"; | Yes |
| tcaplus_index | This sets an index key field for a TcaplusDB table | option(tcaplusservice.tcaplus_index) = "index_1(uin,region)"; | No |
| tcaplus_sharding_key | You can customize the table shardkey provided that the table index key is set | option(tcaplusservice.tcaplus_sharding_key) = "uin"; | No |
| tcaplus_field_cipher_suite | If you want to use the field encryption feature, you need to set this parameter. If you want to specify your own encryption algorithm, please see the API sample | option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; | No |
| tcaplus_cipher_md5 | If you want to use the field encryption feature, you need to set this parameter so that the MD5 of the encrypted password string can be saved at the user side | option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; | No |


