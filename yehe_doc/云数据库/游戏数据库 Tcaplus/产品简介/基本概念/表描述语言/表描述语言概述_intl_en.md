TcaplusDB uses the Google Protocol Buffers data description language to define tables and supports proto2 and proto3 syntax specifications. Below is the description of Proto table creation file rules.

## Table Description Language Overview
To create a table in TcaplusDB, you first need to use a table description language to define the table format and write the table definition content into a table IDL description file.
The table IDL description file defines the table based on Protocol Buffers rules.
The definition information is mainly divided into three types:
- File definition information
- Table definition information
- Nested type information

### File definition information
The file definition information area mainly defines the common information of the current table description file, which contains the following three types of contents:

| Option Name | Feature Description | Sample Value | Required |
| --- | --- | --- | --- |
| syntax | It specifies the syntax specification version for writing the current file | proto2, proto3 | Yes |
| package | It specifies the custom package name of the current file | Package name information | Yes |
| import | It indicates some common information imported into the TcaplusDB table, which must be imported in the table definition | tcaplusservice.optionv1.proto | Yes |


### Table definition information
In table definition information, the table format (including extended information and field information) is defined in a message.

#### Extended information definition
Table definition information can be extended by `option` on the basis of protobuf syntax, which can implement richer semantic features. The definable content is as shown below:
The detailed definition format is `option(tcaplusservice.option) = "value";`

| Option Name | Feature Description | Example | Required |
| --- | --- | --- | --- |
| tcaplus_primary_key | This sets a primary key field for a TcaplusDB table | `option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";` | Yes |
| tcaplus_index | This sets an index key field for a TcaplusDB table | `option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";` | No |
| tcaplus_sharding_key | You can customize the table shardkey | `option(tcaplusservice.tcaplus_sharding_key) = "uin";` | No |
| tcaplus_field_cipher_suite | If you want to use the field encryption feature, you need to set this parameter and specify your own encryption algorithm | `option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite";` | No |
| tcaplus_cipher_md5 | If you want to use the field encryption feature, you need to set this parameter so that the MD5 of the encrypted password string can be saved at the user side | `option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b";` | No |

#### Field information definition
TcaplusDB field definition format is `field modifier field type field name = identifier[special definition];`.

- **Field modifier**
proto2 supports three limiting modifiers, while proto3 no longer supports the `required` modifier and uses `optional` as the default modifier.
 - required: it indicates that the field is required. In proto2, primary key fields must be declared with `required`.
 - optional: it indicates that the field is optional. You can set a default value for an optional field.
 - repeated: it indicates that the field can contain 0–N elements. Its characteristics are the same as those of `optional`, but it can contain multiple values at a time, which can be considered as an array. The special definition of `[packed = true]` must be specified.

- **Field type**
TcaplusDB supports general fields and nested fields.

- **Field name**
You can name a field based on its current attribute. The name can contain letters, digits, and underscores and cannot start with a digit. You are recommended to use camelCase for the name.

- **Identifier**
Identifier value range: [1,2^29 - 1]
Identifiers within [19000,19999] cannot be used, as they are reserved in Protocol Buffers. If you use any of them, an error will be reported.
Each field will occupy memory when being encoded, and the occupied memory size is subject to the identifier:
 - A field with an identifier within [1,15] occupies 1 byte during encoding.
 - A field with an identifier within [16,2047] occupies 2 bytes during encoding.

- **Special definition**
 - If the `packed=true` option needs to be specified for a field declared with the `repeated` modifier, the syntax will be as follows:
```
repeated int64 lockid = 6 [packed = true]; 
```
 - You can use `default = 1` to specify the default value for a field declared with the `optional` modifier. The syntax is as follows:
```
optional int32 logintime = 5 [default = 1];
```
 - You can specify the fields in `string` and `bytes` types as encrypted fields. The syntax is as follows:
```
required string name = 2[(tcaplusservice.tcaplus_crypto) = true];
```

### Nested type information
TcaplusDB supports nested types. A nested type can contain another one as its field. You can also define a new nested type in another one.
Similar to table definition, nested type definition is also declared with a message, but the nested type structure cannot contain definition of extended information such as "primary key" and "index".

TcaplusDB supports up to 128 levels of consecutive nesting; however, you are not recommended to use a high number of nesting levels, as it will compromise the data access performance.
