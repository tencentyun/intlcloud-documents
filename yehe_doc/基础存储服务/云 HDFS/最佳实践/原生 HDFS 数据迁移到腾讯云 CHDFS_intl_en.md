## Preparations

1. Create a CHDFS instance and a CHDFS mount point and configure the permission information at the Tencent Cloud official website.
2. Access the created CHDFS instance from a CVM instance in a VPC. For more information, please see [Creating CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41961).
3. After the mount is successful, open the Hadoop command line tool and run the following command to verify whether the CHDFS instance works properly.
```bash
hadoop fs -ls ofs://f4xxxxxxxxxxxxxxx.chdfs.ap-beijing.myqcloud.com/
```
If you can see the output similar to the following, the CHDFS instance works properly.
![](https://main.qcloudimg.com/raw/3be9476976dd7da027ea6e634652c00b.png)

## Migration

After the preparations are completed, you can use the standard DistCp tool in the Hadoop community to perform full or incremental HDFS data migration. For more information, please see [DistCp](https://hadoop.apache.org/docs/r1.0.4/cn/distcp.html).

#### Notes

The Hadoop DistCp tool provides some parameters that are incompatible with CHDFS. If you specify some parameters in the following table, they will not take effect.

| Parameter| Description                                        | Status |
| -------- | ----------------------------------------------- | -------- |
| -p[rbax] | r: replication; b: block-size; a: ACL, x: XATTR | Not effective   |

#### Samples

1. When the CHDFS instance is ready, run the following Hadoop command to perform data migration.
```bash
hadoop distcp hdfs://10.0.1.11:4007/testcp ofs://f4xxxxxxxx-xxxx.chdfs.ap-beijing.myqcloud.com/
```
Here, `f4xxxxxxxx-xxxx.chdfs.ap-beijing.myqcloud.com` is the mount point domain name, which needs to be replaced with the information of your actual mount point.
2. After the Hadoop command is executed, the details of the migration will be printed in the log as shown below:
```plaintext
2019-12-31 10:59:31 [INFO ] [main:13300] [org.apache.hadoop.mapreduce.Job:] [Job.java:1385]
 Counters: 38
    File System Counters
        FILE: Number of bytes read=0
        FILE: Number of bytes written=387932
        FILE: Number of read operations=0
        FILE: Number of large read operations=0
        FILE: Number of write operations=0
        HDFS: Number of bytes read=1380
        HDFS: Number of bytes written=74
        HDFS: Number of read operations=21
        HDFS: Number of large read operations=0
        HDFS: Number of write operations=6
        OFS: Number of bytes read=0
        OFS: Number of bytes written=0
        OFS: Number of read operations=0
        OFS: Number of large read operations=0
        OFS: Number of write operations=0
    Job Counters
        Launched map tasks=3
        Other local map tasks=3
        Total time spent by all maps in occupied slots (ms)=419904
        Total time spent by all reduces in occupied slots (ms)=0
        Total time spent by all map tasks (ms)=6561
        Total vcore-milliseconds taken by all map tasks=6561
        Total megabyte-milliseconds taken by all map tasks=6718464
    Map-Reduce Framework
        Map input records=3
        Map output records=2
        Input split bytes=408
        Spilled Records=0
        Failed Shuffles=0
        Merged Map outputs=0
        GC time elapsed (ms)=179
        CPU time spent (ms)=4830
        Physical memory (bytes) snapshot=1051619328
        Virtual memory (bytes) snapshot=12525191168
        Total committed heap usage (bytes)=1383071744
    File Input Format Counters
        Bytes Read=972
File Output Format Counters
        Bytes Written=74
    org.apache.hadoop.tools.mapred.CopyMapper$Counter
        BYTESSKIPPED=5
        COPY=1
        SKIP=2
```

