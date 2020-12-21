TencentDB for TcaplusDB supports two table definition languages: Protocol Buffers (Protobuf) and Tencent Data Representation (TDR).
Protobuf is a method of serializing structured data developed by Google, which emphasizes simplicity and performance.
TDR is a platform-neutral data description language developed by Tencent, which combines the advantages of XML, binary language, and object-relational mapping (ORM) and is widely used in data serialization scenarios of Tencent's games.
Both languages are equally useful. Use either of them based on your usage habits.
This document describes how to define tables in Protobuf.

## Table Definition in Protobuf
To create a table in TcaplusDB, you first need to use a table description language to define the table format and write the table definition content into a table IDL description file.
The table IDL description file defines the table based on Protocol Buffers rules.
The definition information is mainly divided into three types:
- File definition information
- Table definition information
- Nested type information

## File Definition
The file definition information area mainly defines the common information of the current table description file, which contains the following three types of contents:

| Option Name | Description | Sample Value | Required |
| --- | --- | --- | --- |
| syntax | It specifies the syntax specification version for writing the current file. | proto2, proto3 | Yes |
| package | It specifies the custom package name of the current file, which helps avoid name conflicts with messages. | Package name information | Yes |
| importIt | It indicates some common information imported into the TcaplusDB table, which must be imported in the table definition. | tcaplusservice.optionv1.proto | Yes |


## Table Definition

In table definition information, the table format (including extended information and field information) is defined in a message.
#### Extended information definition
Table definition information can be extended by `option` on the basis of Protobuf syntax, which can implement richer semantic features. The definable content is as shown below:
The detailed definition format is `option(tcaplusservice.option) = "value";`.

| Option Name | Description | Configuration Example | Required |
| --- | --- | --- | --- |
| tcaplus_primary_key | Sets the primary key field of the TcaplusDB table. | option(tcaplusservice.tcaplus_primary_key) = "uin,name,region"; | Yes |
| tcaplus_index | Sets the index key field of the TcaplusDB table. | option(tcaplusservice.tcaplus_index) = "index_1(uin,region)"; | No |
| tcaplus_sharding_key | You can customize the table shardkey. | option(tcaplusservice.tcaplus_sharding_key) = "uin"; | No |
| tcaplus_field_cipher_suite | It is required if the field encryption feature is used. To specify your custom encryption algorithm, see the example in the API documentation. | option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; | No |
| tcaplus_cipher_md5 | MD5 (used to encrypt the password string, which is stored at the user side) should be set if the field encryption feature is used. | option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; | No |

#### Field information definition

TcaplusDB field definition format is `field modifier field type field name = identifier[special definition];`.
##### Field modifier
proto2 supports three limiting modifiers, while proto3 no longer supports the `REQUIRED` modifier and uses `OPTIONAL` as the default modifier.
- REQUIRED: it indicates that the field is required. In proto2, primary key fields must be declared with `REQUIRED`.
- OPTIONAL: it indicates that the field is optional. You can set a default value for an optional field.
- REPEATED: it indicates that the field can contain 0–N elements. Its features are the same as those of `OPTIONAL`, but it can contain multiple values at a time, which can be considered as an array. The special definition of `[packed = true]` must be specified.

##### Field type
TcaplusDB supports general fields and nested fields. For more information, please see [Data Types](https://intl.cloud.tencent.com/document/product/1016/38659).
##### Field name
You can name a field based on its current attribute. The name can contain letters, digits, and underscores and cannot start with a digit. You are recommended to use camelCase for the name.
##### Identifier
Identifier value range: [1,2^29 - 1]
Identifiers within [19000,19999] cannot be used, as they are reserved in Protocol Buffers. If you use any of them, an error will be reported.
Each field will occupy memory when being encoded, and the occupied memory size is subject to the identifier:
- A field with an identifier within [1,15] occupies 1 byte during encoding.
- A field with an identifier within [16,2047] occupies 2 bytes during encoding.
##### Special definition
- You can use `packed=true` to specify a field declared with the `REPEATED` modifier. The syntax is as follows:
```
repeated int64 lockid = 6 [packed = true]; 
```
- You can use `default = 1` to specify the default value for a field declared with the `OPTIONAL` modifier. The syntax is as follows:
```
optional int32 logintime = 5 [default = 1];
```
- You can specify the fields in string and bytes types as encrypted fields. The syntax is as follows:
```
required string name = 2[(tcaplusservice.tcaplus_crypto) = true];
```

#### Nested type information
TcaplusDB supports nested types. A nested type can contain another one as its field. You can also define a new nested type in another one.
Similar to table definition, nested type definition is also declared with a message, but the nested type structure cannot contain definition of extended information such as "primary key" and "index".
TcaplusDB supports up to 128 levels of consecutive nesting; however, you are not recommended to use a high number of nesting levels, as it will compromise the data access performance.

## Sample Code for Table Description File in proto2

Below is a table description file in compliance with the proto2 syntax specification:

```
syntax = "proto2";                      // Indicate compliance with the proto2 syntax specification.
package myTcaplusTable;                 // Custom package name

import "tcaplusservice.optionv1.proto"; // Define some common information of the TcaplusDB table, which should be imported in your table definition.

message player {  // Use a message to define the table, and the message name is the table name.

    // Only the message for which the primary key option (tcaplusservice.tcaplus_primary_key) is specified can be recognized as a TcaplusDB business data table. Otherwise, the message is only a structure.
    // The primary key option specifies the list of primary key field names that are separated by commas. Up to four fields can be specified as primary keys.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // Use the "tcaplusservice.tcaplus_index" option to specify the TcaplusDB index.
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // "option(tcaplusservice.tcaplus_sharding_key) = "uin";". You can explicitly set the index sharding field. If you do not explicitly set it, the system will use a primary key field as the sharding field by default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Use the default "DefaultAesCipherSuite" encryption function. This parameter is optional.
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Set the MD5 value of the encryption password string. This parameter is optional.

    // The following shows the definition of table fields.
    // A TcaplusDB table supports the following data types:
    // Non-nested types: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Nested type: message
    // TcaplusDB supports three field modifiers: REQUIRED, OPTIONAL and REPEATED.

    // (Up to four) primary key fields
    required int64 uin = 1;  // The primary key fields must be declared with the REQUIRED modifier. Nested data types are not supported.
    required string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // The string-type and bytes-type fields in a message can be specified as encrypted fields. This parameter is optional.
    required int32 region = 3;
    // A table can contain up to four primary key fields.

    // General value field.
    required int32 gamesvrid = 4; // General fields can be declared with REQUIRED, OPTIONAL, and REPEATED modifiers.
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // The "packed=true" option should be specified for the fields declared with the REPEATED modifier.
    optional bool is_available = 7 [default = false]; // You can specify a default value for an OPTIONAL field.
    optional pay_info pay = 8; // Value fields can be in custom structure types.
}

message pay_info { // Use a message to define the structure.

    required int64 pay_id = 1;
    optional uint64 total_money = 2;
    optional uint64 pay_times = 3;
    optional pay_auth_info auth = 4;

    message pay_auth_info { // Structure types support nested definition.
        required string pay_keys = 1;
        optional int64 update_time = 2;
    }
}
```


## Sample Code for Table Description File in proto3
Below is a table description file in compliance with the proto3 syntax specification:
```
syntax = "proto3";                      // Indicate compliance with the proto3 syntax specification.
package myTcaplusTable;                 // Custom package name

import "tcaplusservice.optionv1.proto"; // Define some common information of the TcaplusDB table, which should be imported in your table definition.

message player {  // Use a message to define the table, and the message name is the table name.

    // Only the message for which the primary key option (tcaplusservice.tcaplus_primary_key) is specified can be recognized as a TcaplusDB business data table. Otherwise, the message is only a structure.
    // The primary key option specifies the list of primary key field names that are separated by commas. Up to four fields can be specified as primary keys.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // Use the "tcaplusservice.tcaplus_index" option to specify the TcaplusDB index.
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // "option(tcaplusservice.tcaplus_sharding_key) = "uin";". You can explicitly set the sharding field. If you do not explicitly set it, the system will use a primary key field as the sharding field by default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Use the default "DefaultAesCipherSuite" encryption function. This parameter is optional.
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Set the MD5 value of the encryption password string. This parameter is optional.

    // The following shows the definition of table fields.
    // A TcaplusDB table supports the following data types:
    // Non-nested types: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Nested type: message

    // (Up to four) primary key fields
    int64 uin = 1;  // The primary key fields must be in non-nested types.
    string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // The string-type and bytes-type fields in a message can be specified as encrypted fields. This parameter is optional.
    int32 region = 3;
    // A table can contain up to four primary key fields.

    // General value field.
    int32 gamesvrid = 4;
    int32 logintime = 5;
    int64 lockid = 6;
    bool is_available = 7;
    pay_info pay = 8; // Value fields can be in custom structure types.
}

message pay_info { // Use a message to define the structure.

    int64 pay_id = 1;
    uint64 total_money = 2;
    uint64 pay_times = 3;
    pay_auth_info auth = 4;

    message pay_auth_info { // Structure types support nested definition.
        string pay_keys = 1;
        int64 update_time = 2;
    }
}
```