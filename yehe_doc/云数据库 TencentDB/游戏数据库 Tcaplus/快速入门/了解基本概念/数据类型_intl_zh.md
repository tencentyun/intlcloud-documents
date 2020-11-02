TcaplusDB 支持的Proto Buffers数据类型

### proto3数据类型与编程语言类型映射
参考链接：https://developers.google.com/protocol-buffers/docs/proto3

| \.proto 类型 | C\+\+ 类型 | Java 类型    | Python 类型   | Go 类型    | Ruby 类型                  | C\# 类型     | PHP 类型         | Dart 类型 | 描述                                         |
|------------|----------|------------|-------------|----------|--------------------------|------------|----------------|---------|--------------------------------------------|
| double     | double   | double     | float       | float64  | Float                    | double     | float          | double  |                                            |
| float      | float    | float      | float       | float32  | Float                    | float      | float          | double  |                                            |
| int32      | int32    | int        | int         | int32    | Fixnum 或 Bignum \(根据需要\) | int        | integer        | int     | 使用可变长度编码。 负数编码效率低下–如果您的字段可能具有负值，请改用sint32。 |
| int64      | int64    | long       | int/long    | int64    | Bignum                   | long       | integer/string | Int64   | 使用可变长度编码。 负数编码效率低下–如果您的字段可能具有负值，请改用sint64。 |
| uint32     | uint32   | int        | int/long    | uint32   | Fixnum 或 Bignum \(根据需要\) | uint       | integer        | int     | 使用可变长度编码。                                  |
| uint64     | uint64   | long       | int/long    | uint64   | Bignum                   | ulong      | integer/string | Int64   | 使用可变长度编码。                                  |
| sint32     | int32    | int        | int         | int32    | Fixnum 或 Bignum \(根据需要\) | int        | integer        | int     | 使用可变长度编码。                                  |
| sint64     | int64    | long       | int/long    | int64    | Bignum                   | long       | integer/string | Int64   | 使用可变长度编码。 有符号的int值。 与常规int32相比，它们更有效地编码负数。 |
| fixed32    | uint32   | int        | int/long    | uint32   | Fixnum 或 Bignum \(根据需要\) | uint       | integer        | int     | 始终为四个字节。 如果值通常大于2^28^，则比uint32更有效。         |
| fixed64    | uint64   | long       | int/long    | uint64   | Bignum                   | ulong      | integer/string | Int64   | 始终为八个字节。如果值通常大于2^56^，则比uint64更有效。          |
| sfixed32   | int32    | int        | int         | int32    | Fixnum 或 Bignum \(根据需要\) | int        | integer        | int     | 始终为四个字节。                                   |
| sfixed64   | int64    | long       | int/long    | int64    | Bignum                   | long       | integer/string | Int64   | 始终为八个字节。                                   |
| bool       | bool     | boolean    | bool        | bool     | TrueClass/FalseClass     | bool       | boolean        | bool    |                                            |
| string     | string   | String     | str/unicode | string   | String \(UTF\-8\)        | string     | string         | String  | 字符串必须始终包含UTF\-8编码或7位ASCII文本，并且不能超过2^32^。   |
| bytes      | string   | ByteString | str         | \[\]byte | String \(ASCII\-8BIT\)   | ByteString | string         |         | 可以包含不超过2^32^个任意字节序列。                       |


### proto2数据类型与编程语言类型映射
参考链接：https://developers.google.com/protocol-buffers/docs/proto

| \.proto 类型 | C\+\+ 类型 | Java 类型    | Python 类型                               | Go 类型     | 描述                                        |
|------------|----------|------------|-----------------------------------------|-----------|-------------------------------------------|
| double     | double   | double     | float                                   | \*float64 |                                           |
| float      | float    | float      | float                                   | \*float32 |                                           |
| int32      | int32    | int        | int                                     | \*int32   | 使用可变长度编码。负数编码效率低下–如果您的字段可能具有负值，请改用sint32。 |
| int64      | int64    | long       | int/long                                | \*int64   | 使用可变长度编码。负数编码效率低下–如果您的字段可能具有负值，请改用sint64。 |
| uint32     | uint32   | int        | int/long                                | \*uint32  | 使用可变长度编码。                                 |
| uint64     | uint64   | long       | int/long                                | \*uint64  | 使用可变长度编码。                                 |
| sint32     | int32    | int        | int                                     | \*int32   | 使用可变长度编码。有符号的int值。与常规int32相比，它们更有效地编码负数。  |
| sint64     | int64    | long       | int/long                                | \*int64   | 使用可变长度编码。有符号的int值。与常规int64相比，它们更有效地编码负数。  |
| fixed32    | uint32   | int        | int/long                                | \*uint32  | 始终为四个字节。如果值通常大于2^28^，则比uint32更有效。         |
| fixed64    | uint64   | long       | int/long                                | \*uint64  | 始终为八个字节。如果值通常大于2^56^，则比uint64更有效。         |
| sfixed32   | int32    | int        | int                                     | \*int32   | 始终为四个字节。                                  |
| sfixed64   | int64    | long       | int/long                                | \*int64   | 始终为八个字节。                                  |
| bool       | bool     | boolean    | bool                                    | \*bool    |
| string     | string   | String     | unicode \(Python 2\) 或 str \(Python 3\) | \*string  | 字符串必须始终包含UTF\-8编码或7位ASCII文本。              |
| bytes      | string   | ByteString | bytes                                   | \[\]byte  | 可以包含任意字节序列。                               |


