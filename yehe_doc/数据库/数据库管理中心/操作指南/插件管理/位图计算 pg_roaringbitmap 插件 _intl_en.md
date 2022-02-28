
TencentDB for PostgreSQL provides the `pg_roaringbitmap` extension to use the bitwise operation feature to improve the query performance.

## Prerequisites
Your TencentDB for PostgreSQL instance is on v10, 11, 12, or 13.

## Background
The roaring bitmap algorithm divides a 32-bit INT value into 216 data chunks, each of which corresponds to the higher 16 bits of an integer and uses a container to store the lower 16 bits.
Roaring bitmap stores the containers in a dynamic array as a level-1 index. Containers are in two different structures: array container for sparse chunks and bitmap container for dense chunks. If a container has less than 4,096 integers, the values are stored in an array container; otherwise, the values are stored in a bitmap container.
By using this storage structure, roaring bitmap can quickly search for a specific value. During bitwise operations (AND, OR, and XOR), roaring bitmap provides the corresponding algorithms to efficiently implement operations between two containers, making it powerful in both storage and computing performance.

## Directions
1. Run the following command to create an extension:
```
CREATE EXTENSION roaringbitmap;
```
2. Run the following command to create a table with data of `roaringbitmap` type:
```
CREATE TABLE t1 (id integer, bitmap roaringbitmap);
```
3. Run the following command to use the `rb_build` function to insert the `roaringbitmap` data:
```
-- Set the bit value of the array to 1.
INSERT INTO t1 SELECT 1,RB_BUILD(ARRAY[1,2,3,4,5,6,7,8,9,200]);
-- Set the bit values of multiple records to 1 and aggregate the bit values into a Roaring bitmap.  
INSERT INTO t1 SELECT 2,RB_BUILD_AGG(e) FROM GENERATE_SERIES(1,100) e;
```
4. Run the following command to perform bitwise operations (OR, AND, XOR, and ANDNOT):
```
-- Set the bit value of the array to 1.
SELECT RB_OR(a.bitmap,b.bitmap) FROM (SELECT bitmap FROM t1 WHERE id = 1) AS a,(SELECT bitmap FROM t1 WHERE id = 2) AS b;
```
5. Run the following command to perform aggregated bitwise operations (OR, AND, XOR, and BUILD) to generate a new Roaring bitmap:
```
SELECT RB_OR_AGG(bitmap) FROM t1;
SELECT RB_AND_AGG(bitmap) FROM t1;
SELECT RB_XOR_AGG(bitmap) FROM t1;
SELECT RB_BUILD_AGG(e) FROM GENERATE_SERIES(1,100) e;
```
6. Run the following command to calculate the cardinality, i.e., number of bits set to 1 in the Roaring bitmap:
```
SELECT RB_CARDINALITY(bitmap) FROM t1;
```
7. Run the following command to return the subscripts of the bits set to 1 in the Roaring bitmap:
```
SELECT RB_ITERATE(bitmap) FROM t1 WHERE id = 1;
```

## Feature Function List

| Function | 	Input | Output | Description | Example | Result |
|---------|---------|---------|---------|---------|---------|
| rb_build | integer[] | roaringbitmap | Create roaringbitmap from integer array | ```rb_build('{1,2,3,4,5}')``` | {1,2,3,4,5}|
| rb_index | roaringbitmap,integer | bigint | Return the 0-based index of element in this roaringbitmap, or -1 if do not exsits | ```rb_index('{1,2,3}',3)``` | 2 |
| rb_cardinality | roaringbitmap | bigint | Return cardinality of the roaringbitmap | ```rb_cardinality('{1,2,3,4,5}')``` | 5 |
| rb_and_cardinality | roaringbitmap,roaringbitmap | bigint | Return cardinality of the AND of two roaringbitmaps | ```rb_or_cardinality('{1,2,3}','{3,4,5}')``` | 1 |
| rb_xor_cardinality | roaringbitmap,roaringbitmap | bigint | Return cardinality of the XOR of two roaringbitmaps | ```rb_xor_cardinality('{1,2,3}','{3,4,5}')``` | 4 |
| rb_andnot_cardinality | roaringbitmap,roaringbitmap | bigint | Return cardinality of the ANDNOT of two roaringbitmaps | ```rb_andnot_cardinality('{1,2,3}','{3,4,5}')``` | 2 |
| rb_is_empty | roaringbitmap | boolean | Check if roaringbitmap is empty. | ```rb_is_empty('{1,2,3,4,5}')``` | t |
| rb_fill | roaringbitmap,range_start bigint,range_end bigint | roaringbitmap | Fill the specified range (not include the range_end) | ```rb_fill('{1,2,3}',5,7)``` | {1,2,3,5,6} |
| rb_clear | roaringbitmap,range_start bigint,range_end bigint | roaringbitmap | Clear the specified range (not include the range_end) | ```rb_clear('{1,2,3}',2,3)``` | {1,3} |
| rb_flip | roaringbitmap,range_start bigint,range_end bigint | roaringbitmap | Negative the specified range (not include the range_end) | ```rb_flip('{1,2,3}',2,10)``` | {1,4,5,6,7,8,9} |
| rb_range | roaringbitmap,range_start bigint,range_end bigint | roaringbitmap | Return new set with specified range (not include the range_end) | ```rb_range('{1,2,3}',2,3)``` | {2} |
| rb_range_cardinality | roaringbitmap,range_start bigint,range_end bigint | bigint | Return the cardinality of specified range (not include the range_end) | ```rb_range_cardinality('{1,2,3}',2,3)``` | 1 |
| rb_min | roaringbitmap | integer | Return the smallest offset in roaringbitmap. Return NULL if the bitmap is empty | ```rb_min('{1,2,3}')``` | 1 |
| rb_max | roaringbitmap | integer | Return the greatest offset in roaringbitmap. Return NULL if the bitmap is empty | ```rb_max('{1,2,3}')``` | 3 |
| rb_rank | roaringbitmap,integer | bigint | Return the number of elements that are smaller or equal to the specified offset | ```rb_rank('{1,2,3}',3)``` | 3 |
| rb_jaccard_dist | roaringbitmap,roaringbitmap | double precision | Return the jaccard distance(or the Jaccard similarity coefficient) of two bitmaps | ```rb_jaccard_dist('{1,2,3}','{3,4}')``` | 0.25 |
| rb_select | roaringbitmap,bitset_limit bigint,bitset_offset bigint=0,reverse boolean=false,range_start bigint=0,range_end bigint=4294967296 | roaringbitmap | Return subset [bitset_offset,bitset_offset+bitset_limit) of bitmap between range [range_start,range_end) | ```rb_select('{1,2,3,4,5,6,7,8,9}',5,2)``` | {3,4,5,6,7} |
| rb_to_array | roaringbitmap | integer[] | Convert roaringbitmap to integer array | ```rb_to_array(roaringbitmap('{1,2,3}'))``` | {1,2,3} |
| rb_iterate | roaringbitmap | SET of integer | Return set of integer from a roaringbitmap data. | ```SELECT rb_iterate(rb_build('{1,2,3}'))``` | 1<br>2<br>3 |

## Aggregate Function List
| Aggregate Function | 	Input | Output | Description | Example | Result |
|---------|---------|---------|---------|---------|---------|
| rb_build_agg | 	integer | 	roaringbitmap | Build a roaringbitmap from a integer set | ```select rb_build_agg(id)
    from (values (1),(2),(3)) t(id)``` | {1,2,3} |
| rb_or_agg | roaringbitmap | roaringbitmap | 	AND Aggregate calculations from a roaringbitmap set | ```select rb_or_agg(bitmap) 
    from (values (roaringbitmap('{1,2,3}')),
                 (roaringbitmap('{2,3,4}'))
          ) t(bitmap)``` | {1,2,3,4} |
| rb_and_agg | roaringbitmap | roaringbitmap | 	AND Aggregate calculations from a roaringbitmap set | ```select rb_and_agg(bitmap) 
    from (values (roaringbitmap('{1,2,3}')),
                 (roaringbitmap('{2,3,4}'))
          ) t(bitmap)``` | {2,3} |
| rb_xor_agg | roaringbitmap | roaringbitmap | XOR Aggregate calculations from a roaringbitmap set | ```select rb_xor_agg(bitmap) 
    from (values (roaringbitmap('{1,2,3}')),
                 (roaringbitmap('{2,3,4}'))
          ) t(bitmap)``` | {1,4} |
| rb_or_cardinality_agg | roaringbitmap | bigint | 	OR Aggregate calculations from a roaringbitmap set, return cardinality. | ```select rb_or_cardinality_agg(bitmap) 
    from (values (roaringbitmap('{1,2,3}')),
                 (roaringbitmap('{2,3,4}'))
          ) t(bitmap)``` | 4 |
| rb_and_cardinality_agg | roaringbitmap | bigint | AND Aggregate calculations from a roaringbitmap set, return cardinality | ```select rb_and_cardinality_agg(bitmap) 
    from (values (roaringbitmap('{1,2,3}')),
                 (roaringbitmap('{2,3,4}'))
          ) t(bitmap)``` | 2 |
| rb_xor_cardinality_agg | roaringbitmap | bigint | XOR Aggregate calculations from a roaringbitmap set, return cardinality | ```select rb_xor_cardinality_agg(bitmap) 
    from (values (roaringbitmap('{1,2,3}')),
                 (roaringbitmap('{2,3,4}'))
          ) t(bitmap)``` | 2 |


