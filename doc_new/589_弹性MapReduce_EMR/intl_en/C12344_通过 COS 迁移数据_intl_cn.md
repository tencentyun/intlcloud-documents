- Migrating non-HDFS files

    If your source file is a non-HDFS file, upload it to COS via COS Console or API, and then analyze it in the EMR cluster.

- Migrating HDFS files

    1. Get the COS migration tool

        Click [here](https://github.com/tencentyun/hdfs_to_cos_tools) to download the migration tool. For more migration tools, see [here](https://intl.cloud.tencent.com/document/product/436/6242).

    2. Configuring the tool

        All configuration files are stored in the conf directory of the tool directory. Copy the core-site.xml file of the HDFS cluster to be synced to conf, which contains the configuration information of the NameNode. Edit the configuration file cos_info.conf by including your appid, bucket, region, and key information.

    3. Command parameter descriptions

        ```
        -ak <ak>                                the cos secret id
        -appid,--appid <appid>                  the cos appid
        -bucket,--bucket <bucket_name>          the cos bucket name
        -cos_info_file,--cos_info_file <arg>    the cos user info config default is ./conf/cos_info.conf
        -cos_path,--cos_path <cos_path>         the absolute cos folder path
        -h,--help                               print help message
        -hdfs_conf_file,--hdfs_conf_file <arg>  the hdfs info config default is ./conf/core-site.xml
        -hdfs_path,--hdfs_path <hdfs_path>      the hdfs path
        -region,--region <region>               the cos region. legal value cn-south, cn-east, cn-north, sg
        -sk <sk>                                the cos secret key
        -skip_if_len_match,--skip_if_len_match  skip upload if hadoop file length match cos
        ```

    4.  Executing data migration

        ``` shell
        # All operations must be performed in the tool directory. If both configuration files and command line parameters are set, the latter will prevail
        ./hdfs_to_cos_cmd -h

        # Copy from HDFS to COS (The file will be overwritten if it already exists in COS)
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

- After the command is verified and run, a log will be outputted as shown below:

    ``` 
    [Folder Operation Result : [ 53(sum)/ 53(ok) / 0(fail)]
    [File Operation Result: [22(sum)/ 22(ok) / 0(fail) / 0(skip)]
    [Used Time: 3 s]
    ```

    As shown in the figure above, sum indicates the total number of files to be migrated; ok the number of files successfully migrated; fail the number of files failed to be migrated; skip the number of files skipped because they have the same length as the files of the same name in the destination after the skip_if_len_match parameter is added. You can also log in to the COS Console to see whether the data has been migrated correctly.

- FAQs  
    - Please ensure that the configuration information is correct, including appID, key, bucket, and region. Ensure that the server time is the same as Beijing time (one-minute difference is acceptable. If the difference is too large, please re-set your server time).  
    - Please ensure that the server for the copy program is accessible to DateNode. The NameNode uses a public IP address and can be accessed, but the DateNode where the obtained block is located uses a private IP address and cannot be accessed; therefore, it is recommended that the copy program be placed in a Hadoop node for execution, so that both the NameNode and DateNode can be accessed.    
    - In case of a permissions issue, use the current account to download a file with the Hadoop command, check whether everything is correct, and then use the synchronization tool to sync the data in Hadoop.    
    - Files that already exist in COS are overwritten by default in case of repeated upload, unless you explicitly specify the -skip_if_len_match parameter, which indicates to skip files if they have the same length as the existing files.    
    - The COS path is always considered as a directory, and files that are eventually copied from HDFS will be stored in this directory.
