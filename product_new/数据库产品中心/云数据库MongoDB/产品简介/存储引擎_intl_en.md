TencentDB for MongoDB supports both MongoRocks and WiredTiger engines.

## MongoRocks Engine
MongoRocks is based on RocksDB, a KV store that is ideal for MongoDB document structures.
Currently, it supports MongoDB 3.2 (stable version), MongoDB 3.4 (stable version), and MongoDB 3.6 (unstable version which does not support some features in v3.6 such as Change Stream).

### Pros and Cons of MongoRocks
As MongoRocks is based on RocksDB, it has the common advantages and disadvantages of Log Structured Merge (LSM) storage systems, including:

- **Read amplification**
In RocksDB, reads are first made to MemTable. If no MemTable is found, RocksDB will scan through SST files layer by layer from the newest to the oldest (from top to bottom) until the desired data is located. This process may require more than one I/O. Although the read amplification can be reduced with Bloom filter and Cache, it is still quite obvious in scenarios such as range query.
- **Write amplification**
Each write in RocksDB needs to be persisted as level-0 SST files by Immutable MemTable, and the Level-0 files need to be compacted into level-1 files. Thus one write request will generate multiple disk I/Os. The lifespan of an SSD is subject to the number of writes to it, so special attention should be paid to write amplification for SSDs.
- **Disk amplification**
All writes are appends, so expired data will not be immediately cleaned up.
- **Write limitation**
Write Stall may cause lags in RocksDB. If the writing speed is higher than the speed of MemTable persistence and SST files compaction, the engine will limit the write speed; otherwise, SST files will increase dramatically in number, which will further degrade read performance. Therefore, lags may occur if the writing speed is too high.

### Optimization of MongoRocks by Tencent Cloud
#### Background
In the native MongoRocks, when the size of the oplog reaches the upper limit, the delete oplog action will be triggered, which will generate many disk I/Os after write amplification. The oplog has the following features:
- Oplogs are created chronologically, so they are also sequenced by key when stored in RocksDB.
- There is an insert option but no update option, so SST files do not need compaction.
- Oplogs are deleted from the oldest to the newest, which means that the deletion starts with the earliest SST file.

#### Optimizations
Given the features of the oplog, we put oplogs and oplog metadata separately into two column families and clean up oplogs through compaction. In this way, only very few I/Os will be generated. Please find the specific process below:
- Determine whether extra oplogs need to be deleted by checking whether the space occupied exceeds the upper limit by the size of 2 SST files.
- Obtain the SST file metadata of the oplogs and scan through the SST files starting from the earliest one until the total size of the files scanned exceeds the space needed.
- Call the maximum deletion time of the compaction filter and set it as the maximum key for the SST file cluster mentioned above.
- Actively call CompactRange to delete the oplogs. With such optimization, only very few I/Os are generated for the oplog clean-up.

### Applicable Scenarios of MongoRocks
Currently, MongoRocks is widely used in the industry. For example, cached cold data and WeChat billing cold data within Tencent are stored with the MongoRocks engine.
- **Scenarios that require minimal latency and glitches**
Practice shows that the performance of the WiredTiger engine is excellent when its cache size is larger than the index size; however, the database will trigger eviction if the index is not completely in the memory. In this case, the request delay will increase significantly. In contrast, MongoRocks has a much more stable performance.
- **Multi-table scenarios**
In the WiredTiger engine, each table and index is stored as a single file. When there are too many tables, a large number of small files will be generated on the disk, which will seriously compromise performance. Practical experience shows that the performance of the database will deteriorate when the number of collections reaches several thousand. In contrast, the MongoRocks engine does not create a file for each table, which avoids this problem.
- **Cold data storage scenario**
For cost considerations, cold data is usually stored on inexpensive storage media such as SATA. The performance of the WiredTiger engine on HDDs is not satisfactory either, especially in the case of eviction. By contrast, the MongoRocks engine converts random writes of I/O to sequential writes, which is very friendly to HDDs.

## WiredTiger Engine
WiredTiger has a typical B-tree structure.

## Engine Comparison
**Test environment:**
CPU: Intel Xeon 2.3 GHz, 24 cores
Memory: 50 GB Cache
Disk: PCIE-SSD
Version: MongoDB v3.2, WiredTiger engine, and MongoRocks engine

| Test Performance | Test Result | 
|---------|---------|
| Disk capacity consumption | Test model: compare the size of disk data files after writing 500 GB of documents (each 500 B in size). <br>Conclusion: for the same data, MongoRocks consumes slightly more disk capacity than WiredTiger. | 
| 100% read performance comparison | Test model: read data randomly in a single collection of 500 GB data, and after the data is warmed up for 10 minutes, record the QPS value within the next 10 minutes. <br>Conclusion: MongoRocks is slightly better than WiredTiger in terms of read performance and has a more stable QPS in read-only scenarios. | 
| 100% write performance comparison | Test model: compare the writing speed within the 10 minutes after 500 GB of documents (each 500 B in size) are written. <br>Conclusion: MongoRocks is significantly better than WiredTiger in terms of write performance, and MongoRocks does not show the performance deterioration WiredTiger shows during the writing process. | 
| 1:1 read/write performance comparison | Test model: read and write with a 1:1 ratio after 500 GB of documents (each 500 B in size) are written, after the data is warmed up for 10 minutes, record the QPS value within the next 10 minutes. <br>Conclusion: MongoRocks and WiredTiger tie in performance in the 1:1 read/write scenario, but WiredTiger has some performance glitches. | 

