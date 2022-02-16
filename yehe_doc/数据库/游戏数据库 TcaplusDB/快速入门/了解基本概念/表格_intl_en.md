## Table Overview
Like in other databases, a table in TcaplusDB is a data set as a combination of business data stored based on the table definition.
From the perspective of gaming business, a table can manage a set of correlated data of a business module such as user table and item table.

For example, the player table below can store the information of all players in a game such as game character name, gender, race, level, strength, gears, mount, and items.
```
{
player_id:11474,
player_name: "Test account 2",
gender:0,
ethnicity:"Elf",
FightingPower:10,
equipment:
	{
		helmet:0,
		Warframe:0,
		gloves:0,
		necklace:0,
		pants:0,
		Shoes:0
	},
horse:"0"
}，
{
player_id:11475,
player_name: "Test account 1",
gender:1,
ethnicity:"Orc",
FightingPower:1477,
equipment:
	{
		helmet:1478,
		Warframe:21,
		gloves:554,
		necklace:12,
		pants:64,
		Shoes:122
	},
horse:"3"
}
```


### Record
A record is a set of field values of the same object. In the sample player character table above, all information of a player character consists of multiple attribute field values, which together represent the set of the player's character information in the game. A record can contain up to 1 MB data.

### Field
A field describes an attribute of a specified object. In the sample player character table above, an independent attribute of a player character is called a field, such as `player_name` and `ethnicity`.

#### Primary key field
As can be found from the sample table above, each record has a field that marks its uniqueness. This field is called primary key field. In the player character table above, the primary key fields are `player_id` and `player_name`. TcaplusDB supports up to 4 primary key fields.

#### General field
In addition to the fields marking the record uniqueness, each record also has other attributes called general fields. In the sample player character table above, the general fields include `equipment` and `FightingPower`. TcaplusDB supports up to 128 general fields.

#### Sharding field
TcaplusDB is a distributed database system that can provide higher concurrent request capability for tables. If you set a sharding field, TcaplusDB will calculate its hash value to automatically adjust the table shards based on the current table access conditions; otherwise, the system will use a primary key field as the sharding field.

The setting of the sharding field is subject to the backend data distribution. You need to evaluate whether the values of the field used as the sharding field are discrete. You are not recommended to set a field with limited values such as gender and weekday as the sharding field; instead, you are recommended to use fields such as ID and name.

#### Field type
TcaplusDB supports multiple data types as detailed below:

| Field Type | Description |
|----------|--------------|
| int32 | Variable-length signed integer that can represent a value between \-2^31 and \+2^31. It is relatively inefficient to represent a negative number. |
| int64 | Variable-length signed integer that can represent a value between \-2^63 and \+2^63. |
| uint32 | Variable-length unsigned integer that can represent a value between 0 and 2^32. |
| uint64 | Variable-length unsigned integer that can represent a value between 0 and 2^64. |
| sint32 | Variable-length signed `int` value which is more efficient to represent a negative number than regular `int32`. |
| sint64 | Variable-length signed `int` value which is more efficient to represent a negative number than regular `int64`. |
| bool | Boolean value representing `True` or `False`. |
| fixed32 | Fixed-length numeric type always taking 4 bytes. It is more efficient than `uint32` if the value is generally above 2^28. |
| fixed64 | Fixed-length numeric type always taking 8 bytes. It is more efficient than `uint64` if the value is generally above 2^56. |
| sfixed32 | Fixed-length numeric type always taking 4 bytes. |
| sfixed64 | Fixed-length numeric type always taking 8 bytes. |
| float | 32-bit binary floating point taking 4 bytes. |
| double | 64-bit binary double-precision floating point taking 8 bytes. |
| strings | String encoded with UTF\-8 or 7-bit ASCII that cannot exceed 2^32 in length. |
| bytes | Byte sequence of a length below 2^32. |
| message | Nested type. It supports up to 128 consecutive nesting levels. A high number of nesting levels will affect the performance. |

### Table definition format
TcaplusDB supports Protocol Buffers, which is a lightweight and efficient structured data storage format and mainly used to store structured data sequentially.
For more information on the table formats, please see [Table Description Language](https://intl.cloud.tencent.com/document/product/1016/36559).
