The database has a rich set of native data types available to users. You may also define new data types by using the `CREATE TYPE` command. This reference shows all of the built-in data types.

|          Name         | Alias          | Size             | Range                        |               Description                    |
| ------------------ | ------------- | ---------------- | ------------------------ | --------------------------------- |
|   bigint      | int8      | 8 bytes      |[-9223372036854775808, 9223372036854775807]       |  Large range integer      |
|    bigserial       | serial8       | 8 bytes        | [1, 9223372036854775807]                       |    Large autoincrementing  integer    |
|     bit [ (n)]        |      -         | *n* bits         | [bit string constant]     |       Fixed-length bit string         |
|  bit varying [ (n) ]       | varbit      | actual number of bits    | [bit string constant]      |    Variable-length bit string             |
|    boolean          | bool      | 1 byte          | true/false,   t/f, yes/no, y/n, 1/0              |    Logic boolean (true/false) |
|   box             |        -      | 32 bytes         | ((x1,y1),(x2,y2))          |   Rectangular box in the plane - not allowed in distribution key columns.  |
|  bytea        |   -     | 1 byte + *binary string* | sequence of [octets]    | Variable-length binary string        |
|   character [ (n) ]    | char   [ (n) ]       | 1 byte + *n*             | strings up to *n* characters in length         |  Fixed-length, blank padded    |
|   character  varying [ (n)]   | varchar   [ (n) ]    | 1 byte + *string size*   | strings up to *n* characters in length   |   Variable-length with limit        |
|    cidr   |       -     | 12–24 bytes           |           -          |    IPv4 and IPv6 networks     |
|   circle    |    -   | 24 bytes       | <(x,y),r>   (center and radius)      |           Circle in the plane - not allowed in distribution key columns            |
| date   |     -      | 4 bytes                  | [4713 BC, 294,277 AD]         |                Calendar date (year, month, day)                |
| decimal [ (p, s)]     | numeric   [ (p, s) ] | variable      | no limit           |        User-specified precision, exact                 |
| double   precision    | float8   float       | 8 bytes      | 15 decimal digits precision        |     Variable-precision, inexact                   |
|  inet         |               -       | 12 or 24 bytes           |       -       | IPv4 and IPv6 hosts and networks               |
|  integer    | int,   int4          | 4 bytes     | [-2147483648, +2147483647]      |    Usual choice for integer                   |
|  interval   [ (p) ]             |     -    | 12 bytes                 | [-178000000 years, 178000000 years]     |      Time span             |
|   json    |        -    | 1 byte + json size       | json of any length    |                  Variable unlimited length    |
|  lseg     |       -               | 32 bytes                 | ((x1,y1),(x2,y2))                                |          Line segment in the plane - not allowed in distribution key columns     |
|  macaddr    |      -   | 6 bytes                  |    -           |    MAC address                      |
|  money        |          -       | 8 bytes                  | [-92233720368547758.08, +92233720368547758.07] |      Currency amount                       |
| path        |       -     | 16+16n bytes             | [(x1,y1),...]     |       Geometric path in the plane - not allowed in distribution key columns        |
|  point     |          -    | 16 bytes                 | (x,y)           |        Geometric point in the plane - not allowed in distribution key columns        |
| polygon    |            -          | 40+16n bytes             | ((x1,y1),...)            |    Closed geometric path in the plane - not allowed in distribution key columns     |
| real    | float4      | 4 bytes        | 6 decimal digits precision     |  Variable-precision, inexact                   |
|   serial      | serial4       | 4 bytes       | [1, 2147483647]             |     Autoincrementing integer                     |
| smallint     | int2     | 2 bytes     | [-32768, +32767]            |    Small range integer                      |
|   text[1]     | -       | 1 byte + *string size*   | strings of any length      |          Variable unlimited length                      |
|   time   [ (p) ] [ without time zone ]    |   -    | 8 bytes    | [00:00:00[.000000], 24:00:00[.000000]]          |   Time of day only                     |
|       time   [ (p) ] with time zone       | timetz   | 12 bytes    | [00:00:00+1359, 24:00:00-1359]      |    Time of day only, with time zone                 |
| timestamp   [ (p) ] [ without time zone ] |     -  | 8 bytes    | [4713 BC, 294,277 AD]        |       Both date and time                      |
|    timestamp   [ (p) ] with time zone     | timestamptz          | 8 bytes      | [4713 BC, 294,277 AD]       |  Both date and time, with time zone                  |
|   uuid        |    -   | 32 bytes     |        -            | Universally unique identifier according to RFC 4122, ISO/IEC 9834-8:2005 |
|    xml[1]      |   -          | 1 byte + *xml size*      | xml of any length       |     Variable unlimited length                      |
|    txid_snapshot       |    -     |           -        |     -    |     User-level transaction ID snapshot                   |


