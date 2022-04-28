## Overview

Hadoop-COS implements a standard Hadoop file system on the Tencent Cloud COS platform. It helps integrate COS with big data computing frameworks such as Hadoop, Spark, and Tez, so that they can read and write COS data as they do with HDFS file systems.

Since Hadoop-COS uses COSN (a Tencent Cloud big data tool) as its URI scheme, it can also be referred to as a COSN-based file system.


## Operating Environment

#### Operating system

Windows, Linux, or macOS

#### Software requirements

Hadoop-2.6.0 or later

>?
>1. Hadoop-COS has been integrated in Apache Hadoop-3.3.0. For details, please click [here](https://hadoop.apache.org/docs/r3.3.0/hadoop-cos/cloud-storage/index.html).
>2. If your version is earlier than Apache Hadoop-3.3.0, or the CDH has integrated the Hadoop-COS JAR package, you need to restart NodeManager to load the JAR package.
>3. To build a JAR package of a specified Hadoop version, modify `hadoop.version` in the pom file.



## Download and Installation

#### Obtaining the Hadoop-COS JAR package and dependencies

Download link: [Hadoop-COS release](https://github.com/tencentyun/hadoop-cos/releases)

#### Installing the Hadoop-COS plugin

1. Copy `hadoop-cos-{hadoop.version}-{version}.jar` and `cos_api-bundle-{version}.jar` to `$HADOOP_HOME/share/hadoop/tools/lib`.

> ?Select the JAR package that corresponds to your Hadoop version. If you cannot find the desired JAR package in the release, manually build and generate one by modifying `hadoop.version` in the pom file. 

2. Modify the `hadoop_env.sh` file under the `$HADOOP_HOME/etc/hadoop` directory by adding the COSN JAR package to your Hadoop environment variables as follows:

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

### COSN configuration

| Attribute Key | Description | Default Value | Required |
| :--------------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----: |
| fs.cosn.userinfo.secretId/secretKey | Specifies the API key for your account. Log in to the [CAM console](https://console.cloud.tencent.com/capi) to view the key. | None | Yes |
| fs.cosn.<br>credentials.provider | Specifies how to obtain your SecretId and SecretKey.<br> There are five methods to choose from: <br>1. org.apache.hadoop.fs.auth.SessionCredential<br>Provider: obtains them from the request URI.<br>Format: `cosn://{secretId}:{secretKey}@examplebucket-1250000000/`<br>2. org.apache.hadoop.fs.auth.SimpleCredentialProvider:<br>obtains them by reading `fs.cosn.userinfo.secretId`<br>and `fs.cosn.userinfo.secretKey` from the `core-site.xml` config file.<br>3. org.apache.hadoop.fs.auth.EnvironmentVariableCredential<br>Provider: obtains them from the system environment variables `COS_SECRET_ID` and `COS_SECRET_KEY`.<br>4. org.apache.hadoop.fs.auth.CVMInstanceCredentials<br>Provider: obtains temporary keys for access to<br>COS using a CVM-bound role.<br>5. org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider: obtains temporary keys for access to<br>COS using a CPM-bound role. | If this parameter is not specified, the default order is as follows:<br>1. org.apache.hadoop.fs.auth.<br>SessionCredentialProvider<br>2. org.apache.hadoop.fs.auth.<br>SimpleCredentialProvider <br>3. org.apache.hadoop.fs.auth.<br>EnvironmentVariableCredentialProvider<br>4. org.apache.hadoop.fs.auth.<br>CVMInstanceCredentialsProvider<br>5. org.apache.hadoop.fs.auth.<br>CPMInstanceCredentialsProvider |   No   |
| fs.cosn.useHttps | Indicates whether to use HTTPS as the transfer protocol for the COS server. | false | No |
| fs.cosn.impl | COSN implementation class for FileSystem; fixed as `org.apache.hadoop.fs.CosFileSystem`. | None | Yes |
| fs.AbstractFileSystem.cosn.impl | COSN implementation class for AbstractFileSystem; fixed as `org.apache.hadoop.fs.CosN`. | None | Yes |
| fs.cosn.bucket.region | Specifies the region of the bucket to access. For enumerated values, please see the region abbreviations outlined in [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).<br>Example: ap-beijing and ap-guangzhou. Compatibility is provided for the old parameter `fs.cosn.userinfo.region`. | None |Yes |
| fs.cosn.bucket.<br>endpoint_suffix | Specifies the COS endpoint to connect (optional). Public cloud COS users <br>only need to provide the correct region in the parameter above. Compatibility is provided for the old parameter `fs.cosn.userinfo.endpoint_suffix`. | None | No |
| fs.cosn.tmp.dir | Specifies an existing local directory where temporary files generated at runtime are stored. | /tmp/hadoop_cos | No |
| fs.cosn.upload.<br>part.size | The size of each part for multipart upload using the COSN file system. A COS multipart upload supports a maximum of 10,000 parts to be uploaded for a single object. You need to estimate the desired part size as needed.<br>For example, if the part size is set to `8388608` (8 MB), you can upload an object of up to 78 GB. The size of a part can be up to 2 GB, that is, the size of a single object can be up to 19 TB. | 8388608 (8 MB) | No |
| fs.cosn.<br>upload.buffer | The type of buffer used when uploading files with COSN. Currently, there are three types of buffers: non_direct_memory, <br>direct_memory, and mapped_disk. The non-direct memory buffer uses JVM on-heap memory, the direct_memory buffer uses off-heap memory, and the mapped_disk buffer works based on memory file mapping. | mapped_disk | No|
| fs.cosn.<br>upload.buffer.size | The size of buffer used during the upload with COSN. A value of `-1` means there is no limit. <br>You can specify this value only if you set the buffer type to `mapped_disk`. If you specify a value greater than 0, it cannot be smaller than the block size. Compatibility is provided for the old parameter `fs.cosn.buffer.size`. | -1 | No |
|  fs.cosn.block.size | The size of a block in the COSN file system. | 134217728 (128 MB) | No | 
|    fs.cosn.<br>upload_thread_pool    | Specifies the number of concurrent threads when files are uploaded to COS via streams. | 8 | No |
|         fs.cosn.<br>copy_thread_pool         | Specifies the number of threads used to copy and delete concurrent files during directory replication.            |                   3                       |   No   |
| fs.cosn.<br>read.ahead.block.size | Size of the read-ahead block | 1048576 (1 MB) |No |
| fs.cosn.<br>read.ahead.queue.size | Length of the read-ahead queue | 8 | No |
| fs.cosn.maxRetries | The maximum number of retries if an error occurs when accessing COS | 200 | No |
| fs.cosn.retry.<br>interval.seconds  | Time interval between retries in seconds | 3 | No |
| fs.cosn.<br>server-side-encryption.algorithm | Specifies the COS server-side encryption algorithm. Valid values: `SSE-C` and `SSE-COS`. If this parameter is left empty (default), no encryption algorithm is used. | None | No |
| fs.cosn.<br>server-side-encryption.key | Specifies the required SSE-C key if the SSE-C server encryption algorithm is used.<br>This parameter is a Base64-encoded AES-256 key. If this parameter is left empty (default), no encryption key is used. | None | No |
| fs.cosn.<br>crc64.checksum.enabled | Indicates whether to enable CRC-64 checksum. It is disabled by default, meaning that you can’t run the `hadoop fs -checksum` command to obtain the CRC-64 checksum of a file. | false | No |
|fs.cosn.<br>crc32c.checksum.enabled    | Indicates whether to enable CRC32C checksum. It is disabled by default, meaning that you cannot run the `hadoop fs -checksum` command to obtain the CRC32C checksum of a file. CRC-64 and CRC32C cannot be both enabled. | false | No |
| fs.cosn.traffic.limit | Specifies the limit on the upload bandwidth, in bit/s. Value range: 819200-838860800. Defaults to `-1`, meaning no limit. | None | No | 


### Hadoop configuration

Modify `$HADOOP_HOME/etc/hadoop/core-site.xml` by adding information on COS users and implementation classes, as shown below:

```xml
<configuration>
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
            4. org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider
            5. org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider
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
        <name>fs.cosn.upload.buffer</name>
        <value>mapped_disk</value>
        <description>The type of upload buffer. Available values: non_direct_memory, direct_memory, mapped_disk</description>
    </property>

    <property>
        <name>fs.cosn.upload.buffer.size</name>
        <value>134217728</value>
        <description>The total size of the upload buffer pool. -1 means unlimited.</description>
    </property>
	
    <property>
    	<name>fs.cosn.upload.part.size</name>
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

You are not advised to configure `fs.defaultFS` in the production environment. To use it for certain test cases (for example, hive-testbench), add the following configurations:

```
<property>
          <name>fs.defaultFS</name>
          <value>cosn://examplebucket-1250000000</value>
        <description>
             This option is not advice to config, this only used for some special test cases.
        </description>
</property>
```
  
### Server-side encryption

Hadoop-COS supports server-side encryption using either of the following two methods: COS-managed keys (SSE-COS) and customer-provided keys (SSE-C). You can enable this feature, which is disabled by default, by configuring as shown below:

#### SSE-COS encryption

SSE-COS encryption refers to server-side encryption with COS-managed keys. That is, Tencent Cloud COS manages the master key and its data. When using Hadoop-COS, you can add the following configuration in the `$ HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-COS encryption.

```shell
<property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-COS</value>
        <description>The server side encryption algorithm.</description>
</property>
```

#### SSE-C encryption

SSE-C encryption refers to server-side encryption with customer-provided keys. That is, the encryption key is provided by the user. When you upload an object, COS will use the encryption key that you provide to apply AES-256 encryption to the data. When using Hadoop-COS, you can add the following configuration in the `$ HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-C encryption.

```shell
<property>
        <name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-C</value>
        <description>The server side encryption algorithm.</description>
 </property>		
 <property>
  	<name>fs.cosn.server-side-encryption.key</name>
        <value>MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=</value> #Users need to configure the SSE-C key in the format of a Base64-encoded AES-256 key.
        <description>The SSE-C server side encryption key.</description>
 </property> 
```

> !
>
> - The SSE-C encryption feature of Hadoop-COS relies on the SSE-C server-side encryption of COS, which means Hadoop-COS does not store any customer-provided encryption keys, just like COS. Instead, COS stores HMAC values with random data added to the encryption keys to verify access requests. COS cannot use the HMAC values to derive the value of an encryption key or decrypt object content. Therefore, if you lose your encryption key, you will not be able to access the object again.
> - If you configure an SSE-C server-side encryption algorithm on Hadoop-COS, you must also configure an SSE-C key using the `fs.cosn.server-side-encryption.key` parameter in the format of a Base64-encoded AES-256 key.

### Examples

Run a command in the format: `hadoop fs -ls -R cosn://<BucketName-APPID>/<path>` or `hadoop fs -ls -R /<path>` (you need to set `fs.defaultFS` to `cosn://BucketName-APPID`). The following example uses a bucket named `examplebucket-1250000000`, to which you can append a specific path.

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

> !This example uses `hadoop-mapreduce-examples-2.7.2.jar`. To use a different version of the JAR file, modify the version number.

```shell
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount cosn://example/mr/input cosn://example/mr/output3
```

If the command is successful, the following information will be returned:

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

## FAQ
If you have any questions about Hadoop-COS, please see [Hadoop Tool](https://intl.cloud.tencent.com/document/product/436/35706).
