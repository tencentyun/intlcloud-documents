## Overview

After migrating data from HDFS to COS by using the `hadoop distcp` command, you can use the Hadoop-cos-DistChecker tool to verify the integrity of the migrated directory. Based on the parallel processing capabilities of MapReduce, it can quickly check the **source directory** against the **destination directory**.

## Operating Environment

- Hadoop-cos above v5.8.2 (for details, see [hadoop-cos release](https://github.com/tencentyun/hadoop-cos/releases).)
- Hadoop MapReduce runtime environment

> !
> - If you are using a self-built Hadoop cluster, the Hadoop-cos dependency should be of the latest version (with GitHub release as 5.8.2 or above) to obtain the CRC64 checksum.
> - If you are using Tencent Cloud EMR, only clusters created after May 8, 2020 contain the Hadoop-cos version above. To deal with earlier clusters, please [contact us](https://intl.cloud.tencent.com/contact-sales).

## Directions

Since Hadoop-cos-distchecker needs to get CRC64 checksum for files from Hadoop-cos (CosN file system) before running, you should first configure `fs.cosn.crc64.checksum.enabled` to `true` to do so. Once this tool finishes, configure the value back to `false` to stop getting CRC64 checksum.

> !The CRC64 checksum in Hadoop-COS is not compatible with the CRC32C checksum in HDFS. Therefore, after using this tool, be sure to set the above parameter to `false`. Otherwise, Hadoop-COS may fail to run in some scenarios where the file system `getFileChecksum` API is called.

### Parameter description

- **Source file list**: a list of subdirectories and files obtained by running the following command:
```plaintext
hadoop fs -ls -R hdfs://host:port/{source_dir} | awk '{print $8}' > check_list.txt
```
 Its format is as follows:
```plaintext
/benchmarks/TestDFSIO
/benchmarks/TestDFSIO/io_control
/benchmarks/TestDFSIO/io_control/in_file_test_io_0
/benchmarks/TestDFSIO/io_control/in_file_test_io_1
/benchmarks/TestDFSIO/io_data
/benchmarks/TestDFSIO/io_data/test_io_0
/benchmarks/TestDFSIO/io_data/test_io_1
/benchmarks/TestDFSIO/io_write
/benchmarks/TestDFSIO/io_write/_SUCCESS
/benchmarks/TestDFSIO/io_write/part-00000
```
- **Source directory**: the directory where the source files are stored; it usually serves as the source path for data migration through the `distcp` command. For example, `hdfs://host:port/source_dir` is the source directory in the following sample:
```plaintext
hadoop distcp hdfs://host:port/source_dir cosn://examplebucket-appid/dest_dir
```
 This is also the common parent directory in the **source file path list**, such as `/ benchmarks` in the sample above.
- **Destination directory**: the destination directory to check against.

### Command line syntax

Hadoop-cos-DistChecker is a MapReduce job-based program, and can be submitted just like a MapReduce job:

```plaintext
hadoop jar hadoop-cos-distchecker-2.8.5-1.0-SNAPSHOT.jar com.qcloud.cos.hadoop.distchecker.App <Absolute path of the source file list> <Absolute path representation of the source directory> <Absolute path representation of the destination directory> [optional parameters]
```

> ? The “optional parameters” are for Hadoop.

### Directions

The example below describes how to use this tool by checking `hdfs://10.0.0.3:9000/benchmarks` against `cosn://hdfs-test-1250000000/benchmarks`.

First, run the following command:

```plaintext
hadoop fs -ls -R hdfs://10.0.0.3:9000/benchmarks | awk '{print $8}' > check_list.txt
```

![](https://main.qcloudimg.com/raw/a2a853be2646b6558983303de805c04e.png)
Export all the source paths to be checked to a `check_list.txt` file which stores the list of source file paths, as shown below:
![](https://main.qcloudimg.com/raw/216d90b20d383e233e50f497e83c24c3.png)

Then, run the following command to put `check_list.txt` to the HDFS:

```plaintext
hadoop fs -put check_list.txt hdfs://10.0.0.3:9000/
```

![](https://main.qcloudimg.com/raw/e5b79519dfeac808b64f29e04c35e9a4.png)

Run the Hadoop-cos-DistChecker to check `hdfs://10.0.0.3:9000/benchmarks` against `cosn://hdfs-test-1250000000/benchmarks`, and output the result to the `cosn://hdfs-test-1250000000/check_result` path by using the following command:

```shell
hadoop jar hadoop-cos-distchecker-2.8.5-1.0-SNAPSHOT.jar com.qcloud.cos.hadoop.distchecker.App hdfs://10.0.0.3:9000/check_list.txt hdfs://10.0.0.3:9000/benchmarks cosn://hdfs-test-1250000000/benchmarks cosn://hdfs-test-1250000000/check_result
```

![](https://main.qcloudimg.com/raw/8356bebae88dae96aaecf03ea202df0d.png)

Hadoop-cos-DistChecker will read the source file list and source directory, and run the MapReduce job to perform a distributed check. The final check result will be output to `cosn://examplebucket-appid/check_result`.

![](https://main.qcloudimg.com/raw/b49000f8613e41a659df31c19bdab2fa.png)

The check report is as follows:

```plaintext
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO       hdfs://10.0.0.3:9000/benchmarks/TestDFSIO,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control    hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_0  hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_0,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control/in_file_test_io_0,CRC64,1566310986176587838,1566310986176587838,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_1  hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_1,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control/in_file_test_io_1,CRC64,-6584441696534676125,-6584441696534676125,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data       hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_0     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_0,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data/test_io_0,CRC64,3534425600523290380,3534425600523290380,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_1     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_1,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data/test_io_1,CRC64,3534425600523290380,3534425600523290380,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write      hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/_SUCCESS     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/_SUCCESS,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write/_SUCCESS,CRC64,0,0,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/part-00000   hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/part-00000,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write/part-00000,CRC64,-4804567387993776854,-4804567387993776854,SUCCESS,'The source file and the target file are the same.'
```



## Check Report Format

The check report is in the following format:

```plaintext
Source file path in `check_list.txt`, absolute path of the source file, absolute path of the destination file, checksum algorithm, checksum of the source file, checksum of the destination file, check result, result description
```

There are 7 check results:

- SUCCESS: The source and destination files exist and are the same.
- MISMATCH: The source and destination files exist but are different.
- UNCONFIRM: The system cannot determine whether the source and destination files are the same. This may be because the destination file already existed in COS before the CRC64 feature was launched, and thus its CRC64 checksum cannot be obtained.
- UNCHECKED: The check is not performed. This is mainly because the source file cannot be read, or its checksum cannot be obtained.
- SOURCE_FILE_MISSING: The source file does not exist.
- TARGET_FILE_MISSING: The destination file does not exist.
- TARGET_FILESYSTEM_ERROR: The destination file system is not CosN.


## FAQs

#### Why is there a negative CRC64 checksum in the check report?

A CRC64 checksum may contain 20 digits, which exceeds the range of the Java `long` type. However, they have the same underlying bytes. Therefore, when the `long` value is printed, it may be negative.

