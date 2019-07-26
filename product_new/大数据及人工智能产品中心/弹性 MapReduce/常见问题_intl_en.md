### How to view task logs?

You can log in to any EMR node and run the following command to view task logs:
```
yarn logs -applicationId application_1507732460084_0057
```

>
>- This command can only be executed by a Hadoop user.
>- If it is a task of another user, you can add the parameter -appOwner username.

To see the cause of a task exception, run the following command:
```
yarn logs -applicationId application_1507732460084_0057|grep -A20 Exception
```

### How to adjust the computing resources of a cluster?
Cluster computing resources are determined by the following two configuration items in yarn-site.xml:
``` xml
<property>
  <name>yarn.nodemanager.resource.cpu-vcores</name>
  <value>4</value>
</property>
<property>
  <name>yarn.nodemanager.resource.memory-mb</name>
  <value>14745</value>
</property>
```
By default, cpu-vcores is equal to number of CPU cores of the server, and memory-mb is equal to 91% of the memory size of the server. They can be adjusted based on your actual needs, but if they are too large, there may be a risk of server failure.

### How to fix an out of memory error?
If an out of memory error occurs when you are submitting a MapReduce task or running an SQL script through Hive, fix it by setting the following parameters:

- `set mapreduce.map.java.opts=-Xmx4096m;`
- `set mapreduce.reduce.java.opts=-Xmx4096m;`

The memory parameter can be adjusted based on your actual computation needs. It can also be written in the ~/.hiverc file in Hive and will be executed automatically when submitted.

### How to estimate the cluster size?
Suppose that you need to run an SQL query. If 64 vcores and 128 GB memory are needed for getting the query result in the specified time period, and the business requires 10 concurrencies, then the required resources would be 640 vcores and 1,280 GB memory. If the server specification you are using is 24 cores and 48 GB memory, then you need around 1280 / 48 = 40 servers.

### How to set up a fetch query in Hive?
The default query in Hive is as follows:

``` sql
select * from tablename where a=’1’ limit 10;
```

The default query does not start a computation task. You can start a distributed query by adding the `set hive.fetch.task.conversion=none` parameter.

### How to choose the cluster storage media?
An EMR cluster supports the following storage media: HDD local disk, SSD local disk, HDD cloud disk, SSD cloud disk, and COS. You can choose the most appropriate one based on your actual needs:
- If your application scenario is large-scale data warehouse analysis which is not very latency-sensitive, you are recommended to use COS as the underlying storage.
- If you are very familiar with HDFS and the cost of migration to COS would be too high, you can use HDD cloud disks.
- If your application is a massive columnar database (HBase) which requires efficient writing and querying, you are recommended to use SSD local or cloud disks.

