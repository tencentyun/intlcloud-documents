By default, Hadoop stores YARN job logs in HDFS. Tencent Cloud EMR also provides the ability to store YARN job logs in external storage (COS).
## Prerequisites
The EMR cluster needs to support COS. For more information, please see [Analyzing Data in HDFS/COS with API](https://intl.cloud.tencent.com/document/product/1026/31128).

## Directions
1. Modify the configuration in `yarn-site.xml` and deliver the configuration to all nodes.
```
yarn.nodemanager.remote-app-log-dir=cosn://[bucket_name]/[logs_dirs]
```
2. Add a new configuration item to `core-site.xml` and deliver it to all nodes.
```
fs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.cosnative.COS
```
3. Restart all the `nodemanager/datanode` services in the cluster.
4. Run the `hive/spark` job to view the job logs stored in COS.
```
hdfs dfs -ls cosn://[bucket_name]/[logs_dirs] 
```
