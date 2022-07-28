This document describes how to select a storage format in CDWPG.

## Storage Format Overview
Greenplum (GP) stores data in heap or AO (AORO or AOCO) tables:
- Heap table: It is inherited from PostgreSQL and is currently the default storage format of GP. It only supports row-oriented storage.
- AO table: AO table was originally designed to only support `APPEND` (i.e., `INSERT`), so it was called append-only. It has been optimized since v4.3 and now supports `UPDATE` and `DELETE`, so it has been renamed append-optimized. AO supports both row-oriented (AORO) and column-oriented (AOCO) storage.

## Heap Table
Heap table is inherited from PostgreSQL and uses MVCC for consistency. If you don't specify any storage format when creating a table, GP will use the heap table format.
A heap table supports partitioned table and row storage but not column storage or compression. It should be noted that when processing `UPDATE` and `DELETE` operations, the heap table does not actually delete data; instead, it relies on version information to block old data. Therefore, if your table has a large number of `UPDATE` or `DELETE` operations, the physical space used by the table will keep increasing. In this case, you need to use `VACUUM` to clear old data.
A heap tables doesn't support logical incremental backup, so if you want to take a snapshot of the heap table, you need to export the full data each time.

Table creation statement:
```
CREATE TABLE heap(
	a int,
	b varchar(32)
) DISTRIBUTED BY (a);
```

### Best practices
- For small tables such as dimension tables in the data warehouse or those containing fewer than one million data records, heap tables are recommended.
- In OLTP scenarios where many `UPDATE` and `DELETE` operations exist and queries are mostly point queries with indexes, heap tables are recommended.

## AO Table
AO table is designed to be used as large fact table in the data warehouse. It supports row storage (not recommended), column storage, and data compression.
An AO table is very different from a heap table in both the logical and physical table structures. For example, the heap table mentioned above uses MVCC to control the visibility of data after `UPDATE` and `DELETE` operations, while the AO table uses an additional bitmap table to indicate what data is visible in the AO table.
For an AO table with a large number of `UPDATE` and `DELETE` operations, you also need to use `VACUUM` for maintenance. However, in the AO table, `VACUUM` needs to reset the bitmap and compress the physical file, so it is usually slower than in a heap table.

### AOCO
An AOCO table organizes data in columns and supports column-level compression.
The table creation statement is as follows, with the partitioning feature added:
```
CREATE TABLE aoco(
	a int  ENCODING (compresstype=zlib, compresslevel=5),
	b int  ENCODING (compresstype=none),
	c varchar(32) ENCODING (compresstype=RLE_TYPE, blocksize=32768),
	d varchar(32),
	fdate date
)
WITH (appendonly=true, orientation=column, compresstype=zlib, compresslevel=6, blocksize=65536)
DISTRIBUTED BY (a)
PARTITION BY RANGE(fdate) 
(
	PARTITION pn START ('2018-11-01'::date) END ('2018-11-10'::date) EVERY ('1 day'::interval),
	DEFAULT PARTITION pdefault
);
```

### Compression
Compression is mainly used for column-oriented tables or append-write (`appendonly=true`) row-oriented tables. The following two types of compression are available:
- Table-level compression.
- Column-level compression, where you can apply different compression algorithms to different columns.

Currently, CDWPG supports zstd, zlib, and rle_type compression algorithms.

Examples:
Create a column-oriented table using level-5 zlib compression:
```
CREATE TABLE foo (a int, b text) 
   WITH (appendonly=true, orientation=column, compresstype=zlib, compresslevel=5);
```

Create a column-oriented table using level-5 zstd compression:
```
CREATE TABLE foo (a int, b text) 
   WITH (appendonly=true, orientation=column, compresstype=zstd, compresslevel=5);
```

### Best practices
- AOCO is typically used for fact tables in the data warehouse. Such tables have many fields and large data volumes and are mainly used in OLAP scenarios, where only some fields in the tables are read and aggregated when queried, with no `SELECT \* FROM` involved.
- As AOCO is generally used for large tables, compression and partitioning are often used together to reduce the actual storage capacity and improve the performance.
- In general, you can select the zlib compression algorithm at level 4 or 5; however, be sure to use the rle_type algorithm for fields with many repeated values.
- Do not make the blocksize too large, especially for partitioned tables. GP maintains a buffer for each field in each partition, so if the blocksize is too large, the memory usage will be very high. The default value of 32768 is suitable in most cases.

