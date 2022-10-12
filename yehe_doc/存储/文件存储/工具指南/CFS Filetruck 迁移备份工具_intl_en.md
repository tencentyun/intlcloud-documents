The traditional rsync tool does not support specifying the start/end time for data migration/backup. As a result, the migration might be performed during business peak hours, consuming the computing, network, storage, and other resources. To solve this problem, CFS introduces the Filetruck tool for users to control the start/end time of data migration tasks.

- Filetruck introduces the following features:
  - Migrating data
  - Incremental migration with automatic MD5 consistency check (you are advised to mount through sync to further ensure consistency)
  - Querying task execution status with a task ID
  - Listing all historical tasks
- Filetruck supports the following source and destination directories:
<table>
	<tr><th>Supported Item</th><th>Source</th><th>Destination</th></tr>
	<tr>
	<td>Migration address</td>
	<td><ul  style="margin: 0;">
	<li>CFS file system </li>
	<li>Local file system (file system installed after the CBS instance is formatted) </li>
	<li>COSFS local path </li>
	<li>All local paths attached to this host after the network is interconnected</li>
	</ul>
</td>
<td><ul  style="margin: 0;">
	<li>CFS file system </li>
	<li>Local file system (file system installed after the CBS instance is formatted)</li>
	<li>COSFS local path </li>
	<li>All local paths attached to this host after the network is interconnected</li>
	</ul>
</td></tr>
</table>
- Filetruck description:
Filetruck is a one-time migration tool. If a source file is modified during the migration, the source and destination files might be different (if a data segment is modified and saved after it is migrated, the modification will not be synced to the destination file. If the data segment is modified and saved before it is migrated, the modification will be synced to the destination file. Therefore, you are not advised to modify the source file during the migration/backup process).


The following describes how to use Filetruck to migrate/back up data.

## Prerequisites

Before the migration, you need to download and install Filetruck.
1. Run the following command to download the `cfs-filetruck` tool:
```
wget https://cfsturbo-client-1251013638.cos.ap-guangzhou.myqcloud.com/tools/cfs-filetruck.tar.gz
```
2. Run the following command to decompress the tool:
```
tar -xzvf cfs-filetruck.tar.gz
```
3. Run the following command to check the MD5 value:
```
cd ./cfs-filetruck/ && md5sum *
cat ./md5sum.txt
```
4. Run the following command to install `cfs-filetruck`.
```
sudo mv ./filetruck_client /usr/local/bin
sudo mv ./server_filetruck /usr/local/bin
```


## Directions
### Creating a data migration task

#### Starting a new task with simple configuration

Filetruck starts a migration task based on the configuration file in `ini` format. The configuration file of a new task needs to be **created by the user manually** and **run as the admin**. The most basic configuration file has the following content:

```
# Absolute path of the source directory
SourceDirPath=/path/to/sourceDir
# Absolute path of the destination directory
TargetDirPath=/path/to/targetDir
```

You can copy the code above to a `newTask.ini` file and modify the source/destination directories as needed. Then, you can start a new task by running the `filetruck_client -c newTask.ini` command as the root account.

If the new task is started successfully, Filetruck will return the following message that includes the `TaskId`:

```
# filetruck_client -c newTask.ini
TaskId=1
```

If the configuration is incorrect, the new task might fail to be started. In this case, Filetruck will return the corresponding error message for you to modify the configuration file:

```
# filetruck_client -c newTask.ini
Error: Directory does not exist: /path/to/sourceDir
```

#### Starting a new task with advanced configuration

In most cases, you only need to specify `SourceDirPath` and `TargetDirPath` to create a migration task. If you need to set the start/end time (`StartDate` and `EndDate`), bandwidth limit (`BandwidthLimitInKbps`), and the destination file matching rules (`IncludeRule` and `ExcludeRule`), you can use the Filetruck advanced task configuration file.

An advanced configuration file has the following content:

```
# Absolute path of the source directory (required)
SourceDirPath=/path/to/sourceDir
# Absolute path of the destination directory (required)
TargetDirPath=/path/to/targetDir
# Task start time, formatted as YYYY MMM DD hh:mm:ss (optional)
StartDate=2020 Aug 02 11:22:33
# Task end time, formatted as YYYY MMM DD hh:mm:ss (optional)
EndDate=2020 Aug 02 12:22:33
# Bandwidth limit (in KiB/s) in the range [0, 2147483647], where 0 indicates no limit (optional)
BandwidthLimitInKbps=1024
# Matching rule for files to migrate (optional)
IncludeRule=*.jpg
# Matching rule for files to skip (optional)
ExcludeRule=*.png
```

#### Parameter description

- `SourceDirPath` and `TargetDirPath` are required and should be set to the absolute paths of the directories.
- `StartDate`, `EndDate`, `BandwidthLimitInKbps`, `IncludeRule`, and `ExcludeRule` are optional and do not need to be specified in the configuration file.
- `StartDate` and `EndDate` must be in the `yyyy mmm dd HH:MM:SS` format. For example, to specify 20:20:08 on August 8, 2020, set the parameter to `2020 Aug 08 20:20:08` instead of `2020 Aug 8 20:20:8`.
- Valid range for `BandwidthLimitInKbps` is [0, 2147483647], where `0` indicates unlimited bandwidth. Note: The Filetruck migration speed is determined by the CPU/memory/bandwidth configurations of the host it is installed on, the network condition of the source/destination paths, and the size of the file to migrate/back up. In most cases, if the host configuration and egress bandwidth are high, and the file size is large, the migration/backup speed will be faster. For example, if the host is configured with 8-core CPU, 16 GB memory, and 1.5 Gbps bandwidth, and the size of the local file to migrate to the CFS high-performance file system is 4 KB, the speed would be about 40 KB/s; if the file size is 1 TB, the speed would be about 140 MB/s.
- The matching rules for `IncludeRule` and `ExcludeRule` are as follows:
  - Filetruck supports only one `IncludeRule` and one `ExcludeRule`.
  - By default, all files (including hard links) in the source directory will be migrated.
  - `IncludeRule` takes effect only when `ExcludeRule` is specified.
  - If both `IncludeRule` and `ExcludeRule` are specified, files in the source directory would be considered as a whole. Files to migrate would be those excluded by `ExcludeRule` as well as those included by both `IncludeRule` and `ExcludeRule`.
  - The common sync wildcards are `*` and `?`. `*` matches all multi-characters except `/`, and `?` matches single-characters except `/`.
  - The common matching rules are `*.jpg`, `abc*`, and `abc*def`.
  - The common matching modes are as follows:
    - Migrating all files, that is, setting `IncludeRule=` and `ExcludeRule=`
    - Skipping .png files, that is, setting `ExcludeRule=*.png`
    - Migrating only .jpg files but not .png files, that is, setting `IncludeRule=*.jpg` and `ExcludeRule=*.png`
    - Migrating .jpg files only, that is, setting `IncludeRule=*.jpg` and `ExcludeRule=sourceDir/*`


###  Querying task execution status

#### Querying all task execution status

You can run the `filetruck_client -l` command to query all historical tasks (including ongoing and completed tasks) of Filetruck as follows:

```
# filetruck_client -l
TaskId  State           FileCount       SentBytes       Speed           Progress
1       Partial Done    59              0               0B/s            3%
2       All Done        1               1073872935      511K/s          100%
3       All Done        2               1073872935      511K/s          100%
4       Partial Done    1               0               0B/s            3%
5       All Done        2               1073872935      511K/s          100%
6       All Done        2               1073872935      511K/s          100%
7       All Done        1285            138796240       502K/s          100%
8       All Done        1               0               0B/s            100%
9       All Done        0               0               0B/s            100%
10      Running         712             82799297        449K/s          24%
```


#### Parameter description
- A migration task can be in the following status:
  - `Waiting`: Waiting
  - `Running`: Running
  - `All Done`: All completed
  - `Partial Done`: Completed partially (stopped due to timeout or user cancellation)
  - `Failed`: Failed
  If the value of `FileCount`, `SentBytes`, `Speed`, or `Progress` is not calculated yet, `-` will be displayed.
- When the migration task is completed, the `inode` value of the file will be changed.
- By default, hard links in the source directory will be migrated.




#### Querying task execution status of a specific task

You can run the `filetruck_client -t TASK_ID` with `TASK_ID` specified to query the detailed information of a task:

```
# filetruck_client -t 3
TaskId:                 3
TaskState:              All Done
SourceDirPath:          /mnt/cfs0/
TargetDirPath:          /mnt/cfs1/
BeginDate:              2020 Dec 02 15:13:20
EndDate:                2020 Dec 02 15:30:25
SentFilesCount:         2
SentDataSizeInByte:     1073872935
SentSpeed:              511K/s
TaskProgress:           100%
```

If the value of `TASK_ID` is invalid, the following error message will be displayed:

```
# filetruck_client -t 999
Error: Task with ID=999 is not founded.
```

### Canceling an ongoing task

You can run the `filetruck_client -k TASK_ID` command with `TASK_ID` specified to cancel an ongoing task:

```
# filetruck_client -k 10
Success
```


<dx-alert infotype="notice" title="">
If an ongoing migration task is canceled, the destination directory of the unfinished file will be released. This is to avoid leaving incomplete files in the destination directory.
</dx-alert>


### Obtaining help information

You can run the `filetruck_client -h` command to obtain the help information of Filetruck as follows:

```
CFS-Filetruck version: 0.1.3b
Copyright (C) 2020 Tencent Inc. All rights reserved.
Link: https://cloud.tencent.com/product/cfs
 
CFS-Filetruck makes file migration easier.
 
Usage:
  Create a new task:
    filetruck_client -c /path/to/new/task/config/file.ini
 
  Get task state by task id:
    filetruck_client -t TASK_ID
 
  Cancel/Kill task by task id:
    filetruck_client -k TASK_ID
 
  List all tasks:
    filetruck_client -l
 
  Print help:
    filetruck_client -h
```
