An HBase table is built based on Hadoop HDFS. Therefore, HBase data can be migrated with DistCp of Hadoop HDFS or relevant tools provided by the HBase layer based on the HBase table structure.
 ![](https://main.qcloudimg.com/raw/2793e8e2ecb6314751b5b4bc0edfc6c2.png)
As shown above, there are multiple HBase migration schemes, among which snapshot-based migration is recommended.

### Snapshot-based HBase Migration
1. Create a table in the new cluster with the same structure as in the original cluster.
2. Run `hbase shell` to create a snapshot in the original cluster.
```
$ ./bin/hbase shell  
hbase>snapshot 'myTable', 'myTableSnapshot'  
```
Here, `'myTable'` is the HBase table name, and `'myTableSnapshot'` is the HBase snapshot name. You can run `list_snapshots` to check whether the snapshot is successfully created or run `delete_snapshot` to delete it.
```
hbase> delete_snapshot 'myTableSnapshot'  
```
3. Export the snapshot from the source cluster to the target one.
```
hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot myTableSnapshot -copy-to hdfs://10.0.0.38:4007/hbase/snapshot/myTableSnapshot  
```
Here, `10.0.0.38:4007` is the value of `$activeip:$rpcport` of the target cluster. When the snapshot is exported, the system will start a MapReduce job. You can add `-mappers 16 -bandwidth 200` to specify the mapper and bandwidth. Here, `200` indicates 200 MB/sec.
4. Restore the snapshot to the target HDFS in the target cluster by running the following command in the target cluster.
```
hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot myTableSnapshot -copy-from /hbase/snapshot/myTableSnapshot -copy-to /hbase/  
```
5. Restore the corresponding HBase table and data from HDFS in the target cluster.
```
hbase> disable "myTable"  
hbase> restore_snapshot 'myTableSnapshot'  
hbase> enable 'myTable'  
```
6. You can test the migration result by using a simple HBase table.
