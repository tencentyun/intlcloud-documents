This document describes how to accelerate the import of massive amounts of data to a database with the TXRocks engine.

## Background
- **Scenario**: The import of massive amounts of data to a database with the TXRocks engine needs to be accelerated.
- **Impact**: The `Rows inserted during bulk load must not overlap existing rows` error may be reported when massive amounts of data are imported.

## Option 1
1. Delete secondary indexes and retain only the primary key index.
2. Adjust memory parameters based on the specification and data volume.
>?Appropriately increase the values of `rocksdb_merge_buf_size` and `rocksdb_merge_combine_read_size` parameters based on the specification and data volume.
>
 - `rocksdb_merge_buf_size` indicates the data volume of each way in k-way merge during index creation. `rocksdb_merge_combine_read_size` indicates the total memory used in k-way merge.
 - `rocksdb_block_cache_size` indicates the size of `rocksdb_block_cache`. We recommend you decrease its value temporarily during k-way merge.
3. Use `bulk load` to import the data.
```
SET session rocksdb_bulk_load_allow_unsorted=1;
SET session rocksdb_bulk_load=1;
...
Import the data
...
SET session rocksdb_bulk_load=0;
SET session rocksdb_bulk_load_allow_unsorted=0;
```
>?If the imported data is sorted, you don't need to configure `rocksdb_bulk_load_allow_unsorted`.
4. Recreate secondary indexes one by one after all data is imported.
>!
>- Secondary index creation involves k-way merge. `rocksdb_merge_buf_size` indicates the data volume of each way, and `rocksdb_merge_combine_read_size` indicates the total memory used in k-way merge.
>- For example, we recommend you set `rocksdb_merge_buf_size` to 64 MB or higher and set `rocksdb_merge_combine_read_size` to 1 GB or higher to avoid OOM. After all data is imported, you must modify the parameters to their original values.
>- As a lot of memory is used during the creation of each secondary index, we recommend you not create many of them at the same time.

## Option 2
You can disable `unique_check` during data import to improve the import performance.
```
SET unique_checks=OFF;
...
Import the data.
...
SET unique_checks=ON;
```
>!After the operation is completed, you must set `unique_checks` back to `ON`; otherwise, the uniqueness of INSERT operations in subsequent normal transaction writes will not be checked.
