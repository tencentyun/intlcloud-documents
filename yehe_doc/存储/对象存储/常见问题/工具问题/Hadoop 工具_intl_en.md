### What is Hadoop-COS?
Hadoop-COS is a tool that helps integrate big-data computing frameworks including Apache Hadoop, Spark and Tez. It allows you to read and write Tencent Cloud COS data just as you do with HDFS. It can also be used as Deep Storage for Druid and other query and analysis engines.

### How do I set a reasonable block (part) size for multipart uploads via Hadoop-COS?
Hadoop-COS uploads large files to COS via concurrent uploads of multiple blocks (parts), you can control the size of each block (part) by configuring `fs.cosn.block.size(Byte)`.

Because a COS multipart upload can support the upload of at most 10,000 parts, when choosing the block size, you need to estimate the largest possible single file size that you may need to upload. For example, with a block size of 8 MB, you can upload a single file of up to 78 GB in size. A maximum block size of 2GB is supported, meaning that the largest singe file size supported is 19 TB. A 400 error will be thrown if the number of blocks exceeds 10,000. If you encounter said error, please check if you have configured this parameter correctly.

### Why is a 503 error thrown?
In big data scenarios, a high level of concurrency may trigger the COS frequency control policy, resulting in a 503 `Reduce your request rate` error exception. You can initiate retries for the failed requests by configuring the `fs.cosn.maxRetries` parameter, which defaults to a maximum of 200 retries.

### Why does my bandwidth limit setting seem to be ineffective?
The bandwidth limit setting `fs.cosn.traffic.limit(b/s)` is supported only by the latest versions of Hadoop-COS with a tag of 5.8.3 or above. For more information, see [Hadoop-COS on Github](https://github.com/tencentyun/hadoop-cos).

### Why can’t I see a large file immediately after it was uploaded to COS?
Hadoop-COS uploads all large files, i.e. those larger than the block size (fs.cosn.upload.part.size), through multipart upload. You can see the file on COS only after all of its parts have been uploaded. Currently, COS does not support Append operations.

### Which Buffer type should I choose for upload? What’s the difference between them?
You can choose a buffer type by setting `fs.cosn.upload.buffer` to one of the following 3 values:
 - mapped_disk (default): You need to place `fs_cosn.tmp.dir` under directory large enough to avoid a full disk runtime.
 - direct_memory: Uses JVM off-heap memory (out of JVM control; not recommended)
 - non_direct_memory: Uses JVM on-heap memory; We recommend configuring it to 128 M

### Why do I get the following error message when I set buffer type to `mapped_disk`: create buffer failed. buffer type: mapped_disk, buffer factory:org.apache.hadoop.fs.buffer.CosNMappedBufferFactory?

**Possible cause**
You do not have read or write permission for the temporary directory used by Hadoop-COS. The directory used by default is `/tmp/hadoop_cos`, and can be customized by configuring `fs.cosn.tmp.dir`.

**Solution**
Obtain read and write permission for the temporary directory used by Hadoop-COS.

### Why do I receive the following message during loading, prompting me that the class CosFileSystem was not found: “Error: java.lang.RuntimeException: java.lang.ClassNotFoundException: Class org.apache.hadoop.fs.CosFileSystem not found”?

**Possible cause**
The configuration has been loaded correctly, but `hadoop classpath` does not include the location of Hadoop-COS jar.

**Solution**
Load the location of Hadoop-COS jar to `hadoop classpath`.


### Why am I prompted that the class CosFileSystem was not found when I use Apache Hadoop?

COS offers 2 versions: Apache Hadoop and Hadoop-COS, which differ in the configuration of `fs.cosn.impl` and `fs.AbstractFileSystem.cosn.impl`.
- Apache Hadoop:
```xml
<property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.cosn.CosNFileSystem</value>
</property>
<property>
        <name>fs.AbstractFileSystem.cosn.impl</name>
        <value>org.apache.hadoop.fs.cosn.CosN</value>
</property>
```
- Tencent COS:
```xml
<property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosFileSystem</value>
</property>
<property>
        <name>fs.AbstractFileSystem.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosN</value>
</property>
```


### What should I do if the following exception is thrown when I perform computing tasks: java.net.ConnectException: Cannot assign requested address (connect failed) (state=42000,code=40000)?

Generally, this exception occurs when you have established too many TCP non-persistent connections in a short period of time. After the connections are closed, local ports will enter a 60-second timeout period by default instead of being immediately repossessed. During the timeout period, there will be no ports available to establish a socket connection with the server.

**Solution**

Modify the `/etc/sysctl.conf` file with changes to the following kernel parameters:
```conf
net.ipv4.tcp_timestamps = 1     #Enables support for TCP timestamp
net.ipv4.tcp_tw_reuse = 1       #Supports the use of a socket in the TIME_WAIT status to form a new TCP connection
net.ipv4.tcp_tw_recycle = 1     #Enables quick repossession of a socket in the TIME-WAIT status
net.ipv4.tcp_syncookies=1       #Enables SYN Cookies. The default value is 0. When the SYN waiting queue overflows, cookies are enabled to prevent a small number of SYN attacks.
net.ipv4.tcp_fin_timeout = 10              #Waiting time after the port is released.
net.ipv4.tcp_keepalive_time = 1200           #The time interval between which TCP sends KeepAlive messages. The default value is 2 hours. Change it to 20 minutes.
net.ipv4.ip_local_port_range = 1024 65000    #The range of ports for external connections. The default value is 32768 to 61000. Change it to 1024 to 65000.
net.ipv4.tcp_max_tw_buckets = 10240          #The maximum number (default: 180000) of sockets in the TIME_WAIT status. Exceeding this number will directly release all the new TIME_WAIT sockets. You may consider reducing this parameter for a smaller number of sockets in the TIME_WAIT status.
```


### When I upload a file, why does the exception “java.lang.Thread.State: TIME_WAITING (parking)” occur with “org.apache.hadoop.fs.BufferPoll.getBuffer” and “java.util.concurrent.locks.LinkedBlockingQueue.poll” locked in the stack?

**Possible cause**

You may have repeatedly initialized the buffer without actually triggering the write operation.

**Solution**

Change the configuration to the following:
```xml
<property>
        <name>fs.cosn.upload.buffer</name>
        <value>mapped_disk</value>
</property>
<property>
        <name>fs.cosn.upload.buffer.size</name>
        <value>-1</value>
</property>
```

### How do I use the Hadoop-COS jar file for self-built Hadoop?
Edit the Hadoop-COS POM file to make sure its version is the same as that of Hadoop. Next, put the Hadoop-COS jar and COS JAVA SDK jar files in the directory `hadoop/share/hadoop/common/lib`. For more information, see [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884).


