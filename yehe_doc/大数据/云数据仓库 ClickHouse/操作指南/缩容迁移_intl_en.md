## Overview

This document describes how to scale in a ClickHouse cluster and migrate data in the console. Currently, CDW supports horizontally scaling in a cluster to reduce nodes. Data on the removed nodes should be migrated to remaining nodes to avoid business data loss. Specifically, data can be migrated by part and then distributed evenly on the remaining nodes. 

## Notes
1. Node data migration is performed by part. When data is migrated from the source shard to the target shard, table data in the target shard will be rebalanced by part.
2. A data table can be associated with only one task, and a cluster supports at most one running task at a time.
3. The local table database must be atomic (default) or ordinary, and the table type must be a table from the MergeTree engine family (including non-replicated and replicated tables; a materialized view table is not supported).
4. The replica relationship of the local table must be consistent with the cluster. There must be a distributed table providing a view to the relationship between shards.
5. Migration will generate a temporary table, which is named in the format of "original table name_resharding_temp_task ID_random number". When the status changes to **To switch**, verify that the temporary table data is correct and perform switching. After the switching is completed, the original table data will be saved in the table named "original table name_resharding_task ID_random number", and you can delete the old data after verifying it is correct.
6. During migration, the original table is set to **read-only** by default. You can select some data in partition granularity to migrate. If no data needs to be written to the migrated partitions, you can disable read-only for the table; if data needs to be written, disabling read-only will cause data inconsistency. Currently, you cannot select all partitions to make them writable.
7. The migration task can be configured with the task concurrency and node concurrency to control the performance. If either of the values is 0, the task will be paused.
8. Migrated data will be saved in a temporary table, which will replace the original table during the table switch. Incorrect data may be read in this process. Generally, the switch takes several seconds.
9. A task may be paused due to cluster problems. If a task is paused, you can repair or configure the cluster based on the reported error, and resume the task.
10. The strings of table creation statements for the migrated local table and distributed table must be identical.
11. Clusters using cloud disks for data tiering must be restarted before scale-in and migration is performed.

## Directions
1. Log in to the [CDW console](https://console.cloud.tencent.com/cdwch), select the target cluster in the **Cluster List**, and click the **Scale-in and Migration** tab on the cluster details page.
2. You can view the list of existing scale-in and migration tasks on the current page.
3. Click **Create Task**, enter the task name, select the v_cluster of the table, source shard, target shard, and distributed table for migration, and click **OK**.
We recommend you select the source and target shards in line with the scale-in requirements and use the shard to be removed as the source shard.
The **part mode** is used by default to migrate data after scale-in. The parts of the table on the source shard are used to rebalance data between shards. This mode doesn't need to follow the sharding specifications of the distributed table, and is more suitable for `rand()` distributed tables.
At the table level, you can select some data in partition granularity to migrate. If no data needs to be written to the migrated partitions, you can disable read-only for the table; if data needs to be written, disabling read-only will cause data inconsistency.

The scale-in and migration feature uses components with multiple concurrency mechanisms to improve the task performance. To strike a balance between the business load and the impact of scale-in and migration on the cluster, you can use the **task concurrency** and **node concurrency** to adjust the performance and speed of the task.
>? 
>- **Node concurrency** indicates the part concurrency on a single ClickHouse node.
>- **Task concurrency** indicates the total concurrency of all the nodes involved in the task during the task execution.
>- Setting either of the parameters to 0 will pause the task. In addition, the effect of the same value may differ by cluster specification or task. You can adjust the values to control the task speed, performance, and cluster load as needed.

4. After creating a scale-in and migration task, you can start, edit, or delete it. The edit window is similar to the creation window and allows you to modify the task information.
5. Click **Start** to start the task, and the CDW instance will enter the **Changing** status (which will also be displayed on the cluster's basic information page, without a progress bar though).

After the task is started, you can click **Modify Parameter** to modify the task concurrency and node concurrency to control the task speed and cluster load and even pause the task.
6. Click **Details** to view the execution details of the scale-in and migration task at the table level.
7. The table data migration has three phases:
  - **Executing**: Data in the table is being migrated, which may involve creating and deleting temporary tables, moving and deleting parts, and reading/writing data. At this point, the read/write performance of the cluster may drop.
  - **To switch**: Data in the distributed table has been migrated, but the original table is not replaced yet. You need to verify and make sure that data in the temporary table generated in the target shard is correct and consistent with the original data. Then, you can perform the switch to make your business access the target table.
>! 
>- **Before switching the data source, be sure to verify the data consistency and accuracy before and after the migration. The data table after switching will be used as the only data source for system reads and writes.**
>- For scale-in and migration by partition, verify data consistency and accuracy before and after the migration at the partition level.

  - **Original table pending deletion**: After the switch, the data file of the original table will not be directly deleted. You need to verify the accuracy of the data rebalanced in the target shard before the deletion. After the deletion, the table will enter the **Executed successfully** status.
>!
>- **This operation will permanently delete the physical files of the data table before data migration. Ensure you have completed data consistency and accuracy checks, and you have finished switching data sources.** 
>- For scale-in and migration by partition, only the data file of the corresponding partition of the original table will be deleted.

8. In addition, before **switching** the migrated table, you can **cancel** the table or the entire task to stop the data migration operation and roll back the data. A **switched** or **deleted** table cannot be rolled back.
9. During task execution, if the network jitters, the ClickHouse component is restarted, or other accidents occur in the cluster, the task may enter the **Paused** status, with the cause displayed. You can adjust the cluster accordingly or submit a ticket for assistance.
10. When all the migrated tables enter the final status (**Canceled** or **Executed successfully**), the migration task status will become **Execution ended**, and the CDW instance status will become **Running**.

## Best Practices
### Scenarios
1. You want to retain the data on a node to be removed and migrate it to a remaining node before scale-in.
2. You want to redistribute the data.

### Parameter adjustment
Before a scale-in and migration task starts, we recommend you add the following parameters to grant permissions; otherwise, the task may pause as the following permissions are required to delete the generated temporary table.
```
<max_table_size_to_drop>0</max_table_size_to_drop>
<max_partition_size_to_drop>0</max_partition_size_to_drop>
```
### Suggestions
 Before using the part mode, we recommend you manually run the `optimize` statement to trigger a merge. This increases the part size while decreasing the transferred data volume, thus improving scale-in and migration performance.