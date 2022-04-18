Apache Hive introduced Live Long and Process (LLAP) on v2.0 and made great optimization on v2.1, which shows that Hive has evolved to memory computing. Currently, as tested by Hortonworks, LLAP working together with Tez is 25 times faster than Hive v1.x. LLAP provides a hybrid execution model consisting of a long-lived daemon which replaces direct interactions with the HDFS DataNode, and a tightly integrated DAG-based framework. For example, features such as caching, pre-fetching, certain query processing, and access control are moved into the daemon. Small/Short queries are largely processed by this daemon directly, while any heavy lifting will be performed in standard YARN containers.

## Hive LLAP Structure Diagram
![](https://main.qcloudimg.com/raw/c650eee1bc1019d8d7d3353b86a469ec.png)
- Persistent daemon
To facilitate caching and JIT optimization, and to eliminate most of the startup costs, a daemon runs on the worker nodes in the cluster. It handles I/O, caching, and query fragment execution.
- Execution engine
LLAP works within existing, process-based Hive execution to preserve the scalability and versatility of Hive. It does not replace the existing execution model but rather enhances it.
- Query fragment execution
LLAP nodes execute "query fragments" such as filters, projections, data transformations, partial aggregates, sorting, bucketing, and hash `joins/semi-joins`.
- I/O
The daemon off-loads I/O and transformation from compressed format to separate threads. The data is passed in to the execution as it becomes ready, so the previous batches can be processed while the next ones are being prepared. The data is passed in to the execution in a simple RLE-encoded columnar format that is ready for vectorized processing; this is also the caching format, with the intent to minimize replication between I/O, cache, and execution.
- Caching
The daemon caches metadata for input files, as well as the data. The metadata and index information can be cached even for data that is not currently cached.

## Installing Hive LLAP
1. Enter the EMR [purchase page](https://buy.cloud.tencent.com/emr).
2. Select `EMR-V2.3.0` as the product version.
3. Select **TEZ 0.9.2** in the **Optional Component** list, and Hive LLAP will be automatically installed in the `/usr/local/service/slider` directory.
 
## Using Hive LLAP
- Modify `/usr/local/service/slider/conf/slider-client.xml` by adding the following configuration items:
```
<property>
	<name>hadoop.registry.zk.quorum</name>
	<value>zk_ip:zk_port</value>
</property>
```
The IP in the `value` is the master node IP for a non-high-availability cluster. For a high-availability cluster, run the following command to view the ZooKeeper component IP:
```
cat /usr/local/service/hadoop/etc/hadoop/hdfs-site.xml |grep 2181
```
- Modify `hive-site.xml` (delivered in the console).
```
<property>
	<name>hive.execution.engine</name>
	<value>tez</value>
</property>
<property>
	<name>hive.llap.execution.mode</name>
	<value>all</value>
</property>
<property>
	<name>hive.execution.mode</name>
	<value>llap</value>
</property>
<property>
	<name>hive.llap.daemon.service.hosts</name>
	<value>@llap_service</value>
</property>
<property>
	<name>hive.zookeeper.quorum</name>
	<value>zk_ip:zk_port</value>
</property>
<property>
	<name>hive.llap.daemon.memory.per.instance.mb</name>
	<value>4000</value>
</property>
<property>
	<name>hive.llap.daemon.num.executors</name>
	<value>2</value>
</property>
<property>
	<name>hive.server2.tez.default.queues</name>
	<value>root.default</value>
</property>
<property>
	<name>hive.server2.tez.initialize.default.sessions</name>
	<value>true</value>
</property>
<property>
	<name>hive.server2.tez.sessions.per.default.queue</name>
	<value>2</value>
</property>
```
>!Here, you need to enter the actual ZooKeeper address and port in the `hive.zookeeper.quorum` configuration item.
>
 - Restart all Hive services.
 - Generate the LLAP start file and command.
```
hive --service llap --name llap_service --instances 2 --size 2g --loglevel INFO --cache 1g --executors 2 --iothreads 5 --slider-am-container-mb 1024 --args " -XX:+UseG1GC -XX:+ResizeTLAB -XX:+UseNUMA -XX:-ResizePLAB" 
```
Here, LLAP execution and configuration files will be generated in the current directory. Run the `run.sh` script as prompted as shown below:
![](https://main.qcloudimg.com/raw/3ed9ac7564736a89a2b17b972582af56.png)
```
llap-slider-27May2020/run.sh
```
Run the `run.sh` file above, and a resident application will be submitted in YARN. Wait for several minutes, and you can see the application in `yarn-ui`.
>?LLAP initialization will take several minutes. Wait until it ends before performing data operations.
- Verify LLAP.
Enter Hive CLI:
```
create table t1(id int, name string);
insert into t1 values('1','test1'),('2', 'test2');
select id, count(1) from t1 group by id;
```
Expected result:
![](https://main.qcloudimg.com/raw/e29c4a4032916bb0e00edca55876ebd0.png)






