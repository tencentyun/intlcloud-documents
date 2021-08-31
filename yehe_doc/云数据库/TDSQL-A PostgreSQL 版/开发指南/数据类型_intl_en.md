## Numeric Types
Numeric types consist of two-, four-, and eight-byte integers, four- and eight-byte floating-point numbers, and selectable-precision decimals. TDSQL-A for PostgreSQL columnar tables support the following data types:

| **Name**         | **Storage Size** | **Description**           | **Range**                                     |
| ---------------- | ------------ | ------------------ | -------------------------------------------- |
| smallint         | 2 bytes        | Small-Range integer          | -32768 to +32767                               |
| integer          | 4 bytes        | Typical choice for integer      | -2147483648 to +2147483647                     |
| bigint           | 8 bytes        | Large-Range integer          | -9223372036854775808 to +9223372036854775807   |
| decimal          | Variable         | User-Specified precision, exact  | Up to 131072 digits before the decimal point; up to 16383 digits after the decimal point      |
| numeric          | Variable         | User-Specified precision, exact | Up to 131072 digits before the decimal point; up to 16383 digits after the decimal point      |
| real             | 4 bytes        | Variable-Precision, inexact    | 6 decimal digits precision                                |
| double precision | 8 bytes        | Variable-Precision, inexact   | 15 decimal digits precision                               |
| smallserial      | 2 bytes        | Small autoincrementing integer    | 1 to 32767                                       |
| serial           | 4 bytes        | Autoincrementing integer      | 1 to 2147483647                                |
| bigserial        | 8 bytes        | large autoincrementing integer    | 1 to 9223372036854775807                       |

## Monetary Type
The `money` type stores a currency amount with a fixed fractional precision:

| **Name** | **Storage Size** | **Description** | **Range**                                     |
| -------- | ------------ | -------- | -------------------------------------------- |
| money    | 8 bytes        | Currency amount   | -92233720368547758.08 to +92233720368547758.07 |

## Character Types
TDSQL-A for PostgreSQL columnar tables support the following character types:
- `character varying(n)` and `character(n)`, where `n` is a positive integer. Both of these types can store strings up to n characters (not bytes) in length.
- `text`, which stores strings of any length.
- `name`, which exists only for the storage of identifiers in the internal system catalogs and is not intended for use by the general user. Its length is currently defined as 64 bytes (63 usable characters plus terminator) but should be referenced by using the constant `NAMEDATALEN` in C source code. The length is set at compile time (and is therefore adjustable for special uses); the default maximum length might change in a future release.
- `"char"` (note the quotes) is different from `char(1)` in that it only uses one byte of storage. It is internally used in the system catalogs as a simplistic enumeration type.

| **Name**                          | **Description**                     |
| --------------------------------- | ---------------------------- |
| character  varying(n), varchar(n) | Variable-Length with limit                   |
| character(n), char(n)             | Fixed-Length, blank padded                 |
| text                              | 1 GB                          |
| "char"                            | 1 byte; single-byte internal type        |
| numeric                           | 64 bytes; internal type for object names |

## Binary Data Type
The `bytea` data type allows the storage of binary strings:

| **Name** | **Storage Size**               | **Description**     |
| -------- | -------------------------- | ------------ |
| bytea    | 1 or 4 bytes plus the actual binary string | Variable-Length binary string |

## Date/Time Types
TDSQL-A for PostgreSQL supports the full set of SQL date and time types.

| **Name**                         | **Storage Size** | **Description**                     | **Low Value**    | **High Value**    | **Resolution**   |
| -------------------------- | ------------ | --------------------- | ------------- | ------------- | ------------ |
| timestamp [ (p) ] [ without time zone ] | 8 bytes        | Both date and time (no time zone)     | 4713 BC       | 294276 AD     | 1 microsecond/14 bits |
| timestamp [ (p) ] with time zone   | 8 bytes        | Both date and time, with time zone       | 4713 BC       | 294276 AD     | 1 microsecond/14 bits |
| date                                     | 4 bytes        | Date (no time of day)     | 4713 BC       | 5874897 AD    | 1 day          |
| time [ (p) ] [ without time zone ]      | 8 bytes        | Time of day (no date)       | 0:00:00       | 24:00:00      | 1 microsecond/14 bits |
| time [ (p) ] with time zone   | 12 bytes       | Time of day (no date), with time zone | 00:00:00+1459 | 24:00:00-1459 | 1 microsecond/14 bits |
| interval [ fields ] [ (p) ]     | 16 bytes       | Time interval                     | -178000000 years  | 178000000 years   | 1 microsecond/14 bits |

## Boolean Type
TDSQL-A for PostgreSQL provides the standard SQL type boolean. The boolean type can have several states: `true`, `false`, and a third state, `unknown`, which is represented by the SQL null value.

| **Name** | **Storage Size** | **Description**     |
| -------- | ------------ | ------------ |
| boolean  | 1 byte        | State of true or false |

## Geometric Types
Geometric data types represent two-dimensional spatial objects. TDSQL-A for PostgreSQL columnar tables support the following geometric types:

| **Name** | **Storage Size** | **Description**                 | **Representation**                |
| -------- | ------------ | ------------------------ | ----------------------- |
| point    | 16 bytes       | Point on a plane               | (x,y)                   |
| line     | 32 bytes       | Infinite line               | {A,B,C}                 |
| lseg     | 32 bytes       | Finite line segment                 | ((x1,y1),(x2,y2))       |
| box      | 32 bytes       | Rectangular box                   | ((x1,y1),(x2,y2))       |
| path     | 16+16n bytes   | Closed path (similar to polygon) | ((x1,y1),…)             |
| path     | 16+16n bytes   | Open path                 | [(x1,y1),…]             |
| circle   | 24 bytes       | Circle                       | <(x,y),r> (center point and radius) |

## Network Address Types
Network address types are used to store IPv4, IPv6, and MAC addresses. It is better to use these types instead of plain text types to store network addresses, because these types offer input error checking and specialized operators and functions.

| **Name** | **Storage Size** | **Description**              |
| -------- | ------------ | --------------------- |
| cidr     | 7 or 19 bytes    | IPv4 and IPv6 networks        |
| inet     | 7 or 19 bytes    | IPv4 and IPv6 hosts and networks  |
| macaddr  | 6 bytes        | MAC addresses               |
| macaddr8 | 8 bytes        | MAC addresses (EUI-64 format) |

## Bit String Types
Bit strings are strings of 1's and 0's. They can be used to store or visualize bit masks.
There are two SQL bit types: `bit(n)` and `bit varying(n)`, where `n` is a positive integer.
- `bit` type data must match the length *n* exactly; it is an error to attempt to store shorter or longer bit strings.
- `bit varying` data is of variable length up to the maximum length *n*; longer strings will be rejected.
Writing `bit` without a length is equivalent to `bit(1)`, while `bit varying` without a length specification means unlimited length.

Sample code:
```
postgres=# CREATE TABLE bit_test (col1 int,col2 BIT(3), col3 BIT VARYING(5))WITH(ORIENTATION=column);
CREATE TABLE
postgres=# INSERT INTO bit_test VALUES(1,B'101', B'00');
INSERT 0 1
postgres=# INSERT INTO bit_test VALUES(2,B'10'::bit(3), B'101');
INSERT 0 1
postgres=# SELECT * FROM bit_test;
 col1 | col2 | col3 
------+------+------
  1 | 101 | 00
  2 | 100 | 101
(2 rows)
```

## Text Search Types
TDSQL-A for PostgreSQL provides two data types: `tsvector` and `tsquery`, to support full-text search, which is the activity of searching through a collection of natural-language documents to locate those that best match a query.

The `tsvector` type represents a document in a form optimized for text search. A `tsvector` value is a sorted list of distinct lexemes, which are words that have been normalized to merge different variants of the same word. Sorting and duplicate-elimination are done automatically during input.

Sample code:
```
postgres=# SELECT 'a fat cat sat on a mat and ate a fat rat'::tsvector;
           tsvector           
----------------------------------------------------
 'a' 'and' 'ate' 'cat' 'fat' 'mat' 'on' 'rat' 'sat'
(1 row)
postgres=# SELECT $$the lexeme '  ' contains spaces$$::tsvector;
         tsvector         
-------------------------------------------
 '  ' 'contains' 'lexeme' 'spaces' 'the'
(1 row)
```
The `tsquery` type similarly represents a text query. A `tsquery` value stores lexemes that are to be searched for, and can combine them by using the Boolean operators `& (AND)`, `| (OR)`, and `! (NOT)`, as well as the phrase search operator `<-> (FOLLOWED BY)`. There is also a variant `<N>` of the `FOLLOWED BY` operator, where N is an integer constant that specifies the distance between the two lexemes being searched for. `<->` is equivalent to `<1>`.

Parentheses can be used to enforce the grouping of these operators. In the absence of parentheses, `! (NOT)` binds most tightly, `<-> (FOLLOWED BY)` next most tightly, then `& (AND)`, with `| (OR)` binding the least tightly.

Sample code:
```
postgres=# SELECT 'fat & rat'::tsquery;
  tsquery  
---------------
 'fat' & 'rat'
(1 row)
postgres=# SELECT 'fat & (rat | cat)'::tsquery;
     tsquery     
---------------------------
 'fat' & ( 'rat' | 'cat' )
(1 row)
postgres=# SELECT 'fat:ab & cat'::tsquery;
   tsquery   
------------------
 'fat':AB & 'cat'
(1 row)
```

## UUID Type
The `uuid` data type stores Universally Unique Identifier (UUID) as defined by RFC 4122, ISO/IEC 9834-8:2005, and related standards. (Some systems refer to this data type as a globally unique identifier, or GUID, instead.) This identifier is a 128-bit quantity that is generated by an algorithm chosen to make it very unlikely that the same identifier will be generated by anyone else in the known universe by using the same algorithm. Therefore, for distributed systems, these identifiers provide a better uniqueness guarantee than sequence generators, which are only unique within a single database.

A UUID is written as a sequence of lowercase hexadecimal digits, in several groups separated by hyphens, specifically a group of 8 digits followed by three groups of 4 digits followed by a group of 12 digits, for a total of 32 digits representing the 128 bits. An example of a UUID in this standard form is:
```
a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11
```

## XML Type
The `xml` data type can be used to store XML data. Its advantage over storing XML data in a text field is that it checks the input values for well-formedness, and there are support functions to perform type-safe operations on it. Use of this data type requires the installation to have been built with `configure --with-libxml`.

The `xml` type can store well-formed "documents", as defined by the XML standard, as well as "content" fragments, which are defined by the production `XMLDecl? content` in the XML standard. Roughly, this means that content fragments can have more than one top-level element or character node. The expression `xmlvalue IS DOCUMENT` can be used to evaluate whether a particular `xml` value is a full document or only a content fragment.

## JSON Types
JSON data types are for storing JavaScript Object Notation (JSON) data. Such data can also be stored as text, but the JSON data types have the advantage of enforcing that each stored value is valid according to the JSON rules. There are also assorted JSON-specific functions and operators available for data stored in these data types.

There are two JSON data types: `json` and `jsonb`, which accept almost identical sets of values as input. The major practical difference is one of efficiency.
- The `json` data type stores an exact copy of the input text, which processing functions must reparse on each execution.
- `jsonb` data is stored in a decomposed binary format that makes it slightly slower to input due to added conversion overhead, but significantly faster to process, since no reparsing is needed. `jsonb` also supports indexing

Because the `json` type stores an exact copy of the input text, it will preserve semantically-insignificant white space between tokens, as well as the order of keys within JSON objects. Also, if a JSON object within the value contains the same key more than once, all the key/value pairs are kept. (The processing functions consider the last value as the operative one.) By contrast, `jsonb` does not preserve white space, does not preserve the order of object keys, and does not keep duplicate object keys. If duplicate keys are specified in the input, only the last value is kept.
In general, most applications should prefer to store JSON data as `jsonb`, unless there are quite specialized needs, such as legacy assumptions about ordering of object keys.
Sample code:
```
postgres=# SELECT '5'::json;
 json 
------
 5
(1 row)

postgres=# SELECT '[1, 2, "foo", null]'::json;
    json     
---------------------
 [1, 2, "foo", null]
(1 row)

postgres=# SELECT '{"foo": [true, "bar"], "tags": {"a": 1, "b": null}}'::json;
            json             
-----------------------------------------------------
 {"foo": [true, "bar"], "tags": {"a": 1, "b": null}}
(1 row)
postgres=# SELECT '{"foo": {"bar": "baz"}}'::jsonb @> '{"foo": {}}'::jsonb;
 ?column? 
----------
 t
(1 row)

postgres=# SELECT '{"foo": {"bar": "baz"}}'::jsonb @> '{"bar": "baz"}'::jsonb;
 ?column? 
----------
 f
(1 row)
```

## Array Types
TDSQL-A for PostgreSQL allows columns of a table to be defined as variable-length multidimensional arrays. Arrays of any built-in or user-defined base type, enum type, composite type, range type, or domain can be created.
An array data type is named by appending square brackets ([]) to the data type name of the array elements.
Sample code:
```
postgres=# CREATE TABLE sal_emp (
postgres(#   name      text,
postgres(#   pay_by_quarter integer[],
postgres(#   schedule    text[][]
postgres(# )with(orientation=column);
CREATE TABLE
postgres=# INSERT INTO sal_emp
postgres-#   VALUES ('Bill',
postgres(#   '{10000, 10000, 10000, 10000}',
postgres(#   '{{"meeting", "lunch"}, {"training", "presentation"}}');
INSERT 0 1
postgres=# 
postgres=# INSERT INTO sal_emp
postgres-#   VALUES ('Carol',
postgres(#   '{20000, 25000, 25000, 25000}',
postgres(#   '{{"breakfast", "consulting"}, {"meeting", "lunch"}}');
INSERT 0 1
postgres=# SELECT * FROM sal_emp;
 name |   pay_by_quarter    |         schedule         
-------+---------------------------+-------------------------------------------
 Carol | {20000,25000,25000,25000} | {{breakfast,consulting},{meeting,lunch}}
 Bill | {10000,10000,10000,10000} | {{meeting,lunch},{training,presentation}}
(2 rows)
```

An alternative syntax, which conforms to the SQL standard by using the keyword `ARRAY`, can be used for one-dimensional arrays.
The `pay_by_quarter` in the `sal_emp` table in the above sample code could have been defined as:
```
pay_by_quarter integer ARRAY[4],
```
Or, if no array size is to be specified:
```
pay_by_quarter integer ARRAY,
```

## Enumerated Types
Enumerated (enum) types are data types that comprise a static, ordered set of values. They are equivalent to the enum types supported in a number of programming languages. An example of an enum type might be the days of the week or a set of status values for a piece of data.
Enum types are created by using the `CREATE TYPE` command. Once created, the enum type can be used in table and function definitions much like any other type:
Sample code:
```
postgres=# CREATE TYPE mood AS ENUM ('sad', 'ok', 'happy');
CREATE TYPE
postgres=# CREATE TABLE person (
postgres(#   name text,
postgres(#   current_mood mood
postgres(# )WITH(ORIENTATION=column);
CREATE TABLE
postgres=# INSERT INTO person VALUES ('Moe', 'happy');
INSERT 0 1
postgres=# SELECT * FROM person WHERE current_mood = 'happy';
 name | current_mood 
------+--------------
 Moe | happy
(1 row)
```

## Composite Types
A composite type represents the structure of a row or record; it is essentially just a list of field names and their data types.
Sample code:
```
postgres=# CREATE TYPE inventory_item AS (
postgres(#   name      text,
postgres(#   supplier_id   integer,
postgres(#   price      numeric
postgres(# );
CREATE TYPE
postgres=# CREATE TABLE on_hand (
postgres(#   item   inventory_item,
postgres(#   count   integer
postgres(# )WITH(ORIENTATION=column);
CREATE TABLE
postgres=# INSERT INTO on_hand VALUES (ROW('fuzzy dice', 42, 1.99), 1000);
INSERT 0 1
postgres=# SELECT * FROM on_hand;
     item     | count 
------------------------+-------
 ("fuzzy dice",42,1.99) | 1000
(1 row)
```

## Range Types
Range types are data types representing a range of values of some element type (called the range's subtype). For instance, ranges of `timestamp` might be used to represent the ranges of time that a meeting room is reserved. In this case, the data type is `tsrange` (short for "timestamp range"), and `timestamp` is the subtype. The subtype must have a total order so that it is well-defined whether element values are within, before, or after a range of values.

Range types are useful because they represent many element values in a single range value, and because concepts such as overlapping ranges can be expressed clearly. The use of time and date ranges for scheduling purposes is the clearest example; but price ranges, measurement ranges from an instrument, and so forth can also be useful.

TDSQL-A for PostgreSQL columnar tables support the following built-in range types:
- int4range - Range of `integer`
- int8range - Range of `bigint`
- numrange - Range of `numeric`
- tsrange - Range of `timestamp` without time zone
- tstzrange - Range of `timestamp` with time zone
- daterange - Range of `date`

Sample code:
```
postgres=# CREATE TABLE reservation (room int, during tsrange)WITH(ORIENTATION=column);
CREATE TABLE
postgres=# INSERT INTO reservation VALUES
postgres-#   (1108, '[2010-01-01 14:30, 2010-01-01 15:30)');
INSERT 0 1
postgres=# SELECT * FROM reservation;
 room |          during           
------+-----------------------------------------------
 1108 | ["2010-01-01 14:30:00","2010-01-01 15:30:00")
(1 row)
```
