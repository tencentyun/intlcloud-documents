## Feature Description
COS Migration is an all-in-one COS data migration tool that enables you to quickly migrate your data from various sources to COS through simple configurations and steps. It has the following features:
- Support for various data sources:
   - Local data: Migrate locally stored data to COS.
   - Other cloud storage services: Currently, it supports migration from AWS S3, Alibaba Cloud OSS, and Qiniu to COS. More service providers will be supported in the future.
   - URL list: Download and migrate data from the specified URL download list to COS.
   - Bucket replication: The data can be replicated among COS buckets. Cross-account cross-region replication is supported.
- Resume capability: Upload resuming is supported. When uploading large files, if you close the tool midway or the upload gets interrupted due to a service failure, the tool can be run again to resume the upload.
- Multipart upload: An object can be uploaded to COS in multiple parts.
- Parallel upload: Multiple objects can be uploaded at the same time.
- Migration verification: Migrated objects can be verified.

>
>- COS Migration only supports UTF-8 for encoding.
>- If you upload a file through this tool, an existing file with the same name will be overwritten. Detection of filename duplication is not supported.

## Prerequisites
### OS
Windows, Linux, or macOS.

### Software Dependency
- JDK 1.8 X64 or above. For more information about JDK installation and configuration, see [Java Installation and Configuration](https://intl.cloud.tencent.com/document/product/436/10865).

## How to Use
### 1. Get the tool
Download COS Migration [here](https://github.com/tencentyun/cos_migrate_tool_v5).

### 2. Decompress the package
#### Windows
 Decompress the package to a local directory, for example:
<pre>
C:\Users\Administrator\Downloads\cos_migrate
</pre>

#### Linux
Decompress the package to a local directory, for example:
<pre>
unzip cos_migrate_tool_v5-master.zip && cd cos_migrate_tool_v5-master
</pre>

#### Migration tool structure
The structure of the properly decompressed COS Migration folder is as follows:
<pre>
COS_Migrate_tool
|——conf  # Directory of the configuration file
|   |——config.ini  # Migration configuration file
|——db    # Record of storage migration successes
|——dep   # JAR package complied by the main logic of the program
|——log   # Log generated during tool execution
|——opbin # Script for compiling
|——src   # Source code of the tool
|——tmp   # Temporary file storage directory
|——pom.xml # Project configuration file
|——README  # Readme document
|——start_migrate.sh  # Migration startup script for Linux
|——start_migrate.bat # Migration startup script for Windows
</pre>


> - The db directory mainly records the IDs of files successfully migrated by the tool. For each migration task, the IDs in db will be compared first, and if the ID of the current file has already been recorded, the current file will be skipped; otherwise, it will be migrated.
> - The log directory keeps all the logs generated during migration. If an error occurs, please check the error.log in this directory first.

### 3. Modify the config.ini file
Before running the migration startup script, you need to modify the config.ini file (path: `./conf/config.ini`) first. This file contains the following parts:

#### 3.1 Configure the migration type
type indicates the migration type, and you should enter the corresponding identifier based on your migration needs. For example, if you need to migrate local data to COS, configure `[migrateType]` as `type=migrateLocal`.
<pre>[migrateType]
type=migrateLocal
</pre>

Currently supported migration types include:

| migrateType | Description |
| ------| ------ |
| migrateLocal| From local system to COS |
| migrateAws| From AWS S3 to COS |
| migrateAli | From Alibaba Cloud OSS to COS |
| migrateQiniu | From Qiniu to COS |
| migrateUrl | From download URL to COS |
| migrateBucketCopy| From source bucket to destination bucket |

#### 3.2 Configure the migration task
You can configure a migration task based on your actual migration needs. Main configuration items include the destination COS bucket and task properties.
<pre>
# The common configuration section of the migration tool, containing account information of the destination COS bucket.
[common]
secretId=COS_SECRETID
secretKey=COS_SECRETKEY
bucketName=examplebucket-1250000000
region=ap-guangzhou
storageClass=Standard
cosPath=/
https=off
tmpFolder=./tmp
smallFileThreshold=5242880
smallFileExecutorNum=64
bigFileExecutorNum=8
entireFileMd5Attached=on
daemonMode=off
daemonModeInterVal=60
executeTimeWindow=00:00,24:00
encryptionType=sse-cos
</pre>

| Name | Description | Default Value |
| ------| ------ |----- |
| secretId | SecretId of your key. Replace `COS_SECRETID` with your real key information, which can be obtained on the TencentCloud API key page in the [CAM Console](https://console.cloud.tencent.com/cam/capi) |-|
| secretKey | SecretKey of your key. Replace `COS_SECRETKEY` with your real key information, which can be obtained on the TencentCloud API key page in the [CAM Console](https://console.cloud.tencent.com/cam/capi) |-|
| bucketName | Name of the destination bucket in the format of `<BucketName-APPID>`. The bucket name must contain the APPID such as examplebucket-1250000000 |-|
| region | Region information of the destination bucket. For the region abbreviations in COS, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) |-|
| storageClass | Storage class: Standard (standard storage), Standard_IA (standard infrequent access storage), or Archive (archive storage) | Standard |
| cosPath | The COS path to migrate to. `/` indicates to migrate to the root path of the bucket, `/folder/doc/` indicates to migrate to `/folder/doc/` in the bucket. If `/folder/doc/` does not exist, it will be created automatically |/|
| https | Whether to use HTTPS for transfer. on: yes; off: no. If this is enabled, the transfer will be slow. This is suitable for scenarios with high transfer security requirements | off |
| tmpFolder | The folder used to store temporary files when data is migrated from another cloud storage service to COS, which will be deleted after the migration is completed. The path has to be an absolute path: <br>The separator on Linux is /, such as `/a/b/c` <br>The separator on Windows is \\, such as `E:\\a\\b\\c` <br>The default value is the tmp directory in the path of the tool | ./tmp |
| smallFileThreshold| Number of bytes as the threshold for small files. If the data size is higher than or equal to this threshold, multipart upload is used; otherwise, simple upload is used. The default value is 5 MB | 5242880 |
| smallFileExecutorNum | Concurrence of small files (i.e., the size is lower than smallFileThreshold). Simple upload is used. If the COS is connected to from a public network with low bandwidth, reduce this value | 64 |
| bigFileExecutorNum | Concurrence of large files (i.e., the size is higher than or equal to smallFileThreshold). Multipart upload is used. If the COS is connected to from a public network with low bandwidth, reduce this value | 8 |
| entireFileMd5Attached | This indicates whether the migration tool calculates the MD5 of the entire file and stores it in the custom header "x-cos-meta-md5" of the file for subsequent verification, because the etag of a large file uploaded to COS in multiple parts is not the MD5 of the entire file | on |
| daemonMode | Whether to enable daemon mode. on: yes; off: no. In daemon mode, the program will keep performing synchronization in a loop. The synchronization interval is set by the daemonModeInterVal parameter | off |
| daemonModeInterVal | This indicates the interval in seconds between two rounds of synchronization | 60 |
| executeTimeWindow | Execution time window with a granularity of one minute, which defines the time period during which the migration tool runs tasks. For example: <br>03:30,21:00 means that tasks will be run between 03:30 and 21:00 and enter sleep mode at other times. In sleep mode, the migration will be paused and the migration progress will be retained until the next time window when the migration will be resumed automatically | 00:00,24:00 |
| encryptionType | This indicates to use SSE-COS server-side encryption | This is left blank by default. Enter if server-side encryption is needed |

#### 3.3 Configure the data source
Configure the appropriate section according to the migration type `[migrateType]`. For example, if the configuration information of `[migrateType]` is `type=migrateLocal`, then you only need to configure the `[migrateLocal]` section.

**3.3.1 Configure a local data source "migrateLocal"**

If you are migrating from a local system to COS, configure this section. The specific configuration items and descriptions are as follows:
<pre>
# Configuration section for migration from a local system to COS
[migrateLocal]
localPath=E:\\code\\java\\workspace\\cos_migrate_tool\\test_data
exeludes=
ignoreModifiedTimeLessThanSeconds=
</pre>

| Configuration Item | Description |
| ------| ------ |
| localPath | Local path which should be an absolute path: <br>The separator on Linux is / such as `/a/b/c` <br>The separator on Windows is \\, such as `E:\\a\\b\\c`|
| excludes | Absolute path of the directory or file to be excluded, which means that some directories or files in the localPath are not to be migrated. Multiple absolute paths are separated by semicolons. If this is left blank, all files in the localPath are to be migrated |
| ignoreModifiedTimeLessThanSeconds | Exclude files whose updated time differs from the current time by less than the specified period of time in seconds. This is left blank by default, indicating that the files are not to be filtered by the lastmodified time. This is applicable to scenarios where you run the migration tool while updating files and want the files being updated not to be migrated to COS. For example, if this is set to 300, only files updated at least 5 minutes ago will be uploaded |

**3.3.2 Configure an Alibaba Cloud OSS data source "migrateAli"**

If you are migrating from Alibaba Cloud OSS to COS, configure this section. The specific configuration items and descriptions are as follows:
<pre># Configuration section for migration from Alibaba Cloud OSS to COS
[migrateAli]
bucket=bucket-aliyun
accessKeyId=yourAccessKeyId
accessKeySecret=yourAccessKeySecret
endPoint= oss-cn-hangzhou.aliyuncs.com
prefix=
proxyHost=
proxyPort=
</pre>

| Configuration Item | Description |
| ------| ------ |
|bucket| Name of the Alibaba Cloud OSS bucket |
|accessKeyId| Replace with your AccessKeyId |
|accessKeySecret| Replace with your AccessKeySecret |
|endPoint| Address of the Alibaba Cloud endpoint |
|prefix| Prefix of the path to be migrated. If all data in the bucket is to be migrated, leave the prefix blank |
|proxyHost| If you want to use a proxy for access, enter the proxy IP address |
|proxyPort| Proxy port |

**3.3.3 Configure an AWS data source "migrateAws"**

If you are migrating from AWS to COS, configure this section. The specific configuration items and descriptions are as follows:
<pre># Configuration section for migration from AWS to COS
[migrateAws]
bucket=bucket-aws
accessKeyId=AccessKeyId
accessKeySecret=SecretAccessKey
endPoint=s3.us-east-1.amazonaws.com
prefix=
proxyHost=
proxyPort=
</pre>

| Configuration Item | Description |
| ------| ------ |
|bucket| Name of the AWS bucket |
|accessKeyId| Replace with your AccessKeyId |
|accessKeySecret| Replace with your SecretAccessKey |
|endPoint| Address of the AWS endpoint, which has to be a domain name instead of region |
|prefix| Prefix of the path to be migrated. If all data in the bucket is to be migrated, leave the prefix blank |
|proxyHost| If you want to use a proxy for access, enter the proxy IP address |
|proxyPort| Proxy port |


**3.3.4 Configure a Qiniu data source "migrateQiniu"**

If you are migrating from Qiniu to COS, configure this section. The specific configuration items and descriptions are as follows:
<pre># Configuration section for migration from Qiniu to COS
[migrateQiniu]
bucket=bucket-qiniu
accessKeyId=AccessKey
accessKeySecret=SecretKey
endPoint=www.bkt.clouddn.com
prefix=
proxyHost=
proxyPort=
</pre>

| Configuration Item | Description |
| ------| ------ |
|bucket| Name of the Qiniu bucket |
|accessKeyId| Replace with your AccessKey |
|accessKeySecret| Replace with your SecretKey |
|endPoint| Download address of Qiniu, which corresponds to downloadDomain |
|prefix| Prefix of the path to be migrated. If all data in the bucket is to be migrated, leave the prefix blank |
|proxyHost| If you want to use a proxy for access, enter the proxy IP address |
|proxyPort| Proxy port |


**3.3.5 Configure a URL list data source "migrateUrl"**

If you are migrating from a specified URL list to COS, configure this section. The specific configuration items and descriptions are as follows:
<pre>
# Configuration section for migration from a URL list to COS
[migrateUrl]
urllistPath=D:\\folder\\urllist.txt
</pre>

| Configuration Item | Description |
| ------| ------ |
|urllistPath| Address of the URL list, which is URL text containing one original URL address per line, such as `http://aaa.bbb.com/yyy/zzz.txt`. There is no need to add any double quotation marks or other symbols. The address of the URL list has to be an absolute path: <br>The separator on Linux is / such as `/a/b/c.txt` <br>The separator on Windows is \\ such as `E:\\a\\b\\c.txt` <br>If a directory is entered, all the files in the directory will be treated as urllist files for scan  and migration |


**3.3.6 Configure bucket replication "MigrateBucketCopy"**

If you are migrating from one COS bucket to another bucket, configure this section. The specific configuration items and descriptions are as follows:
<pre>
# Configuration section for migration from source bucket to destination bucket
[migrateBucketCopy]
srcRegion=ap-shanghai
srcBucketName=examplebucket-1250000000
srcSecretId=COS_SECRETID
srcSecretKey=COS_SECRETKEY
srcCosPath=/
</pre>

| Configuration Item | Description |
| ------| ------ |
|srcRegion| Region information of the source bucket. For more information, see [Available Regions](https://intl.cloud.tencent.com/document/product/436/6224) |
|srcBucketName| Name of the source bucket in the format of `<BucketName-APPID>`. The bucket name must contain the APPID such as examplebucket-1250000000 |
|srcSecretId| SecretId of the key of the account owning the source bucket, which can be viewed in [TencentCloud API Key](https://console.cloud.tencent.com/cam/capi). If the data is owned by the same user, srcSecretId is the same as the SecretId in the common section; otherwise, the migration is cross-account |
|srcSecretKey| SecretKey of the key of the account owning the source bucket, which can be viewed in [TencentCloud API Key](https://console.cloud.tencent.com/cam/capi). If the data is owned by the same user, srcSecretKey is the same as the secretKey in the common section; otherwise, the migration is cross-account |
|srcCosPath| The COS path to be migrated, indicating that the files in this path are to be migrated to the destination bucket |


### 4. Run the migration tool
#### Windows
Double-click **start_migrate.bat** to run it.

#### Linux
1. Read the configuration from the config.ini file. The run command is:
<pre>
sh start_migrate.sh
</pre>
2. Read the configuration of some parameters from the command line. The run command is:
<pre>
sh start_migrate.sh -Dcommon.cosPath=/savepoint0403_10/
</pre>

>
> - The tool supports reading configuration items in two ways: command line or configuration file.
> - The command line takes precedence over the configuration file, i.e., for the same configuration item, the parameter in the command line takes precedence.
> - Reading configuration items from the command line makes it convenient for you to run different migration tasks simultaneously, provided that the key configuration items in the tasks are different, such as the bucket name, COS path, and source path to be migrated, because data in different migration tasks is written to different db directories to make possible concurrent migrations. For more information, see the db information in the tool structure above.
> - The configuration item is in the form of **-D{sectionName}.{sectionKey}={sectionValue}**, where sectionName is the name of the section in the configuration file, sectionKey the name of the configuration item in the section, and sectionValue the value of the configuration item. For example, if you want to set the COS path to migrate to, it can be represented by **-Dcommon.cosPath=/bbb/ddd**.

## Migration Mechanism and Process
### How Migration Works
COS Migration is stateful, and the files successfully migrated are recorded in the db directory and stored in the leveldb file in the form of KV. Before each migration is started, presence of the path to be migrated is first checked in the db directory. If it exists and its attributes are the same as those in db, the migration is skipped; otherwise, the migration is performed. The attributes here vary by migration type. For migrations from a local system, mtime is checked. For migrations from other cloud storage services and bucket replication, it is checked whether the length of the source file's etag is the same as that in db. Therefore, instead of finding a file in COS, db should be checked to see whether it has a successfully migrated record there. If a file is deleted or modified by another means (such as COSCMD or console) and COS Migration is bypassed, COS Migration will not migrate the file again as it cannot perceive the change.

### Migration Steps
1. The configuration file is read, the corresponding configuration section is read according to the migration type, and the parameters are checked.
2. The IDs of the files to be migrated are scanned for and compared in the db directory according to the migration type to decide whether upload is allowed.
3. The execution results are printed out during the migration process, where inprogress indicates migration in progress, skip indicates skipped, fail indicates failed, ok indicates succeeded, and condition_not_match indicates file skipped as it does not meet the migration conditions (such as lastmodified and excludes). The details of the failure can be viewed in the error log in the log directory. Below is an example of the execution process:
 ![](https://main.qcloudimg.com/raw/7561d07ea315c9bacbb228b36d6ad6d6.png)
4. Statistics is printed out after the migration is completed, including total number of migrated, failed, and skipped files as well as the amount of time consumed. For failures, check the error logs or rerun the migration task as the migration tool will skip successfully migrated files and retry migrating the failed ones. Below is an example of execution result of a migration task:
![](https://main.qcloudimg.com/raw/2534fd390218db29bb03f301ed2620c8.png)

## FAQs
If an error such as migration failure or exceptional execution occurs during the use of COS Migration, see [FAQs for COS Migration](https://intl.cloud.tencent.com/document/product/436/30585) for troubleshooting.

