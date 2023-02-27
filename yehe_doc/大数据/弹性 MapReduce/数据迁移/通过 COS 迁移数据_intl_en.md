### Migrating a non-HDFS file
If your source file is not an HDFS file, upload it to COS via the COS console or API, and then analyze it in the EMR cluster.

### Migrating an HDFS file
1. Get the COS migration tool
Get the migration tool [hdfs_to_cos_tools](https://github.com/tencentyun/hdfs_to_cos_tools). For more migration tools, see [Tool Overview](https://intl.cloud.tencent.com/document/product/436/6242).
2. Configuring the tool
All configuration files are stored in the `conf` directory of the tool directory. Copy the `core-site.xml` file of the HDFS cluster to be synced to `conf`, which contains the configuration information of the NameNode. Edit the configuration file `cos_info.conf` by including your `appid`, bucket, region, and key information.
3. Command parameter descriptions
>! 
>- We recommend you use a sub-account key and follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you need to use a permanent key, we recommend you follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission for the permanent key.

```swift
-ak <ak>                                the cos secret id // Your `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information on how to get a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
-appid,--appid <appid>                  the cos appid
-bucket,--bucket <bucket_name>          the cos bucket name
-cos_info_file,--cos_info_file <arg>    the cos user info config default is ./conf/cos_info.conf
-cos_path,--cos_path <cos_path>         the absolute cos folder path
-h,--help                               print help message
-hdfs_conf_file,--hdfs_conf_file <arg>  the hdfs info config default is ./conf/core-site.xml
-hdfs_path,--hdfs_path <hdfs_path>      the hdfs path
-region,--region <region>               the cos region. legal value cn-south, cn-east, cn-north, sg
-sk <sk>                                the cos secret key // Your `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information on how to get a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
-skip_if_len_match,--skip_if_len_match  skip upload if hadoop file length match cos
```

4. Executing data migration 
```shell
# All operations must be performed in the tool directory. If both configuration files and command line parameters are set, the latter will prevail
./hdfs_to_cos_cmd -h
# Copy from HDFS to COS (if a file already exists in COS, it will be overwritten)
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
# Copy from HDFS to COS, and if a file to be copied is of the same length as a file in COS, then it is skipped (this is suitable for repeated copy)
# Only the length is checked here, as the overheads would be very high if the digests of files in Hadoop are to be calculated
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/ -skip_if_len_match
# Set parameters completely through the command line
./hdfs_to_cos_cmd -appid 1252xxxxxx -ak
      AKIDVt55xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -sk
      KS08jDVbVElxxxxxxxxxxxxxxxxxxxxxxxxxx -bucket test -cos_path /hdfs
      -hdfs_path /data/data -region cn-south -hdfs_conf_file
/home/hadoop/hadoop-2.8.1/etc/hadoop/core-site.xml
```
5. After the command is verified and run, a log will be output as shown below:
```swift
[Folder Operation Result : [ 53(sum)/ 53(ok) / 0(fail)]]
[File Operation Result: [22(sum)/ 22(ok) / 0(fail) / 0(skip)]]
[Used Time: 3 s]
```
 - `sum` indicates the total number of files to be migrated.
 - `ok` indicates the number of files successfully migrated.
 - `fail` indicates the number of files failed to be migrated.
 - `skip` indicates the number of files skipped because they have the same length as the files of the same name in the destination after the `skip_if_len_match` parameter is added.

You can also log in to the COS console to see whether the data has been migrated correctly.

### FAQs  
- Make sure that the configuration information is correct, including `appID`, key, bucket, and region. Make sure that the server time is the same as Beijing time (1-minute difference is acceptable. If the difference is too large, reset your server time).  
- Make sure that the server for the copy program is accessible to DateNode. The NameNode uses a public IP address and can be accessed, but the DateNode where the obtained block is located uses a private IP address and cannot be accessed; therefore, we recommend you place the copy program in a Hadoop node for execution, so that both the NameNode and DateNode can be accessed.
- In case of a permissions issue, use the current account to download a file with the Hadoop command, check whether everything is correct, and then use the synchronization tool to sync the data in Hadoop.    
- Files that already exist in COS are overwritten by default in case of repeated upload, unless you explicitly specify the `-skip_if_len_match` parameter, which indicates to skip files if they have the same length as the existing files.    
- The COS path is always considered as a directory, and files that are eventually copied from HDFS will be stored in this directory.
