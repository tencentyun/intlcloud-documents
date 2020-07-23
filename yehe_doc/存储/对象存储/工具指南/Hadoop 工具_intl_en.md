## Feature description

Hadoop-COS implements a standard Hadoop file system on the Tencent Cloud COS platform. It supports the integration of COS with big data computing frameworks such as Hadoop, Spark and Tez, enabling them to read and write data stored on COS when they access the HDFS file system.

Hadoop-COS uses cosn as a URI scheme, so it is also known as a CosN file system.

## Operating Environment

### System environment

Hadoop-COS is supported on the Linux, Windows and macOS operating systems.

### Software requirements

Hadoop-2.6.0 or later.

## Download and installation

### Obtaining the Hadoop-COS plugin

Download the Hadoop-COS Plugin [here](https://github.com/tencentyun/hadoop-cos).

### Installing the Hadoop-COS Plugin

1. Copy `hadoop-cos-X.X.X-shaded.jar *` in the dep directory to `$ HADOOP_HOME/share/hadoop/tools/lib`.

>Select a jar package based on the Hadoop version you have installed. If no matching jar package is found in the dep directory, you can modify the Hadoop version number in the pom file to recompile and generate a jar package. 

2. Modify the `hadoop_env.sh` file.
   Edit the `hadoop_env.sh` file under the `$HADOOP_HOME/etc/hadoop` directory. Add the following content and add the cosn-related jar packages to the Hadoop environment variable:

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

### Configuration Items

| Attribute Key | Description | Default Value | Required |
| :--------------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----: |
| fs.cosn.userinfo.secretId/secretKey | Enter the API key for your account. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) to view your cloud API key | None |Yes|
| fs.cosn.credentials.provider | Configure how to get your secretId and secretKey. There are three methods currently available: 1. org.apache.hadoop.fs.auth.SessionCredentialProvider: get your secretId and secretKey from the request URI in the format: `cosn://{secretId}:{secretKey}@examplebucket-1250000000/`.<br>2. org.apache.hadoop.fs.auth.SimpleCredentialProvider: get your secretId and secretKey by reading fs.cosn.userinfo.secretId and fs.cosn.userinfo.secretKey from the configuration file core-site.xml;<br>3. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: get your secretId and secretKey from the environment variables COS_SECRET_ID and COS_SECRET_KEY. | If the configuration items are not specified, they are read in the following order by default:<br>1.org.apache.hadoop.fs.auth.SessionCredentialProvider<br>2.org.apache.hadoop.fs.auth.SimpleCredentialProvider <br>3.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider | No |
| fs.cosn.impl | The cosn implementation class for FileSystem is fixed as org.apache.hadoop.fs.CosFileSystem. | None | Yes |
| fs.AbstractFileSystem.cosn.impl | The cosn implementation class for AbstractFileSystem is fixed as org.apache.hadoop.fs.CosN. | None | Yes |
| fs.cosn.bucket.region | Enter the region of the bucket to be accessed. For enumerated values, see the region abbreviations outlined in [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224), such as ap-beijing and ap-guangzhou. Compatible with the original configuration: fs.cosn.userinfo.region. | None |Yes |
| fs.cosn.bucket.endpoint_suffix | Specify the COS endpoint to be connected (optional). Public cloud COS users only need to enter the proper region configuration. Compatible with the original configuration: fs.cosn.userinfo.endpoint_suffix | None | No |
| fs.cosn.tmp.dir | For this item, you need to set an actual existing local directory, as temporary files generated when running will be briefly stored in this directory. | /tmp/hadoop_cos | No |
| fs.cosn.block.size | The size of each block in the CosN file system (this value is also the size of each part in a multipart upload). Since a maximum of 10,000 parts are allowed for a multipart upload in COS, you need to estimate the largest possible single file size that you may need to use. For example, if the block size is 8 MB, the largest file that can be uploaded is 78 GB. The maximum allowed block size is 2 GB, so the maximum single file size allowed for upload is 19TB | 8388608 (8 MB) | No |
| fs.cosn.upload_thread_pool | Number of concurrent upload threads when files are uploaded to COS via streams. | CPU cores*5 | No |
| fs.cosn.copy_thread_pool | Number of threads that can be used to copy files concurrently when directories are copied. | CPU cores*3 | No |
| fs.cosn.read.ahead.block.size | Read ahead block size | 1048576 (1 MB) |No |
| fs.cosn.read.ahead.queue.size | Length of the read ahead queue | 8 | No |
| fs.cosn.maxRetries | The maximum number of retries if an error occurs when accessing COS | 3 | No |
| fs.cosn.retry.interval.seconds | Time interval between retries | 3 | No |
| fs.cosn.server-side-encryption.algorithm | This item is used to configure the COS server-side encryption algorithm. Currently two types of encryption are supported SSE-C and SSE-COS, and the default configuration is empty, meaning not encrypted. | None | No |
| fs.cosn.server-side-encryption.key | When SSE-C server-side encryption is enabled, an SSE-C key must be configured. The key is in the format of a base64-encoded AES-256 key; this item’s default configuration is empty, meaning not encrypted. | None | No |

### Configuring Hadoop

Modify `$HADOOP_HOME/etc/hadoop/core-site.xml` and add information on the relevant COS users and implementation classes, as shown below:

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

            This option allows users to specify how to get the credentials.
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
          COS endpoint to which to connect. 
          For public cloud users, we do not recommend setting this option; you only need to enter the proper region information.
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
    	<name>fs.cosn.block.size</name>
        <value>8388608</value>
        <description>Block size to use in the cosn filesysten; this value is also the part size for multipart uploads.
        Considering that COS supports up to 10000 blocks, users should estimate the maximum size of a single file to help decide on the configuration for block size.
        For example, 8MB part size will allow writing a single file of up to 78GB in size.</description>
    </property>
      
    <property>
    	<name>fs.cosn.maxRetries</name>
      <value>3</value>
      <description>
        The maximum number of retries upon failure to access
        COS before we signal failure to the application.
      </description>
    </property>
      
    <property>
    	<name>fs.cosn.retry.interval.seconds</name>
      <value>3</value>
      <description>The time interval between each retry.</description>
    </property>
   
    <property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value></value>
        <description>The server side encryption algorithm.</description>
    </property>	
	
     <property>
    	<name>fs.cosn.server-side-encryption.key</name>
        <value></value>
        <description>The SSE-C server side encryption key.</description>
    </property> 
      
</configuration>
```

### Server Encryption

Hadoop-COS supports server-side encryption, and there are two encryption methods currently available: the COS-managed key method (SSE-COS) and the user-defined key method (SSE-C). The Hadoop-COS encryption function is disabled by default. Please see below for information on how to enable and configure encryption for Hadoop-COS. 

### SSE-COS Encryption

SSE-COS encryption refers to server-side encryption with COS-managed keys. That is, Tencent Cloud COS manages the master key and its data. When using Hadoop-COS, you can add the following configuration in the `$ HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-COS encryption.

```shell
<property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-COS</value>
        <description>The server side encryption algorithm.</description>
</property>
```

### SSE-C Encryption

SSE-C encryption refers to server-side encryption with user-defined keys. That is, the encryption key is provided by the user. When you upload an object, COS will use the encryption key that you provide to apply AES-256 encryption to the data. When using Hadoop-COS, you can add the following configuration in the `$ HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-C encryption.

```shell
<property>
        <name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-C</value>
        <description>The server side encryption algorithm.</description>
 </property>		
 <property>
  	<name>fs.cosn.server-side-encryption.key</name>
        <value>MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=</value> #Users need to configure the SSE-C key in the format of a base-64 encoded AES-256 key.
        <description>The SSE-C server side encryption key.</description>
 </property> 
```

>
>
>- SSE-C server-side encryption of Hadoop-COS relies on the SSE-C server-side encryption of COS. Thus, Hadoop-COS does not store the encryption key provided by the user. In addition, the SSE-C server-side encryption method for COS does not store the encryption key provided by the user. Instead, it stores the HMAC value with random data added, which is then used to verify the user's request to access the object. COS cannot use the HMAC value to derive the value of the encryption key or decrypt the object content. Hence, if the user loses the encryption key, the object cannot be obtained again.
>- When Hadoop-COS is configured with the SSE-C server-side encryption algorithm, the SSE-C key must be configured in the `fs.cosn.server-side-encryption.key` configuration item in the format of a base64-encoded AES-256 key.

### Use case

Command format: `hadoop fs -ls -R cosn://<BucketName-APPID>/<path>` or `hadoop fs -ls -R /<path>` (The `fs.defaultFS` option needs to be configured to `cosn://BucketName-APPID`). As in the following example using examplebucket-1250000000, you can append specific path information to the end of the bucket.

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

Run the wordcount provided in MapReduce and execute the following command.

> !hadoop-mapreduce-examples-2.7.2 in the following command is only applicable to version 2.7.2. For other versions, use the corresponding version number.

```shell
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount cosn://example/mr/input cosn://example/mr/output3
```

The following statistics will be returned if the execution is successful:

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


## FAQs
If you have any question about Hadoop-COS, see the [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/35706) FAQs.
