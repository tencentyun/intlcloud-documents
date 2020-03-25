- Use Apache Phoenix Salted Table

    HBase sequential write may suffer from region server hotspotting if your row key is monotonically increasing. Phoenix provides a way to transparently salt the row key with a salting byte for a particular table. You need to specify this in table creation time by specifying a table property “SALT_BUCKETS” with a value from 1 to 256. Like this:
``` sql
   0: jdbc:phoenix:>CREATE TABLE table (a_key VARCHAR PRIMARY KEY, a_col VARCHAR) SALT_BUCKETS = 20;
```
    Salting the row key provides a way to mitigate the problem caused by HBase sequential write. With salted tables, you don’t need to be knowledgeable about the row key design in HBase. Below is Phoenix's official performance comparison of read and write performance between salted and non-salted tables:
	![Salted table performance](https://mc.qcloudimg.com/static/img/8381e5a72ea654a488dd29b5d0effccf/5-4-4.png)  

 For more information on salting performance or directions, please see the [community documentation for salted tables in Phoenix](http://phoenix.apache.org/salted.html).

- Apache Phoenix Secondary Indexing
    Secondary indexes are an orthogonal way to access data from its primary access path. In HBase, you have a single index that is lexicographically sorted on the primary row key. Access to records in any way other than through the primary row requires scanning over potentially all the rows in the table to test them against your filter. With secondary indexing, the columns or expressions you index form an alternate row key to allow point lookups and range scans along this new axis.

- Configure Secondary Indexing in Apache Phoenix
    Phoenix on EMR supports Phoenix's secondary indexing. If you need to use non-transactional, variable indexing, just follow the steps below to configure it. Go to the component management page in the EMR Console, click **HBase**, select **Configuration** > **Configuration Management**, and add three configuration items in hbase-site.xml: `hbase.regionserver.wal.codec`, `hbase.region.server.rpc.scheduler.factory.class`, and `hbase.rpc.controllerfactory.class`. The detailed configuration is as follows:

    ```xml
    <property>
      <name>hbase.regionserver.wal.codec</name>
      <value>org.apache.hadoop.hbase.regionserver.wal.IndexedWALEditCodec</value>
      </property>
    <property>
      <name>hbase.region.server.rpc.scheduler.factory.class</name>
      <value>org.apache.hadoop.hbase.ipc.PhoenixRpcSchedulerFactory</value>
      <description>Factory to create the Phoenix RPC Scheduler that uses separate queues for index and metadata updates</description>
    </property>
    <property>
      <name>hbase.rpc.controllerfactory.class</name>
      <value>org.apache.hadoop.hbase.ipc.controller.ServerRpcControllerFactory</value>
      <description>Factory to create the Phoenix RPC Scheduler that uses separate queues for index and metadata updates</description>
    </property>
    ```

- Use secondary indexing in Phoenix

    Create a secondary index, such as:
    
    ``` sql
    0: jdbc:phoenix:>CREATE INDEX my_index ON my_table (v1) INCLUDE (v2)；
    ```
    
For more information on secondary indexing, please see the [community documentation of Phoenix secondary indexing](http://phoenix.apache.org/secondary_indexing.html).
