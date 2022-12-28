## Overview
The HDFS TO COS tool is used to copy data from HDFS to Tencent Cloud COS（Cloud Object Storage）.

## Operating Environments
#### Operating system
Linux or Windows

#### Software dependency
JDK v1.7 or v1.8 

#### Installation and configuration
For more information on environment installation and configuration, see [Java](https://intl.cloud.tencent.com/document/product/436/10865).

## Configuration Method
1. Install Hadoop v2.7.2 or higher. For detailed directions, see [Hadoop](https://intl.cloud.tencent.com/document/product/436/10867).
2. Download the HDFS TO COS tool from [GitHub](https://github.com/tencentyun/hdfs_to_cos_tools) and decompress it.
3. Copy the `core-site.xml` file of the HDFS cluster to be synced to the `conf` folder. The `core-site.xml` file contains the configuration information of NameNode.
4. In the `cos_info.conf` configuration file, configure the bucket, region, and API key information. The bucket name is formed by connecting a user-defined string and the system-generated `APPID` with a hyphen, for example, `examplebucket-1250000000`.
5. Specify the configuration file location in the command line parameter. The default location is `conf/cos_info.conf`.
>!If the command line parameter conflicts with the configuration file, the command line parameter shall apply.

## Usage

>?Linux is used as an example below.

### Viewing help

```
./hdfs_to_cos_cmd -h
```


### Copying a file

- Copy from HDFS to COS. If a file with the same name as the file to be copied already exists in COS, the former will be overwritten.
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
- Copy from HDFS to COS. If a file with the same name and length as the file to be copied already exists in COS, the latter will be skipped (this is suitable for repeated copy).
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/ -skip_if_len_match
```
Only the length is checked here, as the overheads would be very high if the digests of files in Hadoop are calculated.

- Copy from HDFS to COS. If the `Har` directory (Hadoop archive file) exists in HDFS, the .har files can be automatically decompressed by specifying the `--decompress_har` parameter:
```
./hdfs_to_cos_cmd --decompress_har --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
If the `--decompress_har` parameter is not specified, the directory will be copied as an ordinary HDFS directory, that is, the files in the `Har` directory such as `index` and `masterindex` will be copied as-is.

### Directory information

```shell
conf: configuration file, which is used to store `core-site.xml` and `cos_info.conf`
log: log directory
src: Java source program
dep: compiled executable JAR package
```

## FAQs and Help
#### Configuration information
Please make sure that the entered configuration information is correct, including bucket, region, and API key information. The bucket name is formed by connecting the user-defined string and system-generated `APPID` with a hyphen, such as `examplebucket-1250000000`. Please also make sure that the time on the server is in sync with the local time  (if there is a difference of about 1 minute, it is okay, but if the difference is large, please set the server time correctly).

#### DataNode
Please make sure that the server where the copy program is located can also access the DataNode. The NameNode uses a public IP address and can be accessed, but the DataNode where the obtained block is located uses a private IP address and cannot be accessed directly; therefore, it is recommended that the copy program be placed in a Hadoop node for execution, so that both the NameNode and DataNode can be accessed.

#### Permissions
Please use the current account to download a file with the Hadoop command, check whether everything is correct, and then use the synchronization tool to sync the data in Hadoop.

#### File overwriting
Files that already exist in COS will be overwritten by default in case of repeated upload, unless you explicitly specify the `-skip_if_len_match` parameter, which indicates to skip files during upload if they have the same length as existing files.

#### cos path
`cos path` is considered as a directory by default, and files that are eventually copied from HDFS will be stored in this directory.


#### Copying data from Tencent Cloud EMR HDFS
To copy data from Tencent Cloud EMR HDFS to COS, you are advised to use the high-performance DistCp tool. For more information, see [Migrating Data Between HDFS and COS](https://intl.cloud.tencent.com/document/product/436/34076).
