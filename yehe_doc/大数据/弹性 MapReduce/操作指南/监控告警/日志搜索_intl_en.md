## Feature Overview
The log search feature collects component operation logs and allows log search. You can search for core service logs of the current cluster and server system logs by keyword so as to quickly view key service logs without logging in to the server.

Log search supports filtering logs by current cluster, log file, server IP, and time range. A log result includes the server IP, absolute path of the log on the server, and log content.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitoring** > **Log Search** to filter and view log content by current cluster, log file, server IP, and time range.

**View Context:** during troubleshooting, you usually need to pay attention to contextual logs of keywords. On the log search result list page, you can select **Operation** > **View Context** to view contextual information of a log.



## Service Types Supported for Log Search

>!
>- Currently, only logs in the last 15 days can be searched for.
>- If log collection has not been enabled on your cluster, you can contact your Tencent Cloud rep for assistance.
	
Logs from the four components, namely, HDFS, YARN, Hive, and HBase, can be collected and stored in the following directories and files:

```
/data/emr/hdfs/logs:
hadoop-hadoop.log
hadoop-hadoop-namenode-x.x.x.x.out
hadoop-hadoop-datanode-x.x.x.x.out

/data/emr/yarn/logs:
yarn-hadoop-resourcemanager-x.x.x.x.out
yarn-hadoop-resourcemanager-x.x.x.x.log
yarn-hadoop-nodemanager-x.x.x.x.out
yarn-hadoop-nodemanager-x.x.x.x.log

/data/emr/hive/logs:
hadoop-hive
hcat.err
hcat.out

/data/emr/hbase/logs:
hbase-hadoop-master-x.x.x.x.out
hbase-hadoop-master-x.x.x.x.log
hbase-hadoop-regionserver-x.x.x.x.out
hbase-hadoop-regionserver-x.x.x.x.log
```

