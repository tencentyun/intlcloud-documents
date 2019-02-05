[//]: # (chinagitpath:XXXXX)

TcaplusDB defines App data tables using the Google Protobuf file, and supports the proto2 and proto3 syntax rules. The following describes the rules for the proto table structure description file.

## Rules for proto2 Table Creation File

The following is an example of a table creation file that meets the proto2 syntax rule.

```
syntax = "proto2";                      // Indicates that the file meets the proto2 syntax rule.
package myTcaplusTable;                 // The name of the custom package.

import "tcaplusservice.optionv1.proto"; // Defines some common information of the Tcaplus table, which should be imported in your table definition.

message tb_example {  // message is used to define the table. The message name is the table name.

    // Only the message for which the primary key option (tcaplusservice.tcaplus_primary_key) is specified can be recognized as a TcaplusDB App data table. Otherwise, the message is only a structure.
    // The primary key option specifies the list of primary key field names that are separated by commas. Up to four fields can be specified as primary keys.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // The tcaplusservice.tcaplus_index option specifies the Tcaplus index.
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    //option(tcaplusservice.tcaplus_sharding_key) = "uin"; You can explicitly set the index shard key that must be a subset of the intersection of all index key fields. If it is not explicitly set, the intersection of the index key set is used as the shard key by default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // (Optional) The default encryption function DefaultAesCipherSuite is used.
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // (Optional) Sets the MD5 value used to encrypt the password string.

    // The following shows the definition of table fields.
    // A Tcaplus table supports the following data types:
    // Non-nested: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Nested: message
    // Tcaplus supports three field modifiers: REQUIRED, OPTIONAL and REPEATED.

    // Primary key fields (4 at most)
    required int64 uin = 1;  // The primary key fields must be declared with the modifier REQUIRED. Non-nested data types are not supported.
    required string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // (Optional) Fields with string and bytes types in the message can be specified as encryption fields.
    required int32 region = 3;
    // A table can contain up to four primary key fields.

    // Common value field.
    required int32 gamesvrid = 4; // Common fields can be declared as either REQUIRED, OPTIONAL and REPEATED modifiers. 
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // The packed=true option should be specified for the fields declared with the modifier REPEATED.
    optional bool is_available = 7 [default = false]; // A default value can be specified for optional-type fields.
    optional pay_info pay = 8; // The type of the value field can be a custom structure type.
}

message pay_info { // message is used to define the structure.

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

### Rules for proto2 table creation file

| No. | Category | Rule |
| -----------------|-------------- | ------------ |
| 1 | Syntax | The proto table definition file must meet the protobuf syntax rule. The file header is identified using `syntax = "proto2";`. |
| 2 | Syntax | The common definition file `tcaplusservice.optionv1.proto` must be imported in the table creation file. |
| 3 | Syntax | The message is used to define tables and common structures. If this message contains the `tcaplusservice.tcaplus_primary_key` option, it is a TcaplusDB App data table definition; otherwise, it is a structure definition. |
| 4 | Field rule | TcaplusDB tables support non-nested type fields: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, and bytes, as well as a nested type field: message. |
| 5 | Field rule | TcaplusDB tables support three field modifiers: REQUIRED, OPTIONAL and REPEATED. |
| 6 | Field rule | TcaplusDB tables contain up to 4 primary key fields and 128 non-primary key fields. |
| 7 | Field rule | TcaplusDB tables contain 1 to 4 `REQUIRED non-nested type` primary keys that are specified using the `tcaplusservice.tcaplus_primary_key` option. The option value is the primary key field name list string, and the primary key fields are separated by commas, such as option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";. |
| 8 | Field rule | Supports defining `non-primary key` fields with nested structure. The maximum nested depth is restricted to 30, and the data access capacity will be compromised if this limit is exceeded. |
| 9 | Field rule | A TcaplusDB table supports creating 0 to 4 indexes which are specified using the `tcaplusservice.tcaplus_index` option, such as option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";. Wherein, "index_1" is the custom index name, and "uin,region" is the list of primary key field names that are separated by commas. |
| 10 | Field rule | The table index key in TcaplusDB tables must be a primary key. If multiple index keys are defined, the intersection of multiple index key sets cannot be empty. |
| 11 | Field rule | You can explicitly set the shard key using the `tcaplusservice.tcaplus_sharding_key` option which must be a subset of the intersection of all index key fields. If it is not explicitly set, the intersection of the index key set is used as the shard key by default. The setting of the shard key is subject to the distribution of backend data. You need to evaluate whether the value of the field used as the key shard is discrete. It is not recommended to set the fields (such as gender, week, etc.) with limited value range as the shard key |
| 12 | Field rule | [packed=true] must be specified for the REPEATED-type fields. |
| 13 | Field rule | In the TcaplusDB table definition, fields with string and bytes types can be specified as encryption fields. TcaplusAPI encrypts the transfer and storage of the field that comes with the `[(tcaplusservice.tcaplus_crypto) = true]` option using the encryption tool specified by the `tcaplusservice.tcaplus_field_cipher_suite` option and the password pair specified by you. |
| 14 | Record rule | A single TcaplusDB data record is limited to 256 KB. |

## Rules for proto3 Table Creation File

```
syntax = "proto3";                      // Indicates that the file meets the proto3 syntax rule.
package myTcaplusTable;                 // The name of the custom package.

import "tcaplusservice.optionv1.proto"; // Defines some common information of the Tcaplus table, which should be imported in your table definition.

message tb_example {  // message is used to define the table. The message name is the table name.

    // Only the message for which the primary key option (tcaplusservice.tcaplus_primary_key) is specified can be recognized as a TcaplusDB App data table. Otherwise, the message is only a structure.
    // The primary key option specifies the list of primary key field names that are separated by commas. Up to four fields can be specified as primary keys.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // The tcaplusservice.tcaplus_index option specifies the Tcaplus index.
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    //option(tcaplusservice.tcaplus_sharding_key) = "uin"; You can explicitly set the index shard key that must be a subset of the intersection of all index key fields. If it is not explicitly set, the intersection of the index key set is used as the shard key by default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // (Optional) The default encryption function DefaultAesCipherSuite is used.
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // (Optional) Sets the MD5 value used to encrypt the password string.

    // The following shows the definition of table fields.
    // A Tcaplus table supports the following data types:
    // Non-nested: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Nested: message

    // Primary key fields (4 at most)
    int64 uin = 1;  // The primary key field must be of a non-nested type.
    string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // (Optional) Fields with string and bytes types in the message can be specified as encryption fields.
    int32 region = 3;
    // A table can contain up to four primary key fields.

    // Common value field.
    int32 gamesvrid = 4;
    int32 logintime = 5;
    int64 lockid = 6;
    bool is_available = 7;
    pay_info pay = 8; // The type of the value field can be a custom structure type.
}

message pay_info { // message is used to define the structure.

    int64 pay_id = 1;
    uint64 total_money = 2;
    uint64 pay_times = 3;
    pay_auth_info auth = 4;

    message pay_auth_info { // The structure type supports nested definitions.
        string pay_keys = 1;
        int64 update_time = 2;
    }
}
```

### Rules for proto3 table creation file


| No. | Category | Rule |
| -----------------|-------------- | ------------ |
| 1 | Syntax | The proto table definition file must meet the protobuf syntax rule. The file header is identified using `syntax = "proto3";`. |
| 2 | Syntax | The common definition file `tcaplusservice.optionv1.proto` must be imported in the table creation file. |
| 3 | Syntax | The message is used to define tables and common structures. If this message contains the `tcaplusservice.tcaplus_primary_key` option, it is a TcaplusDB App data table definition; otherwise, it is a structure definition. |
| 4 | Field rule | TcaplusDB tables support non-nested type fields: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, and bytes, as well as a nested type field: message. |
| 5 | Field rule | TcaplusDB tables contain up to 4 primary key fields and 128 non-primary key fields. |
| 6 | Field rule | TcaplusDB tables contain 1 to 4 `non-nested type` primary keys that are specified using the `tcaplusservice.tcaplus_primary_key` option. The option value is the primary key field name list string, and the primary key fields are separated by commas, such as option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";. |
| 7 | Field rule | Supports defining `non-primary key` fields with nested structure. The maximum nested depth is restricted to 30, and the data access capacity will be compromised if this limit is exceeded. |
| 8 | Field rule | A TcaplusDB table supports creating 0 to 4 indexes which are specified using the `tcaplusservice.tcaplus_index` option, such as option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";. Wherein, "index_1" is the custom index name, and "uin,region" is the list of primary key field names that are separated by commas. |
| 9 | Field rule | The table index key in TcaplusDB tables must be a primary key. If multiple index keys are defined, the intersection of multiple index key sets cannot be empty. |
| 10 | Field rule | You can explicitly set the shard key using the `tcaplusservice.tcaplus_sharding_key` option which must be a subset of the intersection of all index key fields. If it is not explicitly set, the intersection of the index key set is used as the shard key by default. The setting of the shard key is subject to the distribution of backend data. You need to evaluate whether the value of the field used as the key shard is discrete. It is not recommended to set the fields (such as gender, week, etc.) with limited value range as the shard key. |
| 11 | Field rule | In the TcaplusDB table definition, fields with string and bytes types can be specified as encryption fields. TcaplusAPI encrypts the transfer and storage of the field that comes with the `[(tcaplusservice.tcaplus_crypto) = true]` option using the encryption tool specified by the `tcaplusservice.tcaplus_field_cipher_suite` option and the password pair specified by you. |
| 12 | Record rule | A single TcaplusDB data record is limited to 256 KB. |

## Description of tcaplusservice.tcaplus_* Option

The TcaplusDB table definition file is extended using the option based on the protobuf syntax, which can implement more semantic features.

| Option Name | Description | Configuration Example | Required |
| --- | --- | --- | --- |
| tcaplus_primary_key | Sets the primary key field of the TcaplusDB table. | option(tcaplusservice.tcaplus_primary_key) = "uin,name,region"; | Yes |
| tcaplus_index | Sets the index key field of the TcaplusDB table. | option(tcaplusservice.tcaplus_index) = "index_1(uin,region)"; | No |
| tcaplus_sharding_key | You can customize the table shard key after setting the table index key. | option(tcaplusservice.tcaplus_sharding_key) = "uin"; | No |
| tcaplus_field_cipher_suite | It is required if the field encryption feature is used. To specify your custom encryption algorithm, see the example in the API documentation. | option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; | No |
| tcaplus_cipher_md5 | MD5 (used to encrypt the password string, which is stored at the user side) should be set if the field encryption feature is used. | option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; | No |



