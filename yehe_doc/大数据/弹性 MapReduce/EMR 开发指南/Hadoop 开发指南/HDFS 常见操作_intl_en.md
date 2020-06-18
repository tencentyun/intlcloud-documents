Elastic MapReduce (EMR) Hadoop service is integrated with the COS service. When you purchase an EMR cluster, if you select COS and make it available for your cluster, you can manipulate the data stored in COS with common Hadoop commands by running the following command.

``` shell
# cat data
hadoop fs -cat /usr/hive/warehouse/hivewithhdfs.db/record/data.txt
# Modify directory or file permission
hadoop fs -chmod -R 777 /usr
# Change file or directory owner
hadoop fs -chown -R root:root /usr
# Create a folder
hadoop fs -mkdir <paths>
# Send a local file to HDFS
hadoop fs -put <localsrc> ... <dst>
# Copy a local file to HDFS
hadoop fs -copyFromLocal <localsrc> URI
# View the storage usage of a file or directory
hadoop fs -du URI [URI …]
# Delete a file
hadoop fs -rm URI [URI …]
# Set the number of copies of a directory or file
hadoop fs–setrep [-R] [-w] REP PATH [PATH …]
# Check for bad blocks of a cluster file
hadoop fsck <path> [-move | -delete | -openforwrite] [-files [-blocks [-locations | -racks]]]
```


For more HDFS commands, please see the [community documentation](http://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-hdfs/HDFSCommands.html). If your cluster is a high-availability cluster (dual-namenode), you can see which namenode is active by running following command:

``` shell
# nn1 is the ID of namenode, which is generally nn1 and nn2
hdfs haadmin -getServiceState nn1
# View current cluster report
hdfs dfsadmin -report
# namenode exited safe mode
hdfs dfsadmin -safemode leave
```

