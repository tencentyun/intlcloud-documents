The GooseFS-integrated Tencent Cloud EMR will be released in the latest version, which allows you to use GooseFS as an EMR component without having to deploy it for the EMR environment separately.

For Tencent Cloud EMR clusters that have not integrated with GooseFS, you can refer to this document to deploy the EMR environment for GooseFS.

First, select a framework that suits the production environment by referring to [Cluster Deployment and Running](https://cloud.tencent.com/document/product/436/57224#.E9.9B.86.E7.BE.A4.E6.A8.A1.E5.BC.8F.E9.83.A8.E7.BD.B2.E8.BF.90.E8.A1.8C) and then deploy the cluster.
After that, configure according to the GooseFS-supportive EMR component. This document describes the configuration for Hadoop MapReduce, Spark, and Flink supports.

## Hadoop MapReduce Support

To allow Hadoop MapReduce jobs to read and write GooseFS data, add the GooseFS client’s dependent path to `HADOOP_CLASSPATH` in `hadoop-env.sh`. This can be performed in the EMR console as follows:

![](https://main.qcloudimg.com/raw/dd28fc42063509d5a43dc219ab4637b1.png)

Then, configure the HCFS implementation of GooseFS in `core-site.xml` in the EMR console.

Configure `fs.AbstractFileSystem.gfs.impl` as follows:
```
com.qcloud.cos.goosefs.hadoop.GooseFileSystem
```

![](https://main.qcloudimg.com/raw/4475c860359ad9a6b2305c2100b399a6.png)

Configure `fs.gfs.impl` as follows:
```
com.qcloud.cos.goosefs.hadoop.FileSystem
```

![](https://main.qcloudimg.com/raw/53adde8f2bbd97d17b10dc277b2395b4.png)


After the configurations are delivered, you can restart YARN-related components for the configurations to take effect.


## Spark Support

To allow Spark to access GooseFS, you also need to set `spark.executor.extraClassPath` to the GooseFS client’s dependency package in the `spark-defaults.conf` file as follows:

```conf
...
spark.driver.extraClassPath ${GOOSEFS_HOME}/client/goosefs-x.x.x-client.jar
spark.executor.extraClassPath ${GOOSEFS_HOME}/client/goosefs-x.x.x-client.jar
spark.hadoop.fs.gfs.impl com.qcloud.cos.goosefs.hadoop.FileSystem
spark.hadoop.fs.AbstractFileSystem.gfs.impl com.qcloud.cos.goosefs.hadoop.GooseFileSystem
...
```

This configuration can also be done and delivered on the Spark component configuration page in the EMR console 

![](https://main.qcloudimg.com/raw/6bf4295b7bbddf2e11108e2cec52e4ee.png)

## Flink Support

EMR’s Flink adopts the Flink on YARN deployment mode. Therefore, you need to ensure that `fs.hdfs.hadoopconf` is set to the Hadoop configuration path in `${FLINK_HOME}/flink-conf.yaml`. For Tencent Cloud EMR clusters, the value is `/usr/local/service/hadoop/etc/hadoop` in most cases.

You don’t need to configure other configuration items. You can use Flink on YARN to submit the Flink jobs, which can access GooseFS through `gfs://master:port/<path>`.


>! If Flink needs to access GooseFS, the master and port must be specified.
>

## Hive, Impala, HBase, Sqoop, and Oozie Support

If the environment support for Hadoop MapReduce has been configured, components such as Hive, Impala, and HBase can be used directly without requiring separate configuration.
  
