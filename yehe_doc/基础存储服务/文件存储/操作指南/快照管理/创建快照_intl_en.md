## Overview

You can create snapshots for a file system to save its data at specific points of time. The file system snapshot feature adopts the incremental mode to create snapshots, and it creates a snapshot that records only the data changes compared with the last snapshot. This process is quick if the data changes a little. Although snapshots are created in incremental mode, if there are snapshots available, you can always use an undeleted snapshot to restore the data at the time when the snapshot is created.

You can create a snapshot for a file system in the normal state, but the snapshot can only capture the written data rather than data being written by an app or process. Therefore, according to your business needs, you can choose to temporarily stop all data writes and create a snapshot after data synchronization to obtain a complete snapshot. 

## Prerequisites
- You have activated CFS.
>! Currently, only Standard file systems support the snapshot feature.
>
- You have not reached the upper limits for the number and total size of snapshots in the current region. See [Use Limits](https://intl.cloud.tencent.com/document/product/582/44913).

## Notes

For better system performance, data is stored in the memory buffer before it is written to the file system at the proper moment. A snapshot can only capture the written data but not cached data in the memory (such as files in the `/run` directory in a Linux system) of a file system. Therefore, the snapshot created for the file system does not contain data that is stored in the memory buffer and has not been written to the file system. As a result, data inconsistency occurs. We strongly recommend that you ensure that all data in the memory is written to the file system and suspend read and write operations of the file system before creating a snapshot. The recommended method for writing data in the memory to the file system is as follows:
- To resolve this issue, run the `sync` command to forcibly write the data in the memory buffer immediately to the file system, and then prevent new data from being written to the file system. If no error message is returned after the command is executed, the data in the memory buffer has been successfully written to the file system, as shown below:
![](https://main.qcloudimg.com/raw/e1b0ac245e325281a0693f7ae43946ff.png)



## Directions[](id:CreateSnapshot)

1. Log in to the [CFS console](https://console.cloud.tencent.com/cfs).
2. Click **Create Snapshot** in the row of the target file system.
3. In the pop-up, enter the snapshot name and click **Confirm**.
	

