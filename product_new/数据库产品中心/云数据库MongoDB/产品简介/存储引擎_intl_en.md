TencentDB for MongoDB supports both MongoRocks and WiredTiger engines.

## MongoRocks Engine
The MongoRocks engine is built on RocksDB, a KV store that is ideal for MongoDB document structures.
Currently, it supports MongoDB 3.2 (stable version), MongoDB 3.4 (stable version), and MongoDB 3.6 (unstable version, where features in v3.6 such as Change Stream are not supported).

### Pros and Cons of MongoRocks
As MongoRocks is built on RocksDB, it has both the common advantages and disadvantages of Log Structured Merge (LSM) storage systems, including:

- **Read amplification**
In RocksDB, reads are first made to MemTable, and if no MemTable is found, the SST file must be found layer by layer from newest to oldest (top to bottom) until the desired data is located. This process may require more than one I/O. Although the read amplification can be improved with Bloom filter and Cache, it is still quite obvious in scenarios such as range query.
- **Write amplification**
Each write operation in RocksDB needs to be persisted as SST files of level 0 by Immutable MemTable, the level 0 files are merged into level 1 files, the level 1 files are merged into level 2 files, and so on and so forth. One write request will generate multiple disk I/Os. The lifetime of an SSD is subject to the number of writes to it, so special attention should be paid to write amplification for SSDs.
- **Disk amplification**
All writes are appends, so expired data will not be immediately cleaned up.
- **Write limitation**
WriteStall may cause lags in RocksDB. If the write speed exceeds the speed of MemTable persistence and SST merge, the engine will limit the write speed; otherwise, the number of SST files will increase dramatically, and the read performance will decrease accordingly. Therefore, lags may occur if the writing speed is too high.

### Optimization of MongoRocks by Tencent Cloud
#### Background
In native MongoRocks, when the oplog space reaches the upper size limit of capped collection, the delete oplog action will be triggered, which will generate many disk I/Os after write amplification. The oplogs have the following features:
- They are incremented strictly by time sequence, so they are also sorted by key when stored in RocksDB.
- They have insert operations but no update operations, so there is no need for compaction of the SST files.
- When deleted, they are deleted from oldest to newest, i.e., starting with the earliest SST file.

#### Optimizations
In terms of the characteristics of oplogs, we separate oplogs and oplog metadata into two column families and use compact to clean up oplogs, which will generate very few I/Os. The specific process is as shown below:
- Determine whether extra oplogs require deletion (by checking whether the space occupied exceeds the size of 2 SST files).
- Obtain the SST file metadata of the oplogs and traverse starting from the earliest SST file, until the total size of the SST files exceeds the space threshold.
- Call the maximum deletion time of the compaction filter and set it to the maximum key of the SST file cluster found above.
- Actively call compactRange to remove the oplogs. After such optimization, the oplogs are cleaned up and only minimal I/Os are produced.

### Applicable Scenarios of MongoRocks
Currently, MongoRocks is widely used in the industry. For example, cached cold data and WeChat billing cold data within Tencent are stored with the MongoRocks engine.
- **Scenarios with extremely high latency and glitch requirements**
Practice shows that the performance of the WiredTiger engine is excellent when its cache size is higher than the index size; however, the database will trigger eviction if the index is not completely in the memory. In this case, the request delay will be increased significantly. In contrast, MongoRocks has a much more stable performance.
- **Multi-table scenarios**
In the WiredTiger engine, each table and index are stored as a single file. When there are too many tables, a large number of small files will be generated on the disk, which seriously compromises performance. Practical experience shows that the performance of the database will deteriorate when the number of collections reaches several thousand. In contrast, the MongoRocks engine does not create a file for each table, which helps avoid this problem.
- **Cold data storage scenario**
For cost considerations, cold data is usually stored on inexpensive storage media such as SATA. The performance of the WiredTiger engine on HDDs is not satisfactory, especially in the case of eviction. On the contrary, the MongoRocks engine converts random writes of I/O to sequential writes, which is very friendly to HDDs.

## WiredTiger Engine
WiredTiger is a typical B-tree structure.

## Engine Comparison
**Test environment:**
CPU: Intel Xeon 2.3 GHz, 24 cores
Memory: 50 GB Cache
Disk: PCIE-SSD
Version: MongoDB v3.2, WiredTiger engine, and MongoRocks engine

| Test Performance | Test Result | 
|---------|---------|
| Disk capacity consumption | Test model: Compare the size of disk data files after writing 500 GB of documents (each 500 B in size). <br>Conclusion: For the same data, MongoRocks consumes slightly more disk capacity than WiredTiger. | 
| 100% read performance comparison | Test model: In a single collection of 500 GB data, the data is read randomly, and after the data is warmed up for 10 minutes, the QPS value within the next 10 minutes is recorded. <br>Conclusion: MongoRocks slightly outperforms WiredTiger in terms of data reads and has a more stable QPS in pure read scenarios. | 
| 100% write performance comparison | Test model: Compare the write speed 10 minutes after 500 GB of documents (each 500 B in size) is written. <br>Conclusion: The write performance of MongoRocks is significantly better than that of WiredTiger, and MongoRocks does not experience the same performance deterioration as WiredTiger during the write process. | 
| 1:1 read/write performance comparison | Test model: After 500 GB of documents (each 500 B in size) is written, reads and writes are performed on a 1:1 basis. After the data is warmed up for 10 minutes, the QPS value within the next 10 minutes is recorded. <br>Conclusion: MongoRocks and WiredTiger perform basically the same in the 1:1 read/write scenario, but WiredTiger has some performance glitches. | 

