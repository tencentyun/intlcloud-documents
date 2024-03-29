数据库有丰富的本地数据类型集供用户使用。用户还可以使用 CREATE TYPE 命令定义新的数据类型。该引用显示所有的内置数据类型。

|          名称         | 别名          | 尺寸             | 范围                        |               描述                    |
| ------------------ | ------------- | ---------------- | ------------------------ | --------------------------------- |
|   bigint      | int8      | 8bytes      |[-9223372036854775808，9223372036854775807]       |  大范围整数      |
|    bigserial       | serial8       | 8bytes        | [1，9223372036854775807]                       |    大的自动增量整数    |
|     bit [ (n)]        |      -         | *n* bits         | [bit string constant]     |       固定长度位串         |
|  bit varying [ (n) ]       | varbit      | actual   number of bits    | [bit   string constant]      |    可变长度位串             |
|    boolean          | bool      | 1byte          | true/false,   t/f, yes/no, y/n, 1/0              |    逻辑布尔（true / false）|
|   box             |        -      | 32bytes         | ((x1,y1),(x2,y2))          |   平面中的矩形框，分配键列中不允许  |
|  bytea        |   -     | 1 byte + *binary string* | sequence   of [octets]    | 可变长度二进制字符串        |
|   character [ (n) ]    | char   [ (n) ]       | 1byte + *n*             | strings up to *n* characters in length         |  定长的空白填充    |
|   character  varying [ (n)]   | varchar   [ (n) ]    | 1byte + *string size*   | strings up to *n* characters in length   |   受限的可变长度        |
|    cidr   |       -     | 12 - 24bytes           |           -          |    IPv4 和 IPv6 网络     |
|   circle    |    -   | 24bytes       | <(x,y),r>   (center and radius)      |           平面的圆，不允许在分配键列中            |
| date   |     -      | 4bytes                  | [4713 BC，294,277 AD]         |                日历日期（年，月，日）                |
| decimal [ (p, s)]     | numeric   [ (p, s) ] | variable      | no   limit           |        用户指定的精度，精确                 |
| double   precision    | float8   float       | 8bytes      | 15   decimal digits precision        |     可变精度，不精确                   |
|  inet         |               -       | 12  or 24 bytes           |       -       | IPv4 或 IPv6 网络地址               |
|  integer    | int,   int4          | 4 bytes     | [-2147483648，+2147483647]      |    通常选择整数类型                   |
|  interval   [ (p) ]             |     -    | 12 bytes                 | [-178000000 years，178000000 years]     |      时间跨度             |
|   json    |        -    | 1 byte + json size       | json   of any length    |                  不受限制的可变长度     |
|  lseg     |       -               | 32 bytes                 | ((x1,y1),(x2,y2))                                |          平面中的线段，分配键列中不允许     |
|  macaddr    |      -   | 6 bytes                  |    -           |    MAC 地址                      |
|  money        |          -       | 8 bytes                  | [-92233720368547758.08，+92233720368547758.07] |      货币金额                       |
| path        |       -     | 16+16n  bytes             | [(x1,y1),...]     |       平面上的几何路径，分布关键列中不允许        |
|  point     |          -    | 16 bytes                 | (x,y)           |        平面上的几何点，分布关键列中不允许        |
| polygon    |            -          | 40+16n  bytes             | ((x1,y1),...)            |    在平面中封闭的几何路径，分配关键列中不允许     |
| real    | float4      | 4 bytes        | 6   decimal digits precision     |  可变精度，不准确                   |
|   serial      | serial4       | 4 bytes       | [1，2147483647]             |     自动增量整数                     |
| smallint     | int2     | 2 bytes     | [-32768，+32767]            |    小范围整数                      |
|   text[1]     | -       | 1 byte + *string size*   | strings   of any length      |          变量无限长                      |
|   time   [ (p) ] [ without time zone ]    |   -    | 8 bytes    | [00:00:00[.000000]，24:00:00[.000000]]          |   时间只有一天                     |
|       time   [ (p) ] with time zone       | timetz   | 12bytes    | [00:00:00+1359，24:00:00-1359]      |    时间只有一天，带时区                 |
| timestamp   [ (p) ] [ without time zone ] |     -  | 8 bytes    | [4713  BC，294,277 AD]        |       日期和时间                      |
|    timestamp   [ (p) ] with time zone     | timestamptz          | 8 bytes      | [4713  BC，294,277 AD]       |  日期和时间，带时区                  |
|   uuid        |    -   | 32 bytes     |        -            | 根据 RFC 4122，ISO / IEC 9834-8：2005的通用唯一标识符 |
|    xml[1]      |   -          | 1 byte + *xml size*      | xml   of any length       |     变量无限长                      |
|    txid_snapshot       |    -     |           -        |     -    |     用户级事务 ID 快照                   |


