## Description

Hadoop-COS implements a standard Hadoop file system based on Tencent Cloud COS. It supports the integration of COS with big data computing frameworks such as Hadoop, Spark and Tez, enabling them to read and write the data stored on COS as if they were accessing an HDFS file system.

Hadoop-COS uses cosn as a URI scheme, so it is often called CosN file system.

## Operating Environment

### System Environment

Hadoop-COS is supported on Linux, Windows and macOS operating systems.

### Software Requirements

Hadoop-2.6.0 or above.

## Download and Installation

### Obtain Hadoop-COS Plugin

Download the [Hadoop-COS plugin](https://github.com/tencentyun/hadoop-cos).

### Install the Hadoop-COS Plugin

1. Copy cos_hadoop_api-5.2.6.jar and hadoop-cos-2.X.X.jar in the dep directory to `$HADOOP_HOME/share/hadoop/tools/lib`.

> Select a jar package based on the Hadoop version. If no matching version of jar package is found in the dep directory, modify the Hadoop's version number in the pom file to recompile and generate a jar package. 

2. Modify the hadoop_env.sh File.
   Edit hadoop_env.sh under the `$HADOOP_HOME/etc/hadoop` directory. Add the following content and add the cosn-related jar packages to the Hadoop environment variable:

```shell
for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
  if [ "$HADOOP_CLASSPATH" ]; then
    export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
  else
    export HADOOP_CLASSPATH=$f
  fi
done
```

## Usage

### Configuration Items

| Attribute Key| Description| Default Value| Required|
| :---------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----: |
| fs.cosn.userinfo.secretId/secretKey | Enter the API key for your account. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) to view the cloud API key | None |Yes|
|    fs.cosn.credentials.provider     | Set how to get secret id and secret key. Three methods are available: 1. org.apache.hadoop.fs.auth.SessionCredentialProvider: get secret id and secret key from the request URI, with a format of cosn://{secretId}:{secretKey}@examplebucket-1250000000;/<br>2. org.apache.hadoop.fs.auth.SimpleCredentialProvider: Get secret id and secret key by reading fs.cosn.userinfo.secretId and fs.cosn.userinfo.secretKey from the configuration file core-site.xml;<br>3. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: Get them from the environment variables COS_SECRET_ID and COS_SECRET_KEY. | If this is not specified, they are read in the following order:<br>1.org.apache.hadoop.fs.auth.SessionCredentialProvider<br>2.org.apache.hadoop.fs.auth.SimpleCredentialProvider <br>3.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider | No |
|            fs.cosn.impl             | The implementation class of cosn in FileSystem, which is always org.apache.hadoop.fs.CosFileSystem. |None| Yes|
|   fs.AbstractFileSystem.cosn.impl   | The implementation class of cosn in AbstractFileSystem, which is always org.apache.hadoop.fs.CosN. |None |Yes|
|        fs.cosn.bucket.region        |Enter the region of the bucket to be accessed. The enumerated values are the region abbreviations in [Regions and Endpoints](https://cloud.tencent.com/document/product/436/6224), such as ap-beijing and ap-guangzhou. It is compatible with the original configuration: fs.cosn.userinfo.region |  None |Yes|
|   fs.cosn.bucket.endpoint_suffix    | Specify the COS endpoint to be connected (Optional). Public cloud-based COS users simply need to enter the above region correctly. It is compatible with the original configuration: fs.cosn.userinfo.endpoint_suffix | None | No |
|           fs.cosn.tmp.dir           | Set a directory that actually exists. Temporary files generated in the running process are stored in the directory.|                       /tmp/hadoop_cos                        | No|
|        fs.cosn.upload.buffer        | The type of buffer that the CosN file system depends on when uploading files. Three types of buffers are supported: non_direct_memory, direct_memory and mapped_disk. Non-direct memory buffer uses JVM on-heap memory, direct_memory buffer uses off-heap memory, and mapped_disk buffer is a buffer obtained based on memory file mapping. |                         mapped_disk                          | No|
|     fs.cosn.upload.buffer.size      | The size of the buffer that the CosN file system depends on when uploading files. A value of -1 means no limit. If you do not limit the buffer size, the buffer type must be mapped_disk. If you specify a size greater than 0, the value must equal at least one block size. It is compatible with the original configuration: fs.cosn.buffer.size |                       -1（unlimited）                        | No |
|         fs.cosn.block.size          | The size of each block in the CosN file system (size of each part in multipart upload). Since a maximum of 10,000 parts are allowed for a multipart upload in COS, you need to estimate the largest possible size of a single file to be used. For example, if the block size is 8 MB, the largest file that can be uploaded is 78 GB. The maximum block size is 2 GB, so the maximum file size allowed for upload is 19TB |8388608 (8 MB) |No|
|     fs.cosn.upload_thread_pool      | Number of threads running concurrently when files are uploaded to COS in a streaming way. | CPU cores*5 | No |
|      fs.cosn.copy_thread_pool       | Number of threads running concurrently when directories are copied. |CPU cores*3| No |
|    fs.cosn.read.ahead.block.size    | Pre-read block size                       | 1048576 (1 MB) |No |
|    fs.cosn.read.ahead.queue.size    |  Length of pre-read queue | 8 | No |
| fs.cosn.maxRetries | Maximum of retries allowed if an error occurs while accessing COS | 3 | No |
|   fs.cosn.retry.interval.seconds    | The time interval between retries | 3 | No |

### Configure Hadoop

Modify `$HADOOP_HOME/etc/hadoop/core-site.xml`, and add information of COS users and implementation classes, as shown below:

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>cosn://examplebucket-1250000000</value>
    </property>
  
    <property>
        <name>fs.cosn.credentials.provider</name>
        <value>org.apache.hadoop.fs.auth.SimpleCredentialProvider</value>
        <description>

            This option allows the user to specify how to get the credentials.
            Comma-separated class names of credential provider classes which implement
            com.qcloud.cos.auth.COSCredentialsProvider:

            1.org.apache.hadoop.fs.auth.SessionCredentialProvider: Obtain the secret id and secret key from the URI: cosn://secretId:secretKey@examplebucket-1250000000/;
            2.org.apache.hadoop.fs.auth.SimpleCredentialProvider: Obtain the secret id and secret key
            from fs.cosn.userinfo.secretId and fs.cosn.userinfo.secretKey in core-site.xml;
            3.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: Obtain the secret id and secret key
            from system environment variables named COS_SECRET_ID and COS_SECRET_KEY.

            If unspecified, the default order of credential providers is:
            1. org.apache.hadoop.fs.auth.SessionCredentialProvider
            2. org.apache.hadoop.fs.auth.SimpleCredentialProvider
            3. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider

        </description>
    </property>
  
    <property>
        <name>fs.cosn.userinfo.secretId</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxxxx</value>
        <description>Tencent Cloud Secret Id</description>
    </property>
      
    <property>
        <name>fs.cosn.userinfo.secretKey</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxxx</value>
        <description>Tencent Cloud Secret Key</description>
    </property>
      
    <property>
        <name>fs.cosn.bucket.region</name>
        <value>ap-xxx</value>
        <description>The region where the bucket is located.</description>
    </property>
      
    <property>
        <name>fs.cosn.bucket.endpoint_suffix</name>
        <value>cos.ap-xxx.myqcloud.com</value>
        <description>
          COS endpoint to connect to. 
          For public cloud users, it is recommended not to set this option, and only the correct area field is required.
        </description>
    </property>
      
    <property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosFileSystem</value>
        <description>The implementation class of the CosN Filesystem.</description>
    </property>
      
    <property>
        <name>fs.AbstractFileSystem.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosN</value>
        <description>The implementation class of the CosN AbstractFileSystem.</description>
    </property>

    <property>
        <name>fs.cosn.tmp.dir</name>
        <value>/tmp/hadoop_cos</value>
        <description>Temporary files will be placed here.</description>
    </property>
  
    <property>
      <name>fs.cosn.upload.buffr</name>
      <value>mapped_disk</value>
      <description>The type of upload buffer. Available values: non_direct_memory, direct_memory, mapped_disk.</description>
    </property>
    
    <property>
    	<name>fs.cosn.upload.buffer.size</name>
        <value>33554432</value>
        <description>The total size of the buffer pool.</description>
    </property>
      
    <property>
    	<name>fs.cosn.block.size</name>
        <value>8388608</value>
        <description>Block size to use cosn filesysten, which is the part size for MultipartUpload.
        Considering the COS supports up to 10000 blocks, user should estimate the maximum size of a single file.
        For example, 8MB part size can allow  writing a 78GB single file.</description>
    </property>
      
    <property>
    	<name>fs.cosn.maxRetries</name>
      <value>3</value>
      <description>
        The maximum number of retries for reading or writing files to
        COS, before we signal failure to the application.
      </description>
    </property>
      
    <property>
    	<name>fs.cosn.retry.interval.seconds</name>
      <value>3</value>
      <description>The number of seconds to sleep between each COS retry.</description>
    </property>
      
</configuration>
```

### Sample

Command format: `hadoop fs -ls -R cosn://<BucketName-APPID>/<path>` or `hadoop fs -ls -R /<path>` (The `fs.defaultFS` option needs to be set to `cosn://BucketName-APPID`). In the following example, you can append the specified path to the bucket named examplebucket-1250000000.

```shell
hadoop fs -ls -R cosn://examplebucket-1250000000/
-rw-rw-rw-   1 root root       1087 2018-06-11 07:49 cosn://examplebucket-1250000000/LICENSE
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://examplebucket-1250000000/hdfs
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://examplebucket-1250000000/hdfs/2018
-rw-rw-rw-   1 root root       1087 2018-06-12 03:26 cosn://examplebucket-1250000000/hdfs/2018/LICENSE
-rw-rw-rw-   1 root root       2386 2018-06-12 03:26 cosn://examplebucket-1250000000/hdfs/2018/ReadMe
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://examplebucket-1250000000/hdfs/test
-rw-rw-rw-   1 root root       1087 2018-06-11 07:32 cosn://examplebucket-1250000000/hdfs/test/LICENSE
-rw-rw-rw-   1 root root       2386 2018-06-11 07:29 cosn://examplebucket-1250000000/hdfs/test/ReadMe
```

Run the wordcount supplied with MapReduce, and execute the following command.

> hadoop-mapreduce-examples-2.7.2 in the following command is only applicable to Version 2.7.2. For other versions, change it to the actual version number.

```shell
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount cosn://example/mr/input cosn://example/mr/output3
```

If it is successful, the statistics is returned as shown below:

```shell
File System Counters
COSN: Number of bytes read=72
COSN: Number of bytes written=40
COSN: Number of read operations=0
COSN: Number of large read operations=0
COSN: Number of write operations=0
FILE: Number of bytes read=547350
FILE: Number of bytes written=1155616
FILE: Number of read operations=0
FILE: Number of large read operations=0
FILE: Number of write operations=0
HDFS: Number of bytes read=0
HDFS: Number of bytes written=0
HDFS: Number of read operations=0
HDFS: Number of large read operations=0
HDFS: Number of write operations=0
Map-Reduce Framework
Map input records=5
Map output records=7
Map output bytes=59
Map output materialized bytes=70
Input split bytes=99
Combine input records=7
Combine output records=6
Reduce input groups=6
Reduce shuffle bytes=70
Reduce input records=6
Reduce output records=6
Spilled Records=12
Shuffled Maps =1
Failed Shuffles=0
Merged Map outputs=1
GC time elapsed (ms)=0
Total committed heap usage (bytes)=653262848
Shuffle Errors
BAD_ID=0
CONNECTION=0
IO_ERROR=0
WRONG_LENGTH=0
WRONG_MAP=0
WRONG_REDUCE=0
File Input Format Counters
Bytes Read=36
File Output Format Counters
Bytes Written=40
```
