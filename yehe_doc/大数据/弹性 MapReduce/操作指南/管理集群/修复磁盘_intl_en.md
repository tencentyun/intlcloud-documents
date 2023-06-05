## Overview
Local disk replacement events are automatically monitored in the EMR console. After disk replacement, you can initialize the new disk in the console on your own.
>! 
>- After you receive a faulty disk notification from the CVM and repair or replace the physical disk as instructed in the notification, the disk repair operation is triggered in the EMR console.
>- When a disk is replaced, all data on the disk is lost. Make sure that the data on the disk is backed up prior to replacement.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the corresponding cluster in the cluster list.
2. On the cluster details page, choose **Cluster Resource** > **Resource Management** and then repair the disk on the node where the disk is replaced.
3. In the disk repair process, the services on the current node will be restarted, during which both the services and node are unavailable. Therefore, we recommend you repair a disk during off-peak business hours.

## Kudu Service Recovery
>! 
>- If there are multiple local disks and one or more of them use the EMR disk repair feature, the node where the disks are located will run the KuduServer service.
>- Due to the limitation of Kudu's `fs_data_dirs` feature, to ensure normal startup of KuduServer after one or more disks are formatted, all data directories on the KuduServer node are empty. You should confirm that these directories are not used by any businesses other than Kudu.

- Scenario:
Under **Cluster Service** in the EMR console, you can view the health status of the KuduServer on the node where the disk is replaced. The health status is unavailable:
- Data consistency check and recovery:
	1. Ensure that the directory (as described below) is used exclusively for Kudu. If the directory is used for any other purpose, move the relevant data to another directory that is not configured as an `fs_data_dirs` directory before proceeding with the following steps.
	Specific directory: View the `/usr/local/service/kudu/conf/tserver.gflags` file:
	![](https://qcloudimg.tencent-cloud.cn/raw/daf635f30f14fd6c213b562ecdc4c464.png)
	2. Log in to the abnormal node of the local disk to view logs: `/data/emr/kudu/log/kudu-tserver.INFO`:
	![](https://qcloudimg.tencent-cloud.cn/raw/059c22c9e94094405a601b6616e1d94a.png)
	Run the following commands as a root user to remove inconsistent data: 
```
rm -rf /data/emr/kudu/tserver/*
rm -rf /data1/emr/kudu/tserver/*
```
The commands assume that `/data/emr/kudu/tserver/` and ` /data1/emr/kudu/tserver/` are configured in `fs_data_dirs`. Fore more information, view `/usr/local/service/kudu/conf/tserver.gflags`.
	3. Observe the service status of KuduServer in the console.

>? If you encounter any issues, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
