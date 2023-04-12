## Feature Overview

Hadoop-COS implements a standard Hadoop file system on the Tencent Cloud COS platform. It helps integrate COS with big data computing frameworks such as Hadoop, Spark, and Tez, so that they can read and write COS data as they do with HDFS file systems.

Since Hadoop-COS uses COSN (a Tencent Cloud big data tool) as its URI scheme, it can also be referred to as a COSN-based file system.


## Operating Environments

#### Operating system

Windows, Linux, or macOS

#### Software dependency

Hadoop-2.6.0 or later

>?
- Hadoop-COS has been integrated in Apache Hadoop-3.3.0. For details, click [here](https://hadoop.apache.org/docs/r3.3.0/hadoop-cos/cloud-storage/index.html).
- If your version is earlier than Apache Hadoop-3.3.0, or the CDH has integrated the Hadoop-COS JAR package, you need to restart NodeManager to load the JAR package.
-  To build a JAR package of a specified Hadoop version, modify `hadoop.version` in the pom file.



## Download and Installation

#### Obtaining the Hadoop-COS JAR package and dependencies

Download link: [Hadoop-COS release](https://github.com/tencentyun/hadoop-cos/releases)

### Installing the Hadoop-COS plugin

1. Copy `hadoop-cos-{hadoop.version}-{version}.jar` and `cos_api-bundle-{version}.jar` to `$HADOOP_HOME/share/hadoop/tools/lib`.
>? Select the JAR package that corresponds to your Hadoop version. If you cannot find the desired JAR package in the release, manually build and generate one by modifying `hadoop.version` in the pom file.
>
2. Modify the `hadoop-env.sh` file under the `$HADOOP_HOME/etc/hadoop` directory by adding the COSN JAR package to your Hadoop environment variables as follows:
```shell
for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
  if [ "$HADOOP_CLASSPATH" ]; then
    export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
  else
    export HADOOP_CLASSPATH=$f
  fi
done
```

## Configuration Method

### COSN configuration

| Attribute Key | Description | Default Value | Required |
| :---------------------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----: |
|   fs.cosn.userinfo.<br>secretId/secretKey    | The API key for your account. Log in to the [CAM console](https://console.cloud.tencent.com/capi) to view the key. | None | Yes |
|       fs.cosn.<br>credentials.provider       | The way to get `SecretId` and `SecretKey`. Currently, the following ways are supported: <ol  style="margin: 0;"><li>org.apache.hadoop.fs.auth.SessionCredentialProvider: Gets them from the request URI in the format of `cosn://{secretId}:{secretKey}@examplebucket-1250000000/`. </li><li>org.apache.hadoop.fs.auth.SimpleCredentialProvider: Gets them by reading `fs.cosn.userinfo.secretId` and `fs.cosn.userinfo.secretKey` in the `core-site.xml` configuration file. </li><li>org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: Gets them from system variables `COS_SECRET_ID` and `COS_SECRET_KEY`. </li><li>org.apache.hadoop.fs.auth.SessionTokenCredentialProvider: Accesses by using a temporary key as described in [Generating and Using Temporary Keys](https://www.tencentcloud.com/document/product/436/14048). </li><li>org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider: Gets a temporary key to access COS by using the role bound to CVM. </li><li>org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider: Gets a temporary key to access COS by using the role bound to CPM. </li><li>org.apache.hadoop.fs.auth.EMRInstanceCredentialsProvider: Gets a temporary key to access COS by using the role bound to EMR. </li><li>org.apache.hadoop.fs.auth.RangerCredentialsProvider: Gets a key by using Ranger. </li></ol>| If this parameter is not specified, the default order will be as follows: <ol  style="margin: 0;"><li>org.apache.hadoop.fs.auth.SessionCredentialProvider</li><li>org.apache.hadoop.fs.auth.SimpleCredentialProvider</li><li>org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider</li><li>org.apache.hadoop.fs.auth.SessionTokenCredentialProvider</li><li>org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider</li><li>org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider</li><li>org.apache.hadoop.fs.auth.EMRInstanceCredentialsProvider</li></ol> |   No   |
| fs.cosn.useHttps | Whether to use HTTPS as the transfer protocol for the COS backend. | true | No |
|               fs.cosn.impl               | The COSN implementation class for `FileSystem`, which is fixed at `org.apache.hadoop.fs.CosFileSystem`. |                              None                              |   Yes   |
|     fs.AbstractFileSystem.<br>cosn.impl      | The COSN implementation class for `AbstractFileSystem`, which is fixed at `org.apache.hadoop.fs.CosN`. |                              None                              |   Yes   |
|          fs.cosn.bucket.region           | The region of the bucket to access. For enumerated values, see the region abbreviations in [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224), such as `ap-beijing` and `ap-guangzhou`. <br>This parameter is compatible with the old parameter `fs.cosn.userinfo.region`.  |                              None                              |   Yes   |
|      fs.cosn.bucket.<br>endpoint_suffix      | The COS endpoint to connect (optional). Public cloud COS users only need to provide the correct `region` in the parameter above. This parameter is compatible with the old parameter `fs.cosn.userinfo.endpoint_suffix`. To make `endpoint` take effect, you should delete the `fs.cosn.bucket.region` parameter first. | None | No |
|             fs.cosn.tmp.dir              | An existing local directory where temporary files generated at runtime are stored. | /tmp/hadoop_cos | No |
|          fs.cosn.upload.<br>part.size           | The size of each part for multipart upload through the COSN file system. A COS multipart upload supports a maximum of 10,000 parts to be uploaded for a single object. You need to estimate the desired part size as needed. <br>For example, if the part size is set to `8388608` (8 MB), you can upload an object of up to 78 GB in size. The size of a part can be up to 2 GB, that is, the size of a single object can be up to 19 TB. | 8388608 (8 MB) |   No   |
| fs.cosn.<br>upload.buffer | The type of buffer used when files are uploaded through COSN. Currently, there are three types of buffers: non_direct_memory, direct_memory, and mapped_disk. <br>The non-direct memory buffer uses JVM on-heap memory, the direct_memory buffer uses off-heap memory, and the mapped_disk buffer works based on memory file mapping. | mapped_disk | No |
| fs.cosn.<br>upload.buffer.size | The size of buffer used during upload through COSN. A value of `-1` means unlimited. <br>You can specify this value only if you set the buffer type to `mapped_disk`. If you specify a value greater than 0, it cannot be smaller than the block size. This parameter is compatible with the old parameter `fs.cosn.buffer.size`. | -1 | No |
|  fs.cosn.block.size | The size of a block in the COSN file system.                             |                      134217728 (128 MB)                      |   No   |
|        fs.cosn.<br>upload_thread_pool        | The number of concurrent threads when files are uploaded to COS through streams.                  |                        10                        |   No   |
|         fs.cosn.<br>copy_thread_pool         | The number of threads used to copy and delete concurrent files during directory replication.               |                   3                       |   No   |
|      fs.cosn.<br>read.ahead.block.size       | The size of a read-ahead block.                                               |                        1048576 (1 MB)                        |   No   |
|      fs.cosn.<br>read.ahead.queue.size       | The length of the read-ahead queue.                                             |                              8                               |   No   |
|            fs.cosn.maxRetries            | The maximum number of retries if an error occurs when accessing COS.                        |                             200                              |   No   |
|      fs.cosn.retry.<br>interval.seconds      | The time interval between retries in seconds.                                         |                              3                               |   No   |
| fs.cosn.<br>server-side-encryption.algorithm | The COS server-side encryption algorithm. Valid values: `SSE-C`, `SSE-COS`. If this parameter is left empty (default value), no encryption algorithm will be used. |                              None                              |   No   |
|    fs.cosn.<br>server-side-encryption.key    | The required SSE-C key if the SSE-C server encryption algorithm is used. <br>This parameter is a Base64-encoded AES-256 key. If this parameter is left empty (default value), no encryption key will be used.  |                              None                              |   No   |
|     fs.cosn.client-side-encryption.enabled      | Whether to enable client-side encryption, which is not enabled by default. After enabling it, you must configure the public key and private key for it, and you cannot use the APPEND and TRUNCATE APIs. | false | No |
| fs.cosn.client-side-encryption.public.key.path  | The absolute path of the public key file for client-side encryption. | None | No |
| fs.cosn.client-side-encryption.private.key.path | The absolute path of the private key file for client-side encryption. | None | No |
| fs.cosn.<br>crc64.checksum.enabled | Whether to enable CRC-64 checksum. It is disabled by default, meaning that you can't run the `hadoop fs -checksum` command to obtain the CRC-64 checksum of a file. | false | No |
|       fs.cosn.<br>crc32c.checksum.enabled       | Whether to enable CRC32C checksum. It is disabled by default, meaning that you cannot run the `hadoop fs -checksum` command to obtain the CRC32C checksum of a file. CRC-64 and CRC32C cannot be both enabled. | false | No |
| fs.cosn.traffic.limit | The limit on the upload bandwidth in bits/s. Value range: 819200–838860800. Default value: `-1` (unlimited). | None | No |


### Hadoop configuration

Modify `$HADOOP_HOME/etc/hadoop/core-site.xml` by adding the information of COS users and implementation classes as shown below:

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
            4. org.apache.hadoop.fs.auth.SessionTokenCredentialProvider
            5. org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider
            6. org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider
            7. org.apache.hadoop.fs.auth.EMRInstanceCredentialsProvider
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
      <description>The number of seconds to sleep between each COS retry.</description>
    </property>
   
    <property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value></value>
        <description>The server-side encryption algorithm.</description>
    </property>	
	
     <property>
    	<name>fs.cosn.server-side-encryption.key</name>
        <value></value>
        <description>The SSE-C server-side encryption key.</description>
    </property> 
  
    <property>
        <name>fs.cosn.client-side-encryption.enabled</name>
        <value></value>
        <description>Enable or disable the client encryption function</description>
    </property>
  
    <property>
        <name>fs.cosn.client-side-encryption.public.key.path</name>
        <value>/xxx/xxx.key</value>
        <description>The direct path to the public key</description>
    </property>
  
     <property>
        <name>fs.cosn.client-side-encryption.private.key.path</name>
        <value>/xxx/xxx.key</value>
        <description>The direct path to the private key</description>
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

SSE-COS encryption refers to server-side encryption with a COS-managed key. In this mode, COS manages the master key and its data. When using Hadoop-COS, you can add the following configuration in the `$HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-COS encryption.

```shell
<property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-COS</value>
        <description>The server-side encryption algorithm.</description>
</property>
```

#### SSE-C encryption

SSE-C encryption refers to server-side encryption with customer-provided keys. That is, the encryption key is provided by the user. When you upload an object, COS will use the encryption key that you provide to apply AES-256 encryption to the data. When using Hadoop-COS, you can add the following configuration in the `$ HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-C encryption.

```shell
<property>
        <name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-C</value>
        <description>The server-side encryption algorithm.</description>
 </property>		
 <property>
  	<name>fs.cosn.server-side-encryption.key</name>
        <value>MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=</value> #Users need to configure the SSE-C key in the format of a Base64-encoded AES-256 key.
        <description>The SSE-C server-side encryption key.</description>
 </property> 
```

>!
>- The SSE-C encryption feature of Hadoop-COS relies on the SSE-C server-side encryption of COS. This means Hadoop-COS does not store any user-defined encryption keys just like COS. Instead, COS stores HMAC values with random data added to the encryption keys to authenticate access requests. COS cannot use the HMAC values to derive the value of an encryption key or decrypt the content of an object. Therefore, if you lose your encryption key, you will not be able to access the object again.
>- If you configure an SSE-C server-side encryption algorithm in Hadoop-COS, you must also configure an SSE-C key by using the `fs.cosn.server-side-encryption.key` parameter in the format of a Base64-encoded AES-256 key.
>

### Client-side encryption

COSN client-side encryption adopts the RSA encryption method. The key is divided into public key and private key. The former is used for file encryption, and the latter is used for file decryption. When a file is uploaded, COSN will generate a random key and use it to encrypt the file symmetrically. The public key encrypts this key and saves the encrypted information in the file's metadata. When the file is downloaded, COSN will use the private key to obtain the encrypted random key from the file's metadata for decryption and then use the decrypted random key to decrypt the file. The public and private keys only participate in the local calculation in the client but are not transferred on the network or stored on the server, ensuring the data security of the master key.

- When using client-side encryption, you should ensure the integrity and accuracy of the master key. When copying or migrating encrypted data, you should ensure the integrity and accuracy of the cryptographic metadata. If any encrypted data cannot be decoded due to cryptographic metadata loss/corruption caused by your incorrect use or loss of the master key, you shall bear all losses and consequences arising from it.
- After client-side encryption is enabled, APPEND and TRUNCATE APIs are no longer supported.
- If you run the `hadoop fs -cp` command on an encrypted file in a client with the client-side encryption feature disabled, the encrypted information will be lost.
- After client-side encryption is enabled, CRC file verification and async multipart upload are disabled by default.

When using Hadoop-COS, you can add the following configuration in the `$HADOOP_HOME/etc/hadoop/core-site.xml` file to implement SSE-COS encryption.

```shell
 <property>
        <name>fs.cosn.client-side-encryption.enabled</name>
        <value>true</value>
        <description>Enable or disable the client encryption function</description>
    </property>
  
    <property>
        <name>fs.cosn.client-side-encryption.public.key.path</name>
        <value>/xxx/xxx.key</value>
        <description>The direct path to the public key</description>
    </property>
  
     <property>
        <name>fs.cosn.client-side-encryption.private.key.path</name>
        <value>/xxx/xxx.key</value>
        <description>The direct path to the private key</description>
    </property>
```

You can generate the key with the following code:

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.security.KeyPair;
import java.security.KeyPairGenerator;
import java.security.NoSuchAlgorithmException;
import java.security.PrivateKey;
import java.security.PublicKey;
import java.security.SecureRandom;
import java.security.spec.PKCS8EncodedKeySpec;
import java.security.spec.X509EncodedKeySpec;

// Use asymmetric key RSA encryption for randomly generated symmetric keys
public class BuildKey {
    private static final SecureRandom srand = new SecureRandom();
    private static void buildAndSaveAsymKeyPair(String pubKeyPath, String priKeyPath) throws IOException, NoSuchAlgorithmException {
        KeyPairGenerator keyGenerator = KeyPairGenerator.getInstance("RSA");
        keyGenerator.initialize(1024, srand);
        KeyPair keyPair = keyGenerator.generateKeyPair();
        PrivateKey privateKey = keyPair.getPrivate();
        PublicKey publicKey = keyPair.getPublic();

        X509EncodedKeySpec x509EncodedKeySpec = new X509EncodedKeySpec(publicKey.getEncoded());
        FileOutputStream fos = new FileOutputStream(pubKeyPath);
        fos.write(x509EncodedKeySpec.getEncoded());
        fos.close();

        PKCS8EncodedKeySpec pkcs8EncodedKeySpec = new PKCS8EncodedKeySpec(privateKey.getEncoded());
        fos = new FileOutputStream(priKeyPath);
        fos.write(pkcs8EncodedKeySpec.getEncoded());
        fos.close();
    }


    public static void main(String[] args) throws Exception {

        String pubKeyPath = "pub.key";
        String priKeyPath = "pri.key";
        buildAndSaveAsymKeyPair(pubKeyPath, priKeyPath);
    }
}

```

## How to Use


### Examples

Run a command in the format of `hadoop fs -ls -R cosn://<BucketName-APPID>/<path>` or `hadoop fs -ls -R /<path>` (you need to set `fs.defaultFS` to `cosn://BucketName-APPID`). The following example uses a bucket named `examplebucket-1250000000`, to which you can append a specific path.

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

>! This example uses `hadoop-mapreduce-examples-2.7.2.jar`. To use a different version of the JAR file, modify the version number.
>

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

### Accessing COSN through Java code

```
package com.qcloud.chdfs.demo;

import org.apache.commons.io.IOUtils;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FSDataInputStream;
import org.apache.hadoop.fs.FSDataOutputStream;
import org.apache.hadoop.fs.FileChecksum;
import org.apache.hadoop.fs.FileStatus;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

import java.io.IOException;
import java.net.URI;
import java.nio.ByteBuffer;

public class Demo {
    private static FileSystem initFS() throws IOException {
        Configuration conf = new Configuration();
        // For more information on COSN configuration items, visit https://cloud.tencent.com/document/product/436/6884#hadoop-.E9.85.8D.E7.BD.AE.
        // The following configuration items are required
        conf.set("fs.cosn.impl", "org.apache.hadoop.fs.CosFileSystem");
        conf.set("fs.AbstractFileSystem.cosn.impl", "org.apache.hadoop.fs.CosN");
        conf.set("fs.cosn.tmp.dir", "/tmp/hadoop_cos");
        conf.set("fs.cosn.bucket.region", "ap-guangzhou");
        conf.set("fs.cosn.userinfo.secretId", "AKXXXXXXXXXXXXXXXXX");
        conf.set("fs.cosn.userinfo.secretKey", "XXXXXXXXXXXXXXXXXX");
        conf.set("fs.ofs.user.appid", "XXXXXXXXXXX");
        // For more information on other configuration items, visit https://cloud.tencent.com/document/product/436/6884#hadoop-.E9.85.8D.E7.BD.AE.
        // Whether to enable CRC-64 checksum. It is disabled by default, meaning that you can’t run the `hadoop fs -checksum` command to obtain the CRC-64 checksum of a file.
        conf.set("fs.cosn.crc64.checksum.enabled", "true");
        String cosnUrl = "cosn://f4mxxxxxxxx-125xxxxxxx";
        return FileSystem.get(URI.create(cosnUrl), conf);
    }

    private static void mkdir(FileSystem fs, Path filePath) throws IOException {
        fs.mkdirs(filePath);
    }

    private static void createFile(FileSystem fs, Path filePath) throws IOException {
        // Create a file (if it already exists, it will be overwritten)
        // if the parent dir does not exist, fs will create it!
        FSDataOutputStream out = fs.create(filePath, true);
        try {
            // Write a file
            String content = "test write file";
            out.write(content.getBytes());
        } finally {
            IOUtils.closeQuietly(out);
        }
    }

    private static void readFile(FileSystem fs, Path filePath) throws IOException {
        FSDataInputStream in = fs.open(filePath);
        try {
            byte[] buf = new byte[4096];
            int readLen = -1;
            do {
                readLen = in.read(buf);
            } while (readLen >= 0);
        } finally {
            IOUtils.closeQuietly(in);
        }
    }

    private static void queryFileOrDirStatus(FileSystem fs, Path path) throws IOException {
        FileStatus fileStatus = fs.getFileStatus(path);
        if (fileStatus.isDirectory()) {
            System.out.printf("path %s is dir\n", path);
            return;
        }
        long fileLen = fileStatus.getLen();
        long accessTime = fileStatus.getAccessTime();
        long modifyTime = fileStatus.getModificationTime();
        String owner = fileStatus.getOwner();
        String group = fileStatus.getGroup();

        System.out.printf("path %s is file, fileLen: %d, accessTime: %d, modifyTime: %d, owner: %s, group: %s\n",
                path, fileLen, accessTime, modifyTime, owner, group);
    }
    
    private static void getFileCheckSum(FileSystem fs, Path path) throws IOException {
        FileChecksum checksum = fs.getFileChecksum(path);
        System.out.printf("path %s, checkSumType: %s, checkSumCrcVal: %d\n",
                path, checksum.getAlgorithmName(), ByteBuffer.wrap(checksum.getBytes()).getInt());
    }

    private static void copyFileFromLocal(FileSystem fs, Path cosnPath, Path localPath) throws IOException {
        fs.copyFromLocalFile(localPath, cosnPath);
    }

    private static void copyFileToLocal(FileSystem fs, Path cosnPath, Path localPath) throws IOException {
        fs.copyToLocalFile(cosnPath, localPath);
    }

    private static void renamePath(FileSystem fs, Path oldPath, Path newPath) throws IOException {
        fs.rename(oldPath, newPath);
    }

    private static void listDirPath(FileSystem fs, Path dirPath) throws IOException {
        FileStatus[] dirMemberArray = fs.listStatus(dirPath);

        for (FileStatus dirMember : dirMemberArray) {
            System.out.printf("dirMember path %s, fileLen: %d\n", dirMember.getPath(), dirMember.getLen());
        }
    }

    // The recursive deletion flag is used to delete directories
    // If recursion is `false` and `dir` is not empty, the operation will fail
    private static void deleteFileOrDir(FileSystem fs, Path path, boolean recursive) throws IOException {
        fs.delete(path, recursive);
    }

    private static void closeFileSystem(FileSystem fs) throws IOException {
        fs.close();
    }

    public static void main(String[] args) throws IOException {
        // Initialize a file
        FileSystem fs = initFS();

        // Create a file
        Path cosnFilePath = new Path("/folder/exampleobject.txt");
        createFile(fs, cosnFilePath);

        // Read a file
        readFile(fs, cosnFilePath);

        // Query a file or directory
        queryFileOrDirStatus(fs, cosnFilePath);

        // Get a file checksum
        getFileCheckSum(fs, cosnFilePath);

        // Copy a file from the local system
        Path localFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
        copyFileFromLocal(fs, cosnFilePath, localFilePath);

        // Download a file to the local file system
        Path localDownFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
        copyFileToLocal(fs, cosnFilePath, localDownFilePath);

        listDirPath(fs, cosnFilePath);
        // Rename
        mkdir(fs, new Path("/doc"));
        Path newPath = new Path("/doc/example.txt");
        renamePath(fs, cosnFilePath, newPath);

        // Delete a file
        deleteFileOrDir(fs, newPath, false);

        // Create a directory
        Path dirPath = new Path("/folder");
        mkdir(fs, dirPath);

        // Create a file in a directory
        Path subFilePath = new Path("/folder/exampleobject.txt");
        createFile(fs, subFilePath);

        // List directories
        listDirPath(fs, dirPath);

        // Delete a directory
        deleteFileOrDir(fs, dirPath, true);
        deleteFileOrDir(fs, new Path("/doc"), true);

        // Close a file system
        closeFileSystem(fs);
    }
}
```

## FAQs
If you have any questions about Hadoop-COS, see [FAQs > Tools > Hadoop](https://www.tencentcloud.com/document/product/436/35706).
