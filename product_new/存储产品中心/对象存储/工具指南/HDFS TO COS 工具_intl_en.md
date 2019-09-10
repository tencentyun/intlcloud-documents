## Description
HDFS TO COS is used to copy the data from HDFS to Tencent Cloud COS.

## Operating Environment
### System Environment
Linux/Windows system

### Software Requirements
JDK 1.7/1.8 

#### Installation and configuration
For more information on the installation and configuration of environment, see [Installing and Configuring Java](https://cloud.tencent.com/document/product/436/10865).

## Configuration and Usage
### Configuration
1. Install Hadoop-2.7.2 or above by following the steps described in [Installing and Testing Hadoop](https://cloud.tencent.com/document/product/436/10867).
2. Download HDFS TO COS at [GitHub](https://github.com/tencentyun/hdfs_to_cos_tools) and decompress it.
3. Copy the core-site.xml of the HDFS cluster to be synchronized to the conf folder. Core-site.xml contains the configuration information of NameNode.
4. Edit the configuration file `cos_info.conf`, Bucket, Region, and API Keys. The name of Bucket is a hyphen-separated combination of a user-defined string and a system-generated APPID, e.g. "examplebucket-1250000000".
5. Specify the location for the configuration file in the command line parameter. By default, it is located at `conf/cos_info.conf`.
>If the command line parameter conflicts with the configuration file, the command line parameter prevails.

### Usage

The example below shows how to use it on a Linux system.

#### View Help
```
./hdfs_to_cos_cmd -h
```
The execution result is as follows:
![微信图片_20170807163035](//mc.qcloudimg.com/static/img/dcff34d37928c0d8b9c4b45c25ac116e/image.png)

#### Copy files
- When a file is copied from HDFS to COS, if a file with the same name already exists on the COS, the existing file will be overwritten by the new one.
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
- When a file is copied from HDFS to COS, if a file with the same name and length already exists on the COS, the upload is skipped (only applicable to the scenario where the file has been copied once and is copied again).
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/ -skip_if_len_match
```
Only match the file length during this process. The computing of file summary on Hadoop would involve a high cost.

- When a file is copied from HDFS to COS, if there is a Har directory on HDFS (Hadoop Archive), the Har file can be decompressed automatically if you specify the --decompress_har parameter:
```
./hdfs_to_cos_cmd --decompress_har --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
If the `--decompress_har` parameter is not specified, the files including `index` and `masterindex` under the `.har` directory are copied as they are (take the directory as a common directory on HDFS).

#### Directory information
```shell
conf : The configuration file used to store core-site.xml and cos_info.conf.
log  : Log directory
src  : Java source program
dep  :Runnable JAR package generated after compilation
```
## Q&A
#### About configuration information
Be sure to enter the correct configuration information, including Bucket, Region and API Keys. The name of Bucket is a hyphen-separated combination of a user-defined string and a system-generated APPID, e.g. "examplebucket-1250000000". Make sure the time difference between the server time and Beijing time does not exceed 1 minute. Otherwise, reset the server time.

#### About DataNode
Make sure DataNode can be connected to the server where the copy program resides. NameNode can be connected via a public IP, but the DataNode server where the obtained block resides only has a private IP, which makes the direct connection impossible. Therefore, it is recommended to execute the synchronization program at a Hadoop node to ensure both NameNode and DataNode are accessible.

#### Permissions
Use the Hadoop command to download and check files, and then use synchronization tool to synchronize data on Hadoop.

#### File overwriting
For the files that already exist on the COS, the files are copied again and overwrite the original ones by default. If you specify `-skip_if_len_match`, the upload is skipped when the file to be copied to COS has the same name and length as the existing one on COS.

#### cos path
 The **cos path** is a directory by default, and all the files copied from HDFS are stored in the directory.
