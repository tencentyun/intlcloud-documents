#### Feature

Hadoop-COS implements a standard Hadoop file system based on Tencent Cloud COS. It supports the integration of COS with big data computing frameworks such as Hadoop, Spark and Tez, enabling them to read and write data stored on COS the way when they access the HDFS file system.

Hadoop-COS uses cosn as a URI scheme, so it is also called CosN file system.

## Operating Environment

### System Environment

Hadoop-COS is supported on Linux, Windows and macOS operating systems.

### Software Requirements

Hadoop-2.6.0 or later.

## Download and Installation

### Obtaining the Hadoop-COS plugin

Download the [Hadoop-COS Plugin](https://github.com/tencentyun/hadoop-cos).

### Installing the Hadoop-COS Plugin

1. Copy `hadoop-cos-X.X.X-shaded.jar *` in the dep directory to `$ HADOOP_HOME/share/hadoop/tools/lib`.

>Select a jar package based on the Hadoop version. If no matching version of jar package is found in the dep directory, modify Hadoop's version number in pom file to recompile and generate a jar package. 

2. Modify the hadoop_env.sh File.
   Edit hadoop_env.sh file under the `$HADOOP_HOME/etc/hadoop` directory. Add the following content and add cosn-related jar packages to the Hadoop environment variable:

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

| Attribute Key | Description | Default Value | Required |
| :--------------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----: |
| fs.cosn.userinfo.secretId/secretKey | Enter the API key for your account. Log into the [CAM Console](https://console.cloud.tencent.com/capi) to view the cloud API key | None |Yes|
| fs.cosn.credentials.provider | Configure how to get secretId and secretKey. Three methods are currently available: 1. org.apache.hadoop.fs.auth.SessionCredentialProvider: get secret id and secret key from the request URI, with a format of cosn://{secretId}:{secretKey}@examplebucket-1250000000;/<br>2. org.apache.hadoop.fs.auth.SimpleCredentialProvider: Get secret id and secret key by reading fs.cosn.userinfo.secretId and fs.cosn.userinfo.secretKey from the configuration file core-site.xml;<br>3. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: Get them from environment variables COS_SECRET_ID and COS_SECRET_KEY. | If configuration items are not specified, they are read in the following order:<br>1.org.apache.hadoop.fs.auth.SessionCredentialProvider<br>2.org.apache.hadoop.fs.auth.SimpleCredentialProvider <br>3.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider | No |
| fs.cosn.impl | The implementation class of cosn in FileSystem, which is always org.apache.hadoop.fs.CosFileSystem. | None | Yes |
| fs.AbstractFileSystem.cosn.impl | The implementation class of cosn in AbstractFileSystem, which is always org.apache.hadoop.fs.CosN. | None | Yes |
| fs.cosn.bucket.region | Enter the region of the bucket to be accessed. For enumerated values, see region abbreviations in [Regions and Access Domain Names](https://cloud.tencent.com/document/product/436/6224), such as ap-beijing and ap-guangzhou. Compatible with the original configuration: fs.cosn.userinfo.region. | None |Yes |
| fs.cosn.bucket.endpoint_suffix | Specify the COS endpoint to be connected (optional). Public cloud COS users only need to enter the correct region configuration. Compatible with the original configuration: fs.cosn.userinfo.endpoint_suffix | None | No |
| fs.cosn.tmp.dir | Configure a directory that actually exists. Temporary files generated when running are stored in the directory. | /tmp/hadoop_cos | No |
| fs.cosn.block.size | The size of each block in the CosN file system (size of each part in multipart upload). Since a maximum of 10,000 parts are allowed for a multipart upload in COS, you need to estimate the largest possible size of a single file to be used. For example, if the block size is 8 MB, the largest file that can be uploaded is 78 GB. The maximum block size is 2 GB, so the maximum single file size allowed for upload is 19TB | 8388608 (8 MB) | No |
| fs.cosn.upload_thread_pool | Number of threads uploading concurrently when files are uploaded to COS via streams. | CPU cores*5 | No |
| fs.cosn.copy_thread_pool | Number of threads can be used to copy files concurrently when directories are copied. | CPU cores*3 | No |
| fs.cosn.read.ahead.block.size | Pre-read block size | 1048576 (1 MB) |No |
| fs.cosn.read.ahead.queue.size | Length of pre-read queue | 8 | No |
| fs.cosn.maxRetries | The maximum number of retries if an error occurs when accessing COS | 3 | No |
| fs.cosn.retry.interval.seconds | Time interval between retries | 3 | No |
| fs.cosn.server-side-encryption.algorithm | Configure COS server-side encryption algorithm, support SSE-C and SSE-COS, default is empty, meaning not encrypted. | None | No |
| fs.cosn.server-side-encryption.key | When SSE-C server-side encryption algorithm of COS is enabled, SSE-C key must be configured. The format is AES-256 key encoded in base64, default is empty, meaning not encrypted. | None | No |

### Configuring Hadoop

Modify `$HADOOP_HOME/etc/hadoop/core-site.xml`, and add information on COS users and implementation classes, as shown below:

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

Hadoop-COS supports server-side encryption, and two encryption methods are currently available: COS-managed key method (SSE-COS) and user-defined key method (SSE-C). The encryption function of Hadoop-COS is disabled by default. Users can enable and configure it in the following ways.

### SSE-COS Encryption

SSE-COS encryption is server-side encryption with COS-managed keys. Tencent Cloud COS manages the master key and its data. When using Hadoop-COS, users can add the following configuration in `$ HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-COS encryption.

```shell
<property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-COS</value>
        <description>The server side encryption algorithm.</description>
</property>
```

### SSE-C Encryption

SSE-C encryption is server-side encryption with user-defined keys. The encryption key is provided by the user. When the user uploads the object, COS will use the encryption key provided by the user to apply AES-256 encryption to the data. When using Hadoop-COS, users can add the following configuration in `$ HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-C encryption.

```shell
<property>
        <name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-C</value>
        <description>The server side encryption algorithm.</description>
 </property>		
 <property>
  	<name>fs.cosn.server-side-encryption.key</name>
        <value>MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=</value> #User needs to configure the SSE-C key in the format of base64-encoded AES-256 key.
        <description>The SSE-C server side encryption key.</description>
 </property> 
```

>
>
>- SSE-C server-side encryption of Hadoop-COS relies on the SSE-C server-side encryption of COS. Thus, Hadoop-COS does not store the encryption key provided by the user. Additionally, SSE-C server-side encryption method of COS does not store the encryption key provided by the user. Instead, it stores the HMAC value with random data added, which is used to verify the user's request to access the object. COS cannot use the HMAC value to derive the value of the encryption key or decrypt the object content. Hence, if the user loses the encryption key, the object cannot be obtained again.
>- When Hadoop-COS is configured with SSE-C server-side encryption algorithm, SSE-C key must be configured in the fs.cosn.server-side-encryption.key configuration item, and the key format is a base64-encoded AES-256 key .

### Sample

Command format: `hadoop fs -ls -R cosn://<BucketName-APPID>/<path>` or `hadoop fs -ls -R /<path>` (The `fs.defaultFS` option needs to be configured to `cosn://BucketName-APPID`). In the following example, you can append the specified path to the bucket named examplebucket-1250000000.

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

Run the wordcount provided in MapReduce, and execute the following command.

>hadoop-mapreduce-examples-2.7.2 in the following command is only applicable to version 2.7.2. For other versions, use the corresponding version number.

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
