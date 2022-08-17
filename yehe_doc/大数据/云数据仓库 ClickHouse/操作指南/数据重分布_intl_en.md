## Feature Overview
This document describes how to redistribute data in the CDWCH console. Currently, CDWCH supports horizontally scaling out a cluster to add nodes for higher computing and storage capabilities. However, ClickHouse doesn't support automatic data rebalancing in cluster datasets and requires human intervention to redistribute the data. How to automate data redistribution has always been a challenge in ClickHouse use and Ops. In contrast, CDWCH offers an data redistribution feature to implement unattended cluster data rebalancing in part mode or resharding mode.

## Notes
1. Resharding will reinsert data, and the temporary data in the process will occupy storage space. Before using the resharding mode, ensure that the current remaining capacity exceeds the storage size of the table for the current task.
2. A data table can be associated with only one task, and a cluster supports at most one running task at a time.
3. The local table database must be atomic (default) or ordinary, and the table type must be a table from the MergeTree engine family (including non-replicated and replicated tables; a materialized view table is not supported).
4. The replica relationship of the local table must be consistent with the cluster. There must be a distributed table providing a view to the relationship between shards.
5. Resharding redistribution redistributes data according to the hash rules of distributed tables, and part redistribution balances data at part granularity regardless of the hash rules of distributed tables.
6. Redistribution will generate a temporary table, which is named in the format of "original table name_resharding_temp_task ID_random number". When the status changes to "To switch", verify that the temporary table data is correct and perform switching. After the switching is completed, the original table data will be saved in the table named "original table name_resharding_task ID_random number", and you can delete the old data after verifying it is correct.
7. During redistribution, the original table is set to **read-only** by default. At the table level, you can select some data in partition granularity to redistribute. If no data needs to be written to the redistributed partitions, you can disable read-only for the table; if data needs to be written, disabling read-only will cause data inconsistency. Currently, you cannot select all partitions to make them writable.
8. Redistributed data will be saved in a temporary table, which will replace the original table during the table exchange. Incorrect data may be read in this process. Generally, the exchange takes several seconds.
9. A task may be paused due to cluster problems. If a task is paused, you can repair or configure the cluster based on the reported error, and resume the task.
10. The strings of table creation statements for the redistributed local table and distributed table must be identical.
11. In resharding mode, all the cluster shards must have the same `internal_replication` configuration (either `true` or `false`).
12. Clusters using cloud disks for data tiering must be restarted before redistribution is performed.

## Directions
1. Log in to the [CDWCH console](https://console.cloud.tencent.com/cdwch), select the target cluster in the **Cluster List**, and click the **Data Redistribution** tab on the cluster details page. 
2. You can view the list of existing data redistribution tasks on the current page.
![](https://qcloudimg.tencent-cloud.cn/raw/1b55691ef5192ada81c71bcca6710c48.jpg)
3. Click **Create Task**, enter the task name, select the v_cluster of the table, migration mode (part or resharding), and distributed table for redistribution, and click **OK**.
	- **Part mode**: Parts are migrated between cluster shards to rebalance data. This mode doesn't need to follow the sharding specifications of the distributed table, and is more suitable for `rand()` distributed tables.
	- **Resharding mode**: The original table data is rewritten to the entire cluster according to the distributed table specifications to rebalance data between shards. This mode is preferred if data needs to be allocated to the same shard based on the primary key.
At the table level, you can select some data in partition granularity to redistribute. You can also set whether to make the table writable in partition granularity. If no data needs to be written to the redistribution partition, you can disable the read-only status; otherwise, disabling the status will cause data inconsistency.
 ![](https://qcloudimg.tencent-cloud.cn/raw/711fa1ba794026d338dbfb7ba81897c6.jpg)

The data redistribution feature uses components with multiple concurrency mechanisms to improve the task performance. To strike a balance between the business load and the impact of data redistribution on the cluster, you can use the **task concurrency** and **node concurrency** to adjust the performance and speed of the task.
>? 
>- **Node concurrency** indicates the partition concurrency on a single ClickHouse node in resharding mode or the part concurrency on a single ClickHouse node in part mode.
>- **Task concurrency** indicates the total concurrency of all the nodes involved in the task during the task execution.
>- Setting either of the parameters to 0 will pause the task. In addition, the effect of the same value may differ by cluster specification or task. You can adjust the values to control the task speed, performance, and cluster load as needed.

4. After creating a data redistribution task, you can start, edit, or delete it. The edit window is similar to the creation window and allows you to modify the task information.
![](https://qcloudimg.tencent-cloud.cn/raw/390487b6234477b8db2015e9b6e9b6d7.jpg)
5. Click **Start** to start the task, and the CDWCH instance will enter the **Changing** status (which will also be displayed on the cluster's basic information page, without a progress bar though).
![](https://qcloudimg.tencent-cloud.cn/raw/e318c0b4be9589ac04a33cc30a81d51b.jpg)
After the task is started, you can click **Modify Parameter** to modify the task concurrency and node concurrency to control the task speed and cluster load and even pause the task.
6. Click **Details** to view the execution details of the data redistribution task at the table level.
![](https://qcloudimg.tencent-cloud.cn/raw/6d67fa66d0c608658517b329fa223920.jpg)
7. The table data redistribution has three phases:
![](https://qcloudimg.tencent-cloud.cn/raw/eb6b4b23482e61da202ec2b8e00e9586.jpg)

  - **Executing**: Data in the table is being redistributed, which may involve creating and deleting temporary tables, moving and deleting parts, and reading/writing data based on the selected mode. At this point, the read/write performance of the cluster may drop.
  - **To switch**: Data in the distributed table has been redistributed, but the original table is not replaced yet. You need to verify and make sure that data in the temporary table generated during data redistribution is correct and consistent with the original data. Then, you can perform the switch to make your business access the target table.
>! 
>- **Before switching to the data source after redistribution, ensure you have completed data consistency and accuracy checks. The data table after switching will be used as the only data source for system reads and writes.**
>- For redistribution by partition, verify data consistency and accuracy before and after the redistribution at the partition level.

  - **Original table pending deletion**: After the switch, the data file of the original table will not be directly deleted. You need to verify the accuracy of the rebalanced data before the deletion. After the deletion, the table will enter the **Executed successfully** status.

>! 
>- **This operation will permanently delete the physical files of the data table before data redistribution. Ensure you have completed data consistency and accuracy checks, and you have finished switching data sources.** 
>- For redistribution by partition, only the data file of the corresponding partition of the original table will be deleted.

8. In addition, before **switching** the redistributed table, you can **cancel** the table or the entire task to stop the data redistribution operation and roll back the data. A **switched** or **deleted** table cannot be rolled back.
9. During task execution, if the network jitters, the ClickHouse component is restarted, or other accidents occur in the cluster, the task may enter the **Paused** status, with the cause displayed. You can adjust the cluster accordingly or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
10. When all the redistributed tables enter the final status (**Canceled** or **Executed successfully**), the redistribution task status will become **Execution ended**, and the CDWCH instance status will become **Running**.
![](https://qcloudimg.tencent-cloud.cn/raw/1ec749d99c94f41a415b1443300e1b60.jpg)

## Best Practices for Data Redistribution
### Scenarios
1. The data is imbalanced and the distributed table hash is incorrect after scale-out.
2. Data imbalance is caused by business data insertion.
3. You want to adjust the table data distribution policy.

### Parameter adjustment
Before a data redistribution task starts, we recommend you add the following parameters to grant permissions; otherwise, the task may pause as the following permissions are required to delete the generated temporary table.
```
<max_table_size_to_drop>0</max_table_size_to_drop>
<max_partition_size_to_drop>0</max_partition_size_to_drop>
```
For instances with more than 32 CPU cores, we recommend you increase the following parameter values in resharding mode during data redistribution. As data reimport will result in a large number of write requests, doing so will enhance the merge capabilities of the backend to prevent a lot of parts from emerging and thereby causing the too-many-parts error.
```
<background_pool_size>64</background_pool_size>
<background_schedule_pool_size>64</background_schedule_pool_size>
```

### Suggestions
1. We recommend you perform redistribution during off-peak hours, as data will be rewritten in resharding mode and impose a higher load stress on the cluster.
2. Before using the part mode, we recommend you manually run the `optimize` statement to trigger a merge. This increases the part size, reduces the transferred data volume, and thus enhances the redistribution performance.

## Performance Data
### Test environment 1
Kernel version: 21.8.12.29
High availability: High availability
Compute node type: High I/O
Compute node specification: 64-core 256 GB MEM
Compute node quantity: 4 (two shards), 8 (four shards), and 16 (eight shards)
Compute node storage: 14,280 GB local disk
ZooKeeper node specification: 16-core 64 GB MEM
ZooKeeper node quantity: 3
ZooKeeper node storage: 100 GB enhanced SSD
Data generation tool: ssb-dbgen

#### Test scenario 1
Expanding two shards to four shards.

**Resharding mode**

|No. |Number of Tables |Total Data Volume |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |335 GB |2 minutes 58 seconds |1.878 GB/s |
|2 |1 |898 GB |9 minutes 18 seconds |1.609 GB/s |
|3 |2 |670 GB |5 minutes 23 seconds |2.074 GB/s |
|4 |2 |1,796 GB |13 minutes 25 seconds |2.23 GB/s |
|5 |4 |1,340 GB |11 minutes 17 seconds |1.979 GB/s |
|6 |4 |3,592 GB |24 minutes 33 seconds |2.439 GB/s |

**Part mode**

|No. |Number of Tables |Total Data Volume (Migrated Part Volume) |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |335 GB (180 GB) |1 minute 44 seconds |1.737 GB/s |
|2 |1 |898 GB (476 GB) |6 minutes 27 seconds |1.229 GB/s |
|3 |2 |792 GB (397 GB) |4 minutes 50 seconds |1.370 GB/s |
|4 |2 |1,796 GB (952 GB) |11 minutes 38 seconds |1.364 GB/s |
|5 |4 |1,675 GB (903 GB) |10 minutes 28 seconds |1.438 GB/s |
|6 |4 |3,592 GB (2,379 GB) |28 minutes 6 seconds |1.411 GB/s |

#### Test scenario 2
Expanding four shards to eight shards.
**Resharding mode**

|No. |Number of Tables |Total Data Volume |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |1,034 GB |3 minutes 39 seconds |4.715 GB/s |
|2 |2 |2,068 GB |6 minutes 58 seconds |4.95 GB/s |
|3 |4 |4,136 GB |13 minutes 1 second |5.301 GB/s |

**Part mode**

|No. |Number of Tables |Total Data Volume (Migrated Part Volume) |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |1,034 GB (524 GB) |3 minutes 19 seconds |2.633 GB/s |
|2 |2 |2,068 GB (1,049 GB) |6 minutes 35 seconds |2.656 GB/s |
|3 |4 |4,136 GB (2,097 GB) |12 minutes 3 seconds |2.900 GB/s |

#### Test scenario 3
Expanding four shards to four shards.
**Resharding mode**

|No. |Number of Tables |Total Data Volume |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |1,034 GB |10 minutes 16 seconds |1.679 GB/s |
|2 |2 |2,068 GB |20 minutes 34 seconds |1.676 GB/s |
|3 |4 |4,136 GB |37 minutes 12 seconds |1.853 GB/s |

### Test environment 2
Kernel version: 21.8.12.29
High availability: High availability
Compute node type: Big Data
Compute node specification: 64-core 256 GB MEM
Compute node quantity: 16
Compute node storage: 2,142,720 GB local disk
ZooKeeper node specification: 16-core 64 GB MEM
ZooKeeper node quantity: 3
ZooKeeper node storage: 500 GB enhanced SSD
#### Test scenario 1
Expanding two shards to four shards.

**Resharding mode**

|No. |Number of Tables |Total Data Volume |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |773 GB |7 minutes 21 seconds |1.752 GB/s |
|2 |2 |1,585 GB |15 minutes 43 seconds |1.681 GB/s |
|3 |4 |3,209 GB |32 minutes 9 seconds |1.664 GB/s |

**Part mode**

|No. |Number of Tables |Total Data Volume (Migrated Part Volume) |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |774 GB (393 GB) |4 minutes 47 seconds |1.371 GB/s |
|2 |2 |1,548 GB (786 GB) |9 minutes 53 seconds |1.563 GB/s |
|3 |4 |3,096 GB (1,572 GB) |19 minutes 18 seconds |1.358 GB/s |

#### Test scenario 2
Expanding four shards to eight shards.
**Resharding mode**

|No. |Number of Tables |Total Data Volume |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |855 GB |4 minutes 37 seconds |3.087 GB/s |
|2 |2 |1,667 GB |9 minutes 6 seconds |3.053 GB/s |
|3 |4 |3,292 GB |18 minutes 49 seconds |2.916 GB/s |

**Part mode**

|No. |Number of Tables |Total Data Volume (Migrated Part Volume) |Total Duration |Average Speed |
|---------|---------|---------|---------|---------|
|1 |1 |1,072 GB (542 GB) |3 minutes 21 seconds |2.697 GB/s |
|2 |2 |2,144 GB (1,084 GB) |6 minutes 24 seconds |2.823 GB/s |
|3 |4 |4,288 GB (2,167 GB) |12 minutes 34 seconds |2.874 GB/s |
