## Feature Description
The HADOOP cosn plugin is used to execute computing tasks using Tencent Cloud COS as the underlying file storage system. You can use Hadoop engines for big data processing, such as MapReduce, Hive, Spark, and Tez, to process data stored on Tencent Cloud COS.

## Operating Environment
### System environment
Linux or Windows.

### Software requirements
Hadoop-2.6.0 or later versions.

## Download and Installation

### Obtain hadoop-cos plugin
Download link: [hadoop-cos plugin](https://github.com/tencentyun/hadoop-cos).


### Install hadoop-cos plugin

1. Copy cos_hadoop_api-5.2.6.jar and hadoop-cos-2.X.X.jar in the dep directory to `$HADOOP_HOME/share/hadoop/tools/lib`.
>Select a jar package based on the version of hadoop. If no matching variation of jar package is found in the dep directory, you can modify the hadoop's version number in the pom file to recompile and generate a jar package. 

2. Modify hadoop_env.sh
Enter hadoop_env.sh under the `$HADOOP_HOME/etc/hadoop` directory. Add the following content and add the cosn-related jar packages to the Hadoop environment variable:
```shell
for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
  if [ "$HADOOP_CLASSPATH" ]; then
    export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
  else
    export HADOOP_CLASSPATH=$f
  fi
done
```

## Directions

### Configure HADOOP

Modify $HADOOP_HOME/etc/hadoop/core-site.xml, and add COS-related users and implementation class information. For example:

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>cosn://<bucket-appid></value>
    </property>
      
    <property>
        <name>hadoop.tmp.dir</name>
        <value>${HADOOP_PATH}/tmp</value>
    </property>
      
    <property>
        <name>dfs.name.dir</name>
        <value>${HADOOP_PATH}/name</value>
    </property>
  
    <property>
        <name>fs.cosn.credentials.provider</name>
        <value>org.apache.hadoop.fs.auth.SimpleCredentialProvider</value>
        <description>

            This option allows the user to specify how to get the credentials.
            Comma-separated class names of credential provider classes which implement
            com.qcloud.cos.auth.COSCredentialsProvider:

            1.org.apache.hadoop.fs.auth.SimpleCredentialProvider: Obtain the secret id and secret key
            from fs.cosn.userinfo.secretId and fs.cosn.userinfo.secretKey in core-site.xml
            2.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: Obtain the secret id and secret key
            from system environment variables named COS_SECRET_ID and COS_SECRET_KEY

            If unspecified, the default order of credential providers is:
            1. org.apache.hadoop.fs.auth.SimpleCredentialProvider
            2. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider

        </description>
    </property>
  
    <property>
        <name>fs.cosn.userinfo.secretId</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxxxx</value>
        <description>Tencent Cloud Secret Id </description>
    </property>
      
    <property>
        <name>fs.cosn.userinfo.secretKey</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxxx</value>
        <description>Tencent Cloud Secret Key</description>
    </property>
      
    <property>
        <name>fs.cosn.userinfo.region</name>
        <value>ap-xxx</value>
        <description>The region where the bucket is located</description>
    </property>
      
    <property>
        <name>fs.cosn.userinfo.endpoint_suffix</name>
        <value>cos.ap-xxx.myqcloud.com</value>
        <description>
          COS endpoint to connect to. 
          For public cloud users, it is recommended not to set this option, and only the correct area field is required.
        </description>
    </property>
      
    <property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosFileSystem</value>
        <description>The implementation class of the CosN Filesystem</description>
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
    	<name>fs.cosn.buffer.size</name>
        <value>33554432</value>
        <description>The total size of the buffer pool</description>
    </property>
      
    <property>
    	<name>fs.cosn.block.size</name>
        <value>8388608</value>
        <description>Block size to use cosn filesysten, which is the part size for MultipartUpload.
        Considering the COS supports up to 10000 blocks, user should estimate the maximum size of a single file.
        for example, 8MB part size can allow  writing a 78GB single file.</description>
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

### Configuration items


| Attribute Key | Description | Default Value | Required |
|:-----------------------------------:|:----------------------|:-----:|:-----:|
| fs.cosn.userinfo.secretId/secretKey | Enter the API key information of your account, which can be seen by logging in to the [console](https://intl.cloud.tencent.com/login). | None | Yes |
| fs.cosn.credentials.provider | Configures the methods on how to get secret id and secret key. There are two methods: 1. org.apache.hadoop.fs.auth.SimpleCredentialProvider: read fs.cosn.userinfo.secretId and fs.cosn.userinfo.secretKey from the configuration file core-site.xml to get secret id and secret key; 2. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: get them from the environment variables COS_SECRET_ID and COS_SECRET_KEY. | If this is not specified, read the following files in numerical order: 1. org.apache.hadoop.fs.auth.SimpleCredentialProvider; 2. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider. | No |
| fs.cosn.impl | The implementation class of cosn in FileSystem, which is always org.apache.hadoop.fs.CosFileSystem. | None | Yes |
| fs.AbstractFileSystem.cosn.impl | The implementation class of cosn in AbstractFileSystem, which is always org.apache.hadoop.fs.CosN. | None | Yes |
| fs.cosn.userinfo.region | Enter your region. Enumerated values are region abbreviations in the [Available Regions](https://intl.cloud.tencent.com/document/product/436/6224), such as ap-beijing and ap-guangzhou. | None | Yes |
| fs.cosn.userinfo.endpoint_suffix | Specifies the COS endpoint to be connected. This is optional. Public cloud COS users can just enter the above region correctly. | None | No |
| fs.cosn.buffer.dir | Sets a directory that actually exists. Temporary files generated in the running process will be stored here. | /tmp/hadoop_cos | No |
| fs.cosn.buffer.size | The size of the memory buffer used in a local server when files are uploaded to COS via stream. It shall be equal to or larger than the size of a block. | 33554432 (32 MB) | No |
| fs.cosn.block.size | The size of each block in the CosN file system, i.e., the part size in multipart upload. Since a maximum of 10,000 parts is supported in multipart upload for COS, you need to estimate the largest size of a single file to be used. For example, if the block size is 8 MB, the largest size of a file that can be uploaded is 78 GB. The maximum block size is 2 GB, so the maximum size of a file that can be uploaded is 19 TB. | 8388608 (8 MB) | No |
| fs.cosn.upload_thread_pool | Number of threads for concurrent upload when files are uploaded to COS via stream. | CPU cores*5 | No |
| fs.cosn.copy_thread_pool | Number of threads for concurrent copy when you copy directories. | CPU cores*3 | No |
| fs.cosn.read.ahead.block.size | Size of a read-ahead block | 524288 (512 KB) | No |
| fs.cosn.read.ahead.queue.size | Length of a read-ahead queue | 10 | No |
| fs.cosn.maxRetries | The maximum of retries when an error occurred while accessing COS | 3 | No |
| fs.cosn.retry.interval.seconds | Retry interval | 3 | No |


### Demo

Command format: `hadoop fs -ls -R cosn://bucket-appid/<path>` or `hadoop fs -ls -R /<path>` (The fs.defaultFS option shall be set as cosn://bucket-appid). In this example, you can append the specified path to the end of the bucket named hdfs-test-1252681929.

```shell
hadoop fs -ls -R cosn://hdfs-test-1252681929/
-rw-rw-rw-   1 root root       1087 2018-06-11 07:49 cosn://hdfs-test-1252681929/LICENSE
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://hdfs-test-1252681929/hdfs
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://hdfs-test-1252681929/hdfs/2018
-rw-rw-rw-   1 root root       1087 2018-06-12 03:26 cosn://hdfs-test-1252681929/hdfs/2018/LICENSE
-rw-rw-rw-   1 root root       2386 2018-06-12 03:26 cosn://hdfs-test-1252681929/hdfs/2018/ReadMe
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://hdfs-test-1252681929/hdfs/test
-rw-rw-rw-   1 root root       1087 2018-06-11 07:32 cosn://hdfs-test-1252681929/hdfs/test/LICENSE
-rw-rw-rw-   1 root root       2386 2018-06-11 07:29 cosn://hdfs-test-1252681929/hdfs/test/ReadMe
```

Run the wordcount provided in MapReduce, and execute the following command.
>!hadoop-mapreduce-examples-2.7.2 in the following command is only applicable to Version 2.7.2. For other versions, change it to the appropriate version number.

```shell
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount cosn://example/mr/input cosn://example/mr/output3
```
It will return the following statistics if it executes successfully:
```
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

