## Feature Description
Software configuration enables you to customize configurations of components such as HDFS, YARN, and Hive when creating a cluster.
## Custom Software Configuration
Software programs such as Hadoop and Hive have many configuration items. By using the software configuration feature, you can customize component parameters when creating a cluster. During the configuration, you need to provide the corresponding JSON files as required. You can customize the files or generate them by exporting software configuration parameters of an existing cluster for quick cluster creation. For more information on how to export software configuration parameters, please see [Exporting Software Configuration](https://intl.cloud.tencent.com/document/product/1026/34522).
>Currently, only parameters in the following files can be customized:
HDFS: core-site.xml, hdfs-site.xml, hadoop-env.sh, log4j.properties
YARN: yarn-site.xml, mapred-site.xml, fair-scheduler.xml, capacity-scheduler.xml, yarn-env.sh, mapred-env.sh
Hive: hive-site.xml, hive-env.sh, hive-log4j2.properties

**Sample JSON file and description:**

```
[
    {
        "serviceName": "HDFS",
        "classification": "hdfs-site.xml",
        "serviceVersion": "2.8.4",
        "properties": {
            "dfs.blocksize": "67108864",
            "dfs.client.slow.io.warning.threshold.ms": "900000",
            "output.replace-datanode-on-failure": "false"
        }
    },
    {
        "serviceName": "YARN",
        "classification": "yarn-site.xml",
        "serviceVersion": "2.8.4",
        "properties": {
            "yarn.app.mapreduce.am.staging-dir": "/emr/hadoop-yarn/staging",
            "yarn.log-aggregation.retain-check-interval-seconds": "604800",
            "yarn.scheduler.minimum-allocation-vcores": "1"
        }
    },
    {
        "serviceName": "YARN",
        "classification": "capacity-scheduler.xml",
        "serviceVersion": "2.8.4",
        "properties": {
            "content": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<?xml-stylesheet type=\"text/xsl\" href=\"configuration.xsl\"?>\n<configuration><property>\n        <name>yarn.scheduler.capacity.maximum-am-resource-percent</name>\n        <value>0.8</value>\n</property>\n<property>\n        <name>yarn.scheduler.capacity.maximum-applications</name>\n        <value>1000</value>\n</property>\n<property>\n        <name>yarn.scheduler.capacity.root.default.capacity</name>\n        <value>100</value>\n</property>\n<property>\n        <name>yarn.scheduler.capacity.root.default.maximum-capacity</name>\n        <value>100</value>\n</property>\n<property>\n        <name>yarn.scheduler.capacity.root.default.user-limit-factor</name>\n        <value>1</value>\n</property>\n<property>\n        <name>yarn.scheduler.capacity.root.queues</name>\n        <value>default</value>\n</property>\n</configuration>"
        }
    }
]
```

**Configuration parameter description:**
- serviceName: component name, which must be in uppercase.
- classification: filename, which must be a full name with file extension.
- serviceVersion: component version, which must be the same as the corresponding component version in the EMR product version.
- properties: parameters that need to be customized.
- If you want to modify configuration parameters in `capacity-scheduler.xml` or `fair-scheduler.xml`, set `key` in `properties` to `content`, and set `value` to the content of the entire file.

If you want to adjust the component configuration of an existing cluster, you can [configure component parameters](https://intl.cloud.tencent.com/document/product/1026/31109).

## Accessing External Clusters
After configuring the HDFS access address information of an external cluster, you can read data in it.

### Configuration during purchase

EMR allows you to configure access to external clusters when you create an EMR cluster. On the [purchase page](https://buy.cloud.tencent.com/emapreduce#/), you only need to import a JSON file that meets the requirements in the software configuration section. Below is an example based on assumption:

**Assumption**
Assume that the `nameservice` of the external cluster to be accessed is `HDFS8088`, and the access method is as follows:

```
<property>
    <name>dfs.ha.namenodes.HDFS8088</name>
    <value>nn1,nn2</value>
</property>
<property>
    <name>dfs.namenode.http-address.HDFS8088.nn1</name>
    <value>172.21.16.11:4008</value>
</property>
<property>
    <name>dfs.namenode.https-address.HDFS8088.nn1</name>
    <value>172.21.16.11:4009</value>
</property>
    <name>dfs.namenode.rpc-address.HDFS8088.nn1</name>
    <value>172.21.16.11:4007</value>
<property>
    <name>dfs.namenode.http-address.HDFS8088.nn2</name>
    <value>172.21.16.40:4008</value>
</property>
<property>
    <name>dfs.namenode.https-address.HDFS8088.nn2</name>
    <value>172.21.16.40:4009</value>
</property>
<property>
	<name>dfs.namenode.rpc-address.HDFS8088.nn2</name>
	<value>172.21.16.40:4007</value>
<property>
```

If you want to access the external cluster in the newly created cluster, enter the [purchase page](https://buy.cloud.tencent.com/emapreduce#/) and expand the advanced settings.
![](https://main.qcloudimg.com/raw/f964877122db0e9b5f6f68d7b1e9e6f6.png)

**JSON file and description:**
Taking the assumption as an example, import the JSON file (the requirements for its content are the same as those for custom software configuration) in the box.
```
[
    {
        "serviceName": "HDFS",
        "classification": "hdfs-site.xml",
        "serviceVersion": "2.7.3",
        "properties": {
            "newNameServiceName": "newEmrCluster",
            "dfs.ha.namenodes.HDFS8088": "nn1,nn2",
            "dfs.namenode.http-address.HDFS8088.nn1": "172.21.16.11:4008",
            "dfs.namenode.https-address.HDFS8088.nn1": "172.21.16.11:4009",
            "dfs.namenode.rpc-address.HDFS8088.nn1": "172.21.16.11:4007",
            "dfs.namenode.http-address.HDFS8088.nn2": "172.21.16.40:4008",
            "dfs.namenode.https-address.HDFS8088.nn2": "172.21.16.40:4009",
            "dfs.namenode.rpc-address.HDFS8088.nn2": "172.21.16.40:4007"
        }
}
]
```

#### Configuration parameter description
- serviceName: component name, which must be "HDFS".
- classification: filename, which must be "hdfs-site.xml".
- serviceVersion: component version, which must be the same as the corresponding component version in the EMR product version.
- properties: the content must be the same as that in the assumption.
- newNameServiceName: it indicates the `nameservice` of the newly created cluster, which is optional. If this parameter is left empty, its value will be generated by the system; if it is not empty, its value must consist of a string, digits, and hyphen.

> Access to external clusters is supported only for high-availability clusters.
> Access to external clusters is supported only for clusters with Kerberos disabled.

### Configuration after purchase

EMR allows you to use the [configuration distribution](https://intl.cloud.tencent.com/document/product/1026/31109) feature to access external clusters after creating an EMR cluster.
Below is the assumption:
Assume that the `nameservcie` of the cluster is `HDFS80238` (if it is not a high-availability cluster, the `nameservcie` will usually be `masterIp:rpcport`, such as 172.21.0.11:4007).
The `nameservice` of the external cluster to be accessed is `HDFS8088`, and the access method is as follows:

```
<property>
    <name>dfs.ha.namenodes.HDFS8088</name>
    <value>nn1,nn2</value>
</property>
<property>
        <name>dfs.namenode.http-address.HDFS8088.nn1</name>
        <value>172.21.16.11:4008</value>
</property>
<property>
        <name>dfs.namenode.https-address.HDFS8088.nn1</name>
        <value>172.21.16.11:4009</value>
</property>
 <name>dfs.namenode.rpc-address.HDFS8088.nn1</name>
        <value>172.21.16.11:4007</value>
        
        <property>
        <name>dfs.namenode.http-address.HDFS8088.nn2</name>
        <value>172.21.16.40:4008</value>
</property>
<property>
        <name>dfs.namenode.https-address.HDFS8088.nn2</name>
        <value>172.21.16.40:4009</value>
</property>
<property>
		<name>dfs.namenode.rpc-address.HDFS8088.nn2</name>
		<value>172.21.16.40:4007</value>
<property>

```

If the information above is in the EMR cluster, you can view it on the management page of [configuration distribution](https://intl.cloud.tencent.com/document/product/1026/31109) or log in to the server to view the `/usr/local/service/hadoop/etc/hadoop/hdfs-site.xml` file.
1. Enter the [Configuration Distribution](https://intl.cloud.tencent.com/document/product/1026/31109) page and select the `hdfs-site.xml` file of the HDFS component.
2. Change the value of the configuration item `dfs.nameservices` to `HDFS80238,HDFS8088`.
3. Add configuration items and their values.
<table>
<tr>
<th>Configuration Item  </th>
<th>Value</th>
</tr>
<tr>
<td> dfs.ha.namenodes.HDFS8088</td>
<td>nn1,nn2 </td>
</tr>
<tr>
<td>fs.namenode.http-address.HDFS8088.nn1</td>
<td>172.21.16.11:4008  </td>
</tr>
<tr>
<td> dfs.namenode.https-address.HDFS8088.nn1 </td>
<td> 172.21.16.11:4009    </td>
</tr>
<tr>
<td>dfs.namenode.rpc-address.HDFS8088.nn1</td>
<td>172.21.16.11:4007</td>
</tr>
<tr>
<td>fs.namenode.http-address.HDFS8088.nn2</td>
<td>172.21.16.40:4008</td>
</tr>
<tr>
<td>dfs.namenode.https-address.HDFS8088.nn2</td>
<td>172.21.16.40:4009</td>
</tr>
<tr>
<td> dfs.namenode.rpc-address.HDFS8088.nn2</td>
<td>172.21.16.40:4007</td>
</tr>
<tr>
<td>dfs.client.failover.proxy.provider.HDFS8088</td>
<td>org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider</td>
</tr>
<tr>
<td>dfs.internal.nameservices</td>
<td>HDFS80238 </td>
</tr>
</table>

> `dfs.internal.nameservice` needs to be added; otherwise, if the cluster is scaled out, the "datanode" may report an error and be marked as "dead" by the `namenode`.
>
4. Distribute the configuration by using the [Configuration Distribution](https://intl.cloud.tencent.com/document/product/1026/31109) feature.

For more information on relevant configurations and principles, please see the [community documentation](https://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-hdfs/Federation.html).



