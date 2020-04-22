
## Feature Description



After migrating data from HDFS to COS by using the `hadoop distcp` command, you can use the Hadoop-cos-DistChecker tool to verify the integrity of the migrated directory. Based on concurrence capabilities of MapReduce, you can quickly verify and compare the source and target directories.



## Prerequisites

- [hadoop-cos-2.x.x-shaded.jar](https://github.com/tencentyun/hadoop-cos/tree/master/dep)
- Runtime environment of Hadoop MapReduce

>Here, the `hadoop-cos` dependency must be of the latest version (with GitHub tag above 5.8.2) to get the CRC64 checksum.

## Instructions

### Parameter description

#### **Source file path list**

The source file list is a list of subdirectories and files to be checked that you export by running `hadoop fs -ls -R hdfs://host:port/{source_dir} | awk '{print $8}' > check_list.txt`. Its format is as shown in the following sample:

```txt
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

#### **Source directory**

This is the directory where the source files are stored and is usually the source path for data migration through the `distcp` command. For example, in `hadoop distcp hdfs://host:port/source_dir cosn://bucket-appid/dest_dir`, `hdfs://host:port/source_dir` is the source directory.

This is also the common parent directory in the list of source file paths. For example, it is `/benchmarks` in the sample above.

#### **Target directory**

This is the target directory to be compared.

### Command line format

Hadoop-cos-DistChecker is a MapReduce job program and can be committed just like a MapReduce job:

```shell
hadoop jar hadoop-cos-distchecker-2.8.5-1.0-SNAPSHOT.jar com.qcloud.cos.hadoop.distchecker.App <absolute path of the source file list> <absolute path of the source directory> <absolute path of the target directory> [optional Hadoop parameters]
```

### Directions

The following uses checking `hdfs://10.0.0.3:9000/benchmarks` and `cosn://hdfs-test-1250000000/benchmarks` as an example to describe how to use the tool.

First, run `hadoop fs -ls -R hdfs://10.0.0.3:9000/benchmarks | awk '{print $8}' > check_list.txt` to export the source paths to be checked to the `check_list.txt` file, which stores the list of source file paths.



![](https://main.qcloudimg.com/raw/a2a853be2646b6558983303de805c04e.png)

![](https://main.qcloudimg.com/raw/216d90b20d383e233e50f497e83c24c3.png)

Then, save `check_list.txt` to HDFS: `hadoop fs -put check_list.txt hdfs://10.0.0.3:9000/`.

![](https://main.qcloudimg.com/raw/e5b79519dfeac808b64f29e04c35e9a4.png)


Run Hadoop-cos-DistChecker to compare `hdfs://10.0.0.3:9000/benchmarks` with `cosn://hdfs-test-1250000000/benchmarks` and output the result to the `cosn://hdfs-test-1250000000/check_result` path by running the following command:



```shell
hadoop jar hadoop-cos-distchecker-2.8.5-1.0-SNAPSHOT.jar com.qcloud.cos.hadoop.distchecker.App hdfs://10.0.0.3:9000/check_list.txt hdfs://10.0.0.3:9000/benchmarks cosn://hdfs-test-1250000000/benchmarks cosn://hdfs-test-1250000000/check_result
```


![](https://main.qcloudimg.com/raw/8356bebae88dae96aaecf03ea202df0d.png)


Hadoop-cos-DistChecker will read the source file list and source directory and run the MapReduce job to perform a distributed check. The check result will be output to `cosn://bucket-appid/check_result`.




![](https://main.qcloudimg.com/raw/b49000f8613e41a659df31c19bdab2fa.png)

The check report is as follows:

```text
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_0	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_0,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control/in_file_test_io_0,MD5,dee27f089393936ef42dbd3ebd85750b,dee27f089393936ef42dbd3ebd85750b,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_1	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_1,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control/in_file_test_io_1,MD5,526560d99bd99476e5a8e68f0ce87326,526560d99bd99476e5a8e68f0ce87326,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_0	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_0,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data/test_io_0,CRC64,-1057373059199797567,-1057373059199797567,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_1	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_1,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data/test_io_1,CRC64,-1057373059199797567,-1057373059199797567,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/_SUCCESS	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/_SUCCESS,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write/_SUCCESS,MD5,d41d8cd98f00b204e9800998ecf8427e,d41d8cd98f00b204e9800998ecf8427e,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/part-00000	hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/part-00000,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write/part-00000,MD5,5f91c70529f8c9974bf7730c024c867f,5f91c70529f8c9974bf7730c024c867f,SUCCESS,'The source file and the target file are the same.'
```



## Check Report Format

The check report is in the following format:

```TEXT
Source file path in `check_list.txt` absolute path of the source file,absolute path of the target file,checksum algorithm,checksum of the source file,checksum of the target file,check result,result description

```

There are seven check results:

- SUCCESS: the source and target files exist and are the same.
- MISMATCH: the source and target files exist but are different.
- UNCONFIRM: the system cannot determine whether the source and target files are the same. This may be because that the file already exists in COS before the CRC64 feature is launched and thus its CRC64 checksum cannot be obtained.
- UNCHECKED: the check is not performed. This is mainly because that the source file or the checksum of the source file cannot be read.
- SOURCE_FILE_MISSING: the source file does not exist.
- TARGET_FILE_MISSING: the target file does not exist.
- TARGET_FILESYSTEM_ERROR: the target file system is not CosN.



## FAQs


#### 1. Why is there a negative CRC64 checksum in the check report?

A CRC64 checksum may contain 20 digits and thus exceeds the range of the Java long type. However, they have the same underlying bytes. When the long value is printed, it will be negative.

#### 2. Why are both MD5 checksum and CRC64 checksum being used?

Currently, MD5 checksum is used for simple uploads to COS, while CRC64 checksum is used only for multipart uploads. Therefore, there are different types of checksums for check of different file types.
