You can use clickhouse-copier to migrate a CDW cluster.

## Migrating a Cluster with clickhouse-copier
### How clickhouse-copier works 
clickhouse-copier is ClickHouse's official data migration tool, which migrates a cluster or redistributes data based on INSERT operations in distributed tables. 
You can run a clickhouse-copier instance to move data between clusters. It can run simple INSERT...SELECT queries to replicate data between tables with different engine parameters and clusters with different numbers of shards. In the task configuration file, you need to describe the layouts of the source and target clusters and list the tables to be replicated. You can replicate an entire table or certain partitions. clickhouse-copier uses temp distributed tables to select data from the source cluster and insert it to the target cluster. 
clickhouse-copier configures the source and target cluster information as well as the distribution logic of the migrated tables to construct a migration task in each shard and partition. It reads the data from each partition according to certain rules, inserts the read data to temp tables in the target cluster, and runs ATTACH PARTITION to attach the data to the final tables. The task execution status is saved to ZooKeeper to implement task restart, checkpoint restart, and co-execution of the same task by multiple clickhouse-copier processes. 
As the official migration tool, clickhouse-copier also supports tables with MergeTree engines, including replicated and non-replicated ones. 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jzLd831_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E4%BB%93%E5%BA%93%20ClickHouse_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-.png)
                    

### Strengths of clickhouse-copier
1. clickhouse-copier is ClickHouse's official tool maintained and improved by the community in terms of functionality, performance, and other aspects.           
2. Although it is implemented based on the SELECT and INSERT logic and each copier process is executed in a single thread, multiple processes can be used together to process the same task. If one or more processes run on each shard for each copier to handle the local shard data, the overall performance will be improved. The larger the cluster and the more the processes, the better the overall performance.                              
3. It is compatible with various sharding rules of distributed tables. It reads and writes data completely based on the distributed table logic to control the data write logic (such as retaining the original logic or adjusting the sharing rule) during migration based on the task configuration.                              
4. It is adaptive to the cluster shard size before and after migration, eliminating your need to map shards. 
5. It is not affected by business data writes and MERGE operations on the backend. 
6. It can record the status of the migration task in ZooKeeper to support restart upon error and checkpoint restart. This guarantees the migration stability based on the logic of multiple processes. 
7. It doesn't depend on replicated tables, so it supports all tables with MergeTree engines. 
                            
### Notes on clickhouse-copier
1. It is not very easy to use. Many users report in the community that the configuration is complex and difficult, the official documents are insufficient, and best practices need to be summarized. 
2. It has a low standalone performance. It can achieve a high performance only when there are many processes and shards. ClickHouse also recommends a large cluster size for a high performance. 
3. It cannot migrate materialized views at one stop and can hardly retain the logical relationships of underlying tables and materialized views. You need to carefully design a migration plan based on the table characteristics to accelerate migration and minimize the migration's impact on the business.                             
4. Although it supports business data writes and merges during migration, it cannot migrate incremental data if the business doesn't stop writing data. It doesn't support DDL operations either.            
5. It doesn't support non-MergeTree table engines. 
