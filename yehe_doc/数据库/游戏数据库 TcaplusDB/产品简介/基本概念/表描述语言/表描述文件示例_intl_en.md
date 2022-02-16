## Sample proto2 Table Description File
Below is a table description file in compliance with the proto2 syntax specification:

```
syntax = "proto2";                      // Indicate compliance with the proto2 syntax specification
package myTcaplusTable;                 // Custom package name

import "tcaplusservice.optionv1.proto"; // This file defines some common information of the TcaplusDB table, which should be imported into your table definition

message player {  // Use a message to define the table, and the message name is the table name

    // Only the message for which the primary key option (tcaplusservice.tcaplus_primary_key) is specified can be recognized as a TcaplusDB business data table; otherwise, the message is only a structure
    // The primary key option specifies the list of primary key field names that are separated by commas. Up to four fields can be specified as primary keys
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // The `tcaplusservice.tcaplus_index` option specifies the TcaplusDB index
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // `option(tcaplusservice.tcaplus_sharding_key) = "uin";` You can explicitly set the index sharding field. If you do not explicitly set it, the system will use a primary key field as the sharding field by default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Use the default `DefaultAesCipherSuite` encryption function. This parameter is optional
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Set the MD5 value of the encryption password string. This parameter is optional

    // The following shows the definition of table fields
    // A TcaplusDB table supports the following data types:
    // Non-nested types: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Nested type: message
    // TcaplusDB supports three field modifiers: REQUIRED, OPTIONAL, and REPEATED

    // Primary key fields (4 at most)
    required int64 uin = 1;  // The primary key fields must be declared with the `required` modifier. Nested data types are not supported
    required string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // The string-type and bytes-type fields in a message can be specified as encrypted fields. This parameter is optional
    required int32 region = 3;
    // A table can contain up to four primary key fields

    // General value field
    required int32 gamesvrid = 4; // General fields can be declared with `required`, `optional`, and `repeated` modifiers
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // The `packed=true` option should be specified for the fields declared with the `repeated` modifier
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


## Sample proto3 Table Description File
Below is a table description file in compliance with the proto3 syntax specification:
```
syntax = "proto3";                      // Indicate compliance with the proto3 syntax specification
package myTcaplusTable;                 // Custom package name

import "tcaplusservice.optionv1.proto"; // This file defines some common information of the TcaplusDB table, which should be imported into your table definition

message player {  // Use a message to define the table, and the message name is the table name

    // Only the message for which the primary key option (tcaplusservice.tcaplus_primary_key) is specified can be recognized as a TcaplusDB business data table; otherwise, the message is only a structure
    // The primary key option specifies the list of primary key field names that are separated by commas. Up to four fields can be specified as primary keys
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // The `tcaplusservice.tcaplus_index` option specifies the TcaplusDB index
    // The index keys included in each index must be primary keys, and the intersection of all index field sets cannot be empty
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // `option(tcaplusservice.tcaplus_sharding_key) = "uin";` You can explicitly set the sharding field. If you do not explicitly set it, the system will use a primary key field as the sharding field by default.

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

    // General value field
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
