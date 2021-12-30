TencentDB for TcaplusDB supports Protocol Buffers data types.

## Mapping between proto3 and Data Types in Other Programing Languages

| .proto | C++ | Java | Python | Go | Ruby | C\# | PHP| Dart | Notes |    
| ------------ | ---------- | ---------- | ----------- | -------- | ---------------- | ---------- | -------------- | --------- | ----------- |
| double       | double     | double     | float       | float64  | float    | double     | float          | double    |     -     |
| float        | float      | float      | float       | float32  | float               | float      | float          | double    |  -  |
| int32        | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(as required) | int        | integer        | int       | Uses variable-length encoding.<br>Inefficient for encoding negative numbers. If your field is likely to have negative values, use sint32 instead. |
| int64        | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Uses variable-length encoding.<br>Inefficient for encoding negative numbers. If your field is likely to have negative values, use sint64 instead. |
| uint32       | uint32     | int        | int/long    | uint32   | fixnum/<br>bignum<br>(as required) | uint       | integer        | int       | Uses variable-length encoding.                                           |
| uint64       | uint64     | long       | int/long    | uint64   | bignum                        | ulong      | integer/<br>string | Int64     | Uses variable-length encoding.                                           |
| sint32       | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(as required)| int        | integer        | int       | Uses variable-length encoding.                                           |
| sint64       | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Uses variable-length encoding.<br>Signed int value. These more efficiently encode negative numbers than regular int32s. |
| fixed32      | uint32     | int        | int/long    | uint32   | fixnum/<br>bignum<br>(as required)| uint       | integer        | int       | Always four bytes.<br>More efficient than uint32 if values are generally greater than 2^28.     |
| fixed64      | uint64     | long       | int/long    | uint64   | bignum                        | ulong      | integer/<br>string | Int64     | Always eight bytes.<br>More efficient than uint64 if values are generally greater than 2^56.      |
| sfixed32     | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(as required)| int        | integer        | int       | Always four bytes.                                             |
| sfixed64     | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Always eight bytes.                                             |
| bool         | bool       | boolean    | bool        | bool     | trueClass/<br>falseClass          | bool       | boolean        | bool      |           -             |
| string       | string     | String     | str/unicode | string   | string<br>(UTF -8)            | string     | string      | string    | A string must always contain UTF-8 encoded or 7-bit ASCII text, and cannot be longer than 2^32. |
| bytes        | string     | ByteString | str         | byte | string<br>(ASCII-8BIT)        | bytestring | string      |  -         | May contain any arbitrary sequence of bytes no longer than 2^32.                          |


## Mapping between proto2 and Data Types in Other Programing Languages

| .proto | C++ | Java  | Python               | Go   | Notes                       |
| ------------ | ---------- | ---------- | ---------------- | --------- | ---------------------------------- |
| double       | double     | double     | float                                    | \*float64 |   -            |
| float        | float      | float      | float                                    | \*float32 |                -    |
| int32        | int32      | int        | int                                      | \*int32   | Uses variable-length encoding. Inefficient for encoding negative numbers. If your field is likely to have negative values, use sint32 instead. |
| int64        | int64      | long       | int/long                                 | \*int64   | Uses variable-length encoding. Inefficient for encoding negative numbers. If your field is likely to have negative values, use sint64 instead. |
| uint32       | uint32     | int        | int/long                                 | \*uint32  | Uses variable-length encoding.                                           |
| uint64       | uint64     | long       | int/long                                 | \*uint64  | Uses variable-length encoding.                                           |
| sint32       | int32      | int        | int                                      | \*int32   | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. |
| sint64       | int64      | long       | int/long                                 | \*int64   | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. |
| fixed32      | uint32     | int        | int/long                                 | \*uint32  | Always four bytes. More efficient than uint32 if values are generally greater than 2^28.      |
| fixed64      | uint64     | long       | int/long                                 | \*uint64  | Always eight bytes. More efficient than uint64 if values are generally greater than 2^56.      |
| sfixed32     | int32      | int        | int                                      | \*int32   | Always four bytes.                                             |
| sfixed64     | int64      | long       | int/long                                 | \*int64   | Always eight bytes.                                             |
| bool         | bool       | boolean    | bool                                     | \*bool    |   -                        |
| string       | string     | String     | unicode(Python 2)<br>or<br>str(Python 3) | \*string  | A string must always contain UTF-8 encoded or 7-bit ASCII text.                 |
| bytes        | string     | ByteString | bytes                                    | byte  | May contain any arbitrary sequence of bytes.                                       |

