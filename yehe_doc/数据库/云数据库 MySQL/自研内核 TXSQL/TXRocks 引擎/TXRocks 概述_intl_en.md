## TXRocks Overview
TXRocks is a transactional storage engine developed by Tencent's TXSQL team based on RocksDB, a very popular high-performance persistent key-value (KV) store.

## Why TXRocks?
By leveraging the LSM tree storage structure of RocksDB, the TXRocks transactional storage engine not only reduces wastes caused by InnoDB's half-full pages and fragments, but also uses the compact storage format. Therefore, it has a performance comparable to that of InnoDB but requires only a half or even smaller storage space. It is more suitable for businesses with a large data volume and high requirements for the transactional read/write performance.

## RocksDB's LSM Tree Architecture
RocksDB uses the LSM tree storage structure, where data is organized as a set of MemTables in the memory and multi-level SST files on the disk.
For a write request, the new version of the record is first written to an active MemTable, and then WAL is written for data durability. After the MemTable and WAL file are written for the request, a response can be returned.
When the volume of data written into an active MemTable reaches a certain threshold, the MemTable will be switched to a frozen immutable MemTable. The backend thread flushes the immutable MemTable to the disk to generate an SST file. SST files are sorted at L0 to L6 levels in the flush order. At each level, the records of different SST files are sequential and don't overlap. However, to release the memory space occupied by immutable MemTables promptly, such records are allowed to overlap at L0. 

When a record is read, it will be searched for in the active MemTable, immutable MemTable, SST files at L0, and SST files at L1–6 in sequence. Once the record is found in any component, the latest version of the record is found and will be returned immediately.

When a range scan is performed, an iterator will be generated at each level of data containing MemTables. The iterators perform a merge sort to find the next record. As shown in the read process, if the LSM tree has too many levels, the read performance, especially the performance of range scan will drop significantly. Therefore, to maintain a better LSM tree shape, the backend continuously performs compaction operations to merge low-level data to a higher level and thus reduce the number of levels.
![](https://qcloudimg.tencent-cloud.cn/raw/cc38118399e25373a55631ca94f15ec4.png)

## TXRocks Architecture
![](https://qcloudimg.tencent-cloud.cn/raw/b7bd4fb0cc37a7d60c0c29945095c167.png)

## TXRocks Strengths
#### Less storage space
Compared with the B+tree structure used by InnoDB, the LSM tree can save a considerable amount of storage space.
InnoDB's B+tree split often results in half-full pages, idle pages, and space waste; therefore, InnoDB has a lower effective page utilization.

The size of TXRocks SST files is generally set to dozens or hundreds of MB or a greater value. Therefore, TXRocks has much fewer wastes caused by 4K alignment. Although an SST file is divided into blocks, those blocks don't need to be aligned.

In addition, TXRocks SST files use prefix compression, so that only one record will be generated for data records with the same prefix. SST files at different levels can adopt different compression algorithms, further reducing the storage space overheads. For transaction overheads, InnoDB records must contain `trx id` and `roll_ptr` fields. By contrast, other transaction overheads don't need to be stored for SST files at the lowest level of TXRocks (containing most data); for example, the version number in a record can be erased after a long enough period of time.

#### Lower write amplification
InnoDB uses the in-place change mode, where the entire page may be flushed to the disk even when only one row of data is changed, causing a high write amplification and more random writes.

TXRocks uses the append-only change mode, which has a lower write amplification; therefore, it is more friendly to devices such as SSD with a limited number of write cycles.

## Use Cases
TXRocks is very suitable for businesses that are sensitive to the storage costs, have much more writes than reads and a large data volume, and require a high transaction read/write performance.

## How to Use TXRocks
For more information, see [Instructions](https://intl.cloud.tencent.com/document/product/236/47014).

## Optimization and Subsequent Development 
The TXSQL team has been optimizing TXRocks based on business needs; for example, they have improved the SUM query performance by over 30 times. They are also actively exploring the integration with new hardware to uses AEP as the L2 cache for higher performance and cost-effectiveness.

As the storage engine of TencentDB for MySQL, TXRocks will be continuously optimized and improved with regard to problems encountered during use. The TXSQL team will also make technical explorations based on new hardware and release TXRocks in more key services as an important supplement to InnoDB.

