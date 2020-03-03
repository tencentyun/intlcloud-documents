## Feature Overview
Spark on YARN uses YARN as the resource scheduler. In Hadoop version above 2.7.2, YARN is equipped with Label Scheduler in addition to Capacity Scheduler.

Capacity Scheduler is a multi-tenant resource scheduler. Its core principle is that the available resources in a Hadoop cluster are shared by multiple organizations, which collectively provide computing power to the cluster based on their own computing needs. Capacity Scheduler has various features such as hierarchical queuing, capacity guarantee, security, elastic resource, multi-tenancy, resource-based scheduling, and mapping. All resources of the cluster are allocated to multiple queues. All applications submitted to a queue can use the resources allocated to the queue. Idle resources of other organizations can be non-preemptively allocated to applications running in queues where resources are not fully utilized, ensuring that the resource requirements of different applications can be met flexibly while applications can get the minimum resources required.

Capacity Scheduler roughly allocates cluster resources to different queues and cannot specify the running locations of applications in queues. Based on Capacity Scheduler, Label Scheduler adds different node labels to each node in the cluster for more fine-grained resource division, so that running locations of applications can be specified. Node labels have the following characteristics:
1. One node has only one node label (i.e., belonging to only one node partition). A cluster can be divided into multiple disjoint subclusters based on node partitioning.
2. There are two types of node partitions based on the match policy: exclusive and non-exclusive. An exclusive node partition will allocate containers to nodes that exactly match the node partition, while a non-exclusive node partition shares idle resources to containers requesting the default partition.
3. You can set accessible node labels for each queue to specify the node partitions for running applications.
4. You can set the resource ratio of different queues in each node partition.
5. If the required node label is specified in a resource request, the request will only be allocated to nodes with the same label. If the node label is not specified (you can use a configuration item to rename the default label of a queue), the request will only be allocated to nodes in the default partition.

## Configuration Description
### 1. Enable Capacity Scheduler in ResourceManager
Label Scheduler cannot be used alone; instead, it must be used together with Capacity Scheduler, which is the default scheduler of YARN. If you are using another scheduler, please enable Capacity Scheduler first in `${HADOOP_HOME}/etc/hadoop/yarn-site.xml`:
```
<property>
	<name>yarn.resourcemanager.scheduler.class</name>
	<value>org.apache.hadoop.yarn.server.resourcemanager.scheduler.capacity.CapacityScheduler</value>
</property>
```
### 2. Configure Capacity Scheduler parameters
In `${HADOOP_HOME}/etc/hadoop/capacity-scheduler.xml`, set `yarn.scheduler.capacity.root` as the predefined root queue of Capacity Scheduler. All other queues are subqueues of the root queue. All queues are organized in a tree structure. `yarn.scheduler.capacity.<queue-path>.queues` is used to set the subqueues under the `queue-path` path, with subqueues separated by commas.

**Example:**
![](https://main.qcloudimg.com/raw/6e0b2a4713f76cafeaf60533897e4266.png)
**The structure shown above is configured as follows:**
```
<property>
	<name>yarn.scheduler.capacity.root.queues</name>
	<value>q1,q2,q3</value>
</property>
<property>
	<name>yarn.scheduler.capacity.root.q1.queues</name>
	<value>q11,q12</value>
</property>
<property>
	<name>yarn.scheduler.capacity.root.q2.queues</name>
	<value>q21,q22</value>
</property>
```
For other Capacity Scheduler configuration items, please see the relevant documentation.
### 3. Enable node label in ResourceManager
Set it in `conf/yarn-site.xml`.
```
<property>
	<name>yarn.node-labels.fs-store.root-dir</name>
	<value>hdfs://namenode:port/path-to-store/node-labels/</value>
</property>
<property>
	<name>yarn.node-labels.enabled</name>
	<value>true</value>
</property>
<property>
	<name>yarn.node-labels.configuration-type</name>
	<value>centralized or delegated-centralized or distributed</value>
</property>
```
>
1. Make sure that `yarn.node-labels.fs-store.root-dir` has been created and ResourceManager has the permission to access it.
2. You can store node labels in the local file system of ResourceManager at a path such as `file://home/yarn/node-label`; however, in order to ensure high availability of the cluster and avoid loss of label information due to ResourceManager failures, you are recommended to store the label information in HDFS.
3. In Hadoop 2.8.2, you need to configure the `yarn.node-labels.configuration-type` configuration item.

### 4. Configure node label
Set it in `etc/hadoop/capacity-scheduler.xml`.

| Configuration Item | Description | 
|---------|---------| 
| yarn.scheduler.capacity.`<queue-path>`.capacity | It specifies the percentage of nodes in the default partition that a queue can access. **The total capacity of the default partition for all subqueues under the parent queue must be 100.** |  
| yarn.scheduler.capacity.`<queue-path>`.accessible-node-labels  | It specifies the list of labels that a queue can access, and labels should be separated by commas. For example, "HBASE,STORM" means that the queue can access the labels "HBASE" and "STORM". All queues can access nodes with no label. If this field is not set, it will inherit the value of its parent field. If you want a queue to access only nodes with no label, leave this field empty.  |
| yarn.scheduler.capacity.`<queue-path>`.accessible-node-labels.`<label>`.capacity  | It specifies the percentage of nodes in the `<label>` partition that a queue can access. Note that the total capacity of the `<label>` partition for all subqueues under the parent queue must be 100. The default value of this configuration item is 0. |
| yarn.scheduler.capacity.`<queue-path>`.accessible-node-labels.`<label>`.maximum-capacity  | Similar to the `yarn.scheduler.capacity.`<queue-path>`.maximum-capacity` configuration item in Capacity Scheduler, it specifies the maximum capacity of `<queue-path>` in the `<label>` partition. The default value of this configuration item is 100.  |
| yarn.scheduler.capacity.`<queue-path>`.default-node-label-expression  | If a resource request does not have a node label specified, the application will be submitted to the corresponding partition specified by this configuration item. By default, this value is empty, i.e., applications will be allocated to containers in nodes with no label.  |

## Use Cases
### Preparations
1. Prepare a cluster
Confirm that you have activated Tencent Cloud and created an EMR cluster.
2. Check configuration of the YARN component
On the "Component Management" page, select the YARN component to enter its component management page. On the role management tab, confirm the IP of the node where the ResourceManager service resides. Then, switch to the configuration management tab to modify relevant parameters in `yarn-site.xml`, save the changes, and restart all YARN components.
 1. Enter the YARN component management page.
![](https://main.qcloudimg.com/raw/b938adde4eb5b330a11e25bba77a3ca0.png)
 2. Confirm the IP address of ResourceManager.
 ![](https://main.qcloudimg.com/raw/682dafc75d3bc59d1d739ddc437c427f.png)
 3. Modify the `yarn.resourcemanager.scheduler.class` parameter in `yarn-site.xml` of the node where ResourceManager resides.
 ![](https://main.qcloudimg.com/raw/fca9010a03c4a11071c1251a7873ed49.png)

### Configuring the mappings and ratios of node labels and queues in Capacity-Scheduler.xml
1. Create an HDFS directory for storing node labels.
![](https://main.qcloudimg.com/raw/5fadfe11a03a36a7022c3041f80be43a.png)
2. Get the IP and port of ResourceManager in `core-site.xml`.
![](https://main.qcloudimg.com/raw/80adfada78e73691ad073b97cd28a7ad.png)
3. In `yarn-site.xml` of the master node, create a configuration item. Then, restart ResourceManager.
![](https://main.qcloudimg.com/raw/7e4b2a8f096cdbdedc5718828bbdfa5f.png)
4. Run the `yarn rmadmin -addToClusterNodeLabels` command to add labels.
![](https://main.qcloudimg.com/raw/c23e4f3fb2d81cf21da40d6cdec3c6e5.png)
 Enter the WebUI of the YARN component. You can view all labels of the cluster in the "NodeLabels" panel.
![](https://main.qcloudimg.com/raw/6e9a88107651955f1e6b9b783b85bf4b.png)
5. Run the `yarn rmadmin -replaceLabelsOnNode` command to add labels to nodes.
![](https://main.qcloudimg.com/raw/6824f8a6eed39c25bb127a532ed615b3.png)
	As can be seen in the "NodeLabels" panel, the number of nodes in the "normal" and "cpu" partitions has become 1 from 0.
![](https://main.qcloudimg.com/raw/45e47b8fa8f27246dc77cbcc94e8a332.png)
 As can be seen in the "Scheduler" panel, the labels of the two nodes in the testing system have changed.
![](https://main.qcloudimg.com/raw/0388a5e8ecf0a148ad5985080a04e145.jpg)
6. Edit configuration items in `Capacity-Scheduler.xml` to configure the cluster queues, resource ratio of queues, and accessible labels of queues as shown in the following sample:
```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration><property>
        <name>yarn.scheduler.capacity.maximum-am-resource-percent</name>
        <value>0.8</value>
</property>
<property>
        <name>yarn.scheduler.capacity.maximum-applications</name>
        <value>1000</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.queues</name>
        <value>default,dev,product</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.default.capacity</name>
        <value>20</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.dev.capacity</name>
        <value>40</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.product.capacity</name>
        <value>40</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.accessible-node-labels.cpu.capacity</name>
        <value>100</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.accessible-node-labels.normal.capacity</name>
        <value>100</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.accessible-node-labels</name>
        <value>*</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.dev.accessible-node-labels.normal.capacity</name>
        <value>100</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.dev.accessible-node-labels.cpu.capacity</name>
        <value>100</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.dev.accessible-node-labels</name>
        <value>normal</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.dev.default-node-label-expression</name>
        <value>normal</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.product.accessible-node-labels</name>
        <value>cpu</value>
</property>
<property>
        <name>yarn.scheduler.capacity.root.product.default-node-label-expression</name>
        <value>cpu</value>
</property>
<property>
        <name>yarn.scheduler.capacity.normal.sharable-partitions</name>
        <value>cpu</value>
</property>
<property>
        <name>yarn.scheduler.capacity.normal.require-other-partition-resource</name>
        <value>true</value>
</property>
<property>
        <name>yarn.scheduler.capacity.cpu.sharable-partitions</name>
        <value></value>
</property>
<property>
        <name>yarn.scheduler.capacity.cpu.require-other-partition-resource</name>
        <value>true</value>
</property>
</configuration>
```
The "Scheduler" panel displays the 3 partitions of the testing cluster, resource allocation of partitions, and information of included queues. In the "Application Queues" panel, there are 3 partitions: default, normal, and cpu, among which the "default" partition is the default one, the "normal" partition consists of nodes with the "normal" label, and the "cpu" partition consists of nodes with the "cpu" label. In the testing environment, there are two nodes which are labeled as "normal" and "cpu", respectively. You can click "+" on the left of a partition to expand all queues in it.
![](https://main.qcloudimg.com/raw/fa2c002eb9337425c2db519126825db8.png)

## Testing Label Scheduling
- **Test 1. Submit a job to the "product" queue**
```
[hadoop@172 hadoop]$ cd /usr/local/service/hadoop
[hadoop@172 hadoop]$ yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-client-jobclient-2.8.4-tests.jar sleep -Dmapreduce.job.queuename=product -m 32 -mt 1000
```
After the job is submitted, the resource usage of queues in each partition is as shown below:
![](https://main.qcloudimg.com/raw/8a09009b52c529c01ed5b61b024334f6.png)
**Conclusion:** there is a mapping between the "product" queue and the "cpu" label, the default label is "cpu", and the job submitted to the "product" queue runs on the node with the "cpu" label.
- **Test 2. Submit a job to the "dev" queue**
```
[hadoop@172 hadoop]$ cd /usr/local/service/hadoop
[hadoop@172 hadoop]$ yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-client-jobclient-2.8.4-tests.jar sleep -Dmapreduce.job.queuename=dev -m 32 -mt 1000
```
After the job is submitted, the resource usage of queues in each partition is as shown below:
![](https://main.qcloudimg.com/raw/31ea0a2009764d5b14d2c2bfac2769bf.png)
**Conclusion:** there is a mapping between the "dev" queue and the "normal" label, the default label is "normal", and the job submitted to the "dev" queue runs on the node with the "normal" label.
