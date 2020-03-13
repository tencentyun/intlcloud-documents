#### Feature
COS Migration is an all-in-one tool that integrates COS data migration feature. Users can quickly migrate data from various sources to COS through simple configurations and steps. It has the following features:
- Diverse data sources:
   - Local data: Migrate locally stored data to COS.
   - Other cloud storage services: Currently, it supports migration from AWS S3, Alibaba Cloud OSS, and Qiniu to COS. More services will be supported in the future.
   - URL list: Download and migrate data from specified URLs to COS.
   - Bucket replication: Data can be replicated among COS buckets. Cross-account and cross-region replication is supported.
- Resume upload from breakpoints: Resume uploads from breakpoints is supported. For large files, if the upload exits halfway or service failure occurs, you can run the tool again to resume the upload.
- Multipart upload: An object can be uploaded to COS by parts.
- Parallel upload: Multiple objects can be uploaded at the same time.
- Migration verification: Migrated objects can be verified.

>
>- COS Migration only supports UTF-8 encoding.
>- If you use this tool to upload a file whose name already exists, the older file will be overwritten. File name duplication cannot be checked.

## Operating Environment
### System Environment
Windows, Linux, and macOS.

### Software Requirements
- JDK 1.8 X64 or above. For more information on JDK installation and configuration, see [Java](https://intl.cloud.tencent.com/document/product/436/10865).

## Usage
### 1. Get the tool
Download COS Migration [here](https://github.com/tencentyun/cos_migrate_tool_v5).

### 2. Decompress the package
#### Windows
 Decompress the package and save it to a directory, for example:
<pre>
C:\Users\Administrator\Downloads\cos_migrate
</pre>

#### Linux
Decompress the package and save it to a directory, for example:
<pre>
unzip cos_migrate_tool_v5-master.zip && cd cos_migrate_tool_v5-master
</pre>

#### Migration tool structure
The structure of the properly decompressed COS Migration tool is as follows:
<pre>
COS_Migrate_tool
|——conf  #Directory of the configuration file
|   |——config.ini  #Migrate the configuration file
|——db    #Store the record of successful migrations
|——dep   #JAR package complied by the main logic of the program
|——log   #Log generated during tool execution
|——opbin #Script for compiling
|——src   #Source code of the tool
|——tmp   #Temporary file storage directory
|——pom.xml #Project configuration file
|——README  #Readme document
|——start_migrate.sh  #Migration startup script for Linux
|——start_migrate.bat #Migration startup script for Windows
</pre>

>
 - The db directory mainly records the IDs of files successfully migrated by the tool. Each migration job will first compare the records in db directory. If the ID of the current file has already been recorded, the current file will be skipped, otherwise it will be migrated.
 - The log directory keeps all the logs generated during tool migration. If an error occurs during migration, first check the error.log under this directory.

### 3. Modify the config.ini file
Before running the migration startup script, modify the config.ini file (path: `./conf/config.ini`) first. This file contains the following parts:

#### 3.1 Configure the migration type
type indicates the migration type, which is filled in by users based on their migration needs. For example, to migrate local data to COS, users need to configure `type=migrateLocal` for `[migrateType]`.
<pre>[migrateType]
type=migrateLocal
</pre>

Currently, the following migration types are supported:

| migrateType | Description |
| ------| ------ |
| migrateLocal| From local system to COS |
| migrateAws| From AWS S3 to COS |
| migrateAli | From Alibaba Cloud OSS to COS |
| migrateQiniu | From Qiniu to COS |
| migrateUrl | From download URL to COS |
| migrateBucketCopy| From source bucket to destination bucket |
|migrateUpyun | From UpYun to COS |

#### 3.2 Configure the migration job
You can configure a migration job based on your actual needs, including information configuration for the destination COS and job-related configurations.
<pre>
# The common configuration section of the migration tool includes account information to be migrated to the destination COS.
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
| bucketName | Name of the destination bucket in the format of `<BucketName-APPID>`. The bucket name must include the APPID such as examplebucket-1250000000 |-|
| region | Region information of the destination bucket. For region abbreviations in COS, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) |-|
| storageClass | Storage class: Standard (standard storage), Standard_IA (standard infrequent access storage), or Archive (archive storage) | Standard |
| cosPath | COS path to migrate to. `/` indicates to migrate to the root path of the bucket, `/folder/doc/` indicates to migrate to `/folder/doc/` in the bucket. If `/folder/doc/` does not exist, a path will be created automatically |/|
| https | Whether to transfer via HTTPS. on :Yes, off: No. It takes time to enable transfer via HTTPS, which is suitable for scenarios that demand high security. | off |
| tmpFolder | The directory used to store temporary files when data is migrated from another cloud storage service to COS, which will be deleted after the migration is completed. The format must be an absolute path: <br>The separator on Linux is /, such as `/a/b/c`<br>The separator on Windows is \\, such as `E:\\a\\b\\c`<br>The default value is the tmp directory in the path of the tool | ./tmp |
| smallFileThreshold| Number of bytes as the threshold for small files. If the size is greater than or equal to this threshold, multipart upload is used; otherwise, simple upload is used. The default value is 5 MB | 5242880 |
| smallFileExecutorNum | Concurrency for uploading small files (smaller than smallFileThreshold) via simple upload. Decrease the concurrency if files are uploaded to COS via public network with low bandwidth | 64 |
| bigFileExecutorNum | Concurrency for uploading large files (greater than or equal to smallFileThreshold) via multipart upload. Decrease the concurrency if files are uploaded to COS via public network with low bandwidth | 8 |
| entireFileMd5Attached | The migration tool calculates the MD5 of the entire file and stores it in the custom header "x-cos-meta-md5" of the file for subsequent verification, because the etag of a large file uploaded to COS via multipart upload is not the MD5 of the entire file | on |
| daemonMode | Whether to enable daemon mode. on: yes; off: no. In daemon mode, the program will keep performing synchronization. The synchronization interval is configured by the daemonModeInterVal parameter | off |
| daemonModeInterVal | Time interval in seconds between two rounds of synchronization | 60 |
| executeTimeWindow | Execution time window with a granularity in minute, which defines the time period when the migration tool runs jobs. For example: <br>03:30, 21:00 means that jobs will be run between 03:30 and 21:00, and the tool is in sleep mode at other times, when the migration will be paused and the progress will be retained until the next time window when the migration will resume automatically | 00:00,24:00 |
| encryptionType | SSE-COS is used for server encryption | This is left blank by default. Enter if server encryption is needed |

#### 3.3 Configure the data source
Configure each section according to the migration type described in `[migrateType]`. For example, if the configuration item of `[migrateType]` is `type=migrateLocal`, users only need to configure the `[migrateLocal]` section.

**3.3.1 Configure a local data source migrateLocal**

If you migrate from a local system to COS, configure this section. The specific configuration items and descriptions are as follows:
<pre>
# Configuration section for migration from a local system to COS
[migrateLocal]
localPath=E:\\code\\java\\workspace\\cos_migrate_tool\\test_data
excludes=
ignoreModifiedTimeLessThanSeconds=
</pre>

| Configuration Item | Description |
| ------| ------ |
| localPath | Local path in the format of an absolute path: <br>The separator on Linux is /, such as `/a/b/c` <br>The separator on Windows is \\, such as `E:\\a\\b\\c` |
| excludes | Absolute path of the directory or file to be excluded, meaning some directories or files under localPath are not to be migrated. Multiple absolute paths are separated by semicolons. If this is left blank, all files in the localPath will be migrated |
| ignoreModifiedTimeLessThanSeconds | Exclude files whose update time is less than a certain period of time from the current time. Unit in seconds. This is left blank by default, indicating files are not to be filtered by lastmodified time. This is suitable for scenarios where users run the migration tool while updating files, and do not want files being updated to be migrated to COS. For example, if this is configured as 300, only files updated at least 5 minutes ago will be uploaded |

**3.3.2 Configure an Alibaba Cloud OSS data source migrateAli**

If you migrate from Alibaba Cloud OSS to COS, configure this section. The specific configuration items and descriptions are as follows:
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
|accessKeyId| Replace AccessKeyId with your key |
|accessKeySecret| Replace AccessKeySecret with your key |
|endPoint| Address of the Alibaba Cloud endpoint |
|prefix| Prefix of the path to be migrated. If all data in the bucket needs to be migrated, leave the prefix blank |
|proxyHost| If you want to use a proxy for access, enter the proxy IP address |
|proxyPort| Proxy port |

**3.3.3 Configure an AWS data source migrateAws**

If you migrate from AWS to COS, configure this section. The specific configuration items and descriptions are as follows:
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
|accessKeyId| Replace AccessKeyId with your key |
|accessKeySecret| Replace SecretAccessKey with your key |
|endPoint| Address of the AWS endpoint, which must be a domain name instead of region |
|prefix| Prefix of the path to be migrated. If all data in the bucket needs to be migrated, leave the prefix blank |
|proxyHost| If you want to use a proxy for access, enter the proxy IP address |
|proxyPort| Proxy port |

 
**3.3.4 Configure a Qiniu data source migrateQiniu**

If you migrate from Qiniu to COS, configure this section. The specific configuration items and descriptions are as follows:
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
|accessKeyId| Replace AccessKey with your key |
|accessKeySecret| Replace SecretKey with your key |
|endPoint| Download address of Qiniu, which corresponds to downloadDomain |
|prefix| Prefix of the path to be migrated. If all data in the bucket needs to be migrated, leave the prefix blank |
|proxyHost| If you want to use a proxy for access, enter the proxy IP address |
|proxyPort| Proxy port |

 
**3.3.5 Configure a URL list data source migrateUrl**

If you migrate from a specified URL list to COS, configure this section. The specific configuration items and descriptions are as follows:
<pre>
# Configuration section for migration from a URL list to COS
[migrateUrl]
urllistPath=D:\\folder\\urllist.txt
</pre>
     
| Configuration Item | Description |
| ------| ------ |
|urllistPath| Address of the URL list, whose content is URL text with one original URL address per line (such as `http://aaa.bbb.com/yyy/zzz.txt`, no need to add any double quotation marks or other symbols). The address of the URL list must be an absolute path: <br>The separator on Linux is /, such as `/a/b/c.txt` <br>The separator on Windows is \\, such as `E:\\a\\b\\c.txt` <br>If a directory is entered, all files under the directory will be treated as urllist files for scan and migration |

 
**3.3.6 Configure bucket replication migrateBucketCopy**

If you migrate from one COS bucket to another bucket, configure this section. The specific configuration items and descriptions are as follows:
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
|srcRegion| Region information of the source bucket. For more information, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) |
|srcBucketName| Name of the source bucket in the format of `<BucketName-APPID>`. The bucket name must include the APPID, such as examplebucket-1250000000 |
|srcSecretId| SecretId of the user who owns the source bucket, which can be viewed in [Cloud API Key Management](https://console.cloud.tencent.com/cam/capi). If the data is owned by the same user, srcSecretId is the same as the SecretId in the common section, otherwise the migration is cross-account bucket copy |
|srcSecretKey| SecretKey of the user who owns the source bucket, which can be viewed in [Cloud API Key Management](https://console.cloud.tencent.com/cam/capi). If the data is owned by the same user, srcSecretKey is the same as the secretKey in the common section, otherwise, the migration is cross-account bucket copy |
|srcCosPath| The COS path to be migrated, meaning files in this path will be migrated to the destination bucket |

**3.3.7 Configure UpYun data source migrateUpyun**
When you migrate from a local system to COS, configure this section. The specific configuration items and descriptions are as follows:

```
[migrateUpyun]
# Migrate from UpYun
bucket=xxx
# ID of the UpYun operator
accessKeyId=xxx
# Password of the UpYun operator     
accessKeySecret=xxx       
prefix=

# UpYun sdk restriction, this proxy will be configured as a global proxy
proxyHost=
proxyPort=
```

| Configuration Item | Description |
| ------| ------ |
|bucket| Name of the UpYun bucket |
|accessKeyId| Replace with the ID of the UpYun operator |
|accessKeySecret| Replace with the password of the UpYun operator |
|prefix| Prefix of the path to be migrated. If all data in the bucket needs to be migrated, leave the prefix blank |
|proxyHost| If you want to use a proxy for access, enter the proxy IP address |
|proxyPort| Proxy port |

### 4. Run the migration tool
#### Windows
Double-click **start_migrate.bat** to run the tool

#### Linux
1. Read into configurations from the config.ini file. The run command is:
<pre>
sh start_migrate.sh
</pre>
2. Read into configurations from command lines for some parameters. The run command is:
<pre>
sh start_migrate.sh -Dcommon.cosPath=/savepoint0403_10/
</pre>

>
>- The tool supports reading configuration items in two ways: command line or configuration file.
>- The command line takes priority over the configuration file, i.e., for the same configuration item, parameters in command lines take priority.
>- Reading configuration items from command lines allows users to run different migration jobs at the same time, provided that key configuration items (such as bucket name, COS path, source path to be migrated, etc.) in the two jobs are not exactly the same. Concurrent migration can be achieved because different migration jobs are written into different db directories. Please refer to db information in tool structure above.
>- Configuration items are in the format of **-D{sectionName}.{sectionKey}={sectionValue}**. sectionName is the section name of the configuration file. sectionKey is the name of the configuration item in the section. sectionValue is the value of the configuration item in the section. COS path to which data is migrated to should be in the format of **-Dcommon.cosPath=/bbb/ddd**.

## Migration mechanism and process
### Migration Mechanism
COS migration tool has a status. Successful migrations will be recorded in the format of KV in leveldb file under db directory. Before each migration, check whether the path to which data is migrated to has been recorded in db directory. If yes and its attribute is the same as that in db, the migration will be skipped. Otherwise, the migration will be executed. The attribute varies by migration type. For local migration, mtime determines whether to migrate. For migration from other cloud storage services and bucket replication, etag and length of the source file determine whether to migrate. Thus, we search for records of successful migrations in db rather than in COS. If a file is deleted or modified via COSCMD or the console rather than the migration tool, the migration tool cannot detect this change and the file will not be re-migrated.

### Migration Process
1. The configuration file is read, the corresponding configuration section is read according to the migration type, and parameters are checked.
2. The IDs of the files to be migrated are scanned and compared in db directory according to the specified migration type to determine whether upload is allowed.
3. The execution results are printed out during migration, where inprogress indicates migration is in progress, skip indicates skipped, fail indicates failed, ok indicates succeeded, condition_not_match indicates file fails to meet migration conditions (such as lastmodified and excludes) and is skipped. Details about the failure can be viewed in error log. The execution process is shown below:
 ![](https://main.qcloudimg.com/raw/7561d07ea315c9bacbb228b36d6ad6d6.png)
4. Statistics are printed out after the migration is completed, which include the total number of migrated, failed, and skipped files as well as the amount of time consumed. For failures, check the error log, or rerun the migration job as the migration tool will skip successfully migrated files and retry migrating failed ones. The execution result of a migration job is shown below:
![](https://main.qcloudimg.com/raw/2534fd390218db29bb03f301ed2620c8.png)

## FAQ
If an exception such as migration failure or execution error occurs when you use COS Migration tool, see [COS Migration Tool](https://intl.cloud.tencent.com/document/product/436/30585) for troubleshooting.
