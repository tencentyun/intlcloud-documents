You can view the instance details in the TencentDB for MongoDB console to quickly check the instance running status, capacity utilization, and primary/secondary nodes in the cluster from a global perspective and prevent risks promptly.

## Background
During daily OPS, you can quickly view the instance information list to stay up to date with the instance running status and resource usage in order to prevent risks promptly. When an exception occurs, you can further use the instance details such as instance network status, node running status, and latency to quickly locate and troubleshoot the problem step by step.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support instance list display.

## Prerequisites
You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).

## Directions
### Quickly viewing instance list
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance and view its information such as running status, configuration specification, and storage engine.
![](https://qcloudimg.tencent-cloud.cn/raw/0ad37c4c3ebad3a061711bd0ff89579f.png)

### Viewing instance details
Click the ID of the target instance to view its details.
- In the **Basic Info** section, you can view the instance region and network.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5f8d39a58c4db0a2ba6ddc6879d6c9fa.png" style="zoom:67%;" />
- In the **Configuration** section, you can view the instance version, storage engine, node specification, capacity, billing mode, and maintenance time.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cdd603de45d6bbdfbd46ad960e8f7084.png" style="zoom:67%;" />
- In the **Instance Architecture Diagram** section, you can view the system architecture diagram of the cluster to recognize the primary/secondary nodes in the cluster.

## More Operations
### Creating instance
You can click **Create Instance** above the instance list to create an instance. For more information on how to configure the parameters, see [Creating TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/3551) in Getting Started.

### Renaming instance
1. In the [instance list](https://console.cloud.tencent.com/mongodb), hover over the instance name to be modified and click <img src="https://qcloudimg.tencent-cloud.cn/raw/c3386f46a3b0588a84b3c0bf6f952200.png" style="zoom:66%;" /> on the right.
2. In the instance name input box, enter a new name, which must meet the following requirements:
   - It can contain 1–60 characters.
   - It can contain letters, digits, underscores, and hyphens.
   - A letter, digit, or special symbol is counted as one character.

### Setting fields in instance list
1. Click <img src="https://qcloudimg.tencent-cloud.cn/raw/770577c6c61c1f3066210d6345e09b6f.png" style="zoom:67%;" /> in the top-right corner of the instance list.
2. On the **Display Settings** page, select the fields to be displayed.
3. Click **OK**, and you can see the set fields in the instance list.

### Exporting instance list
You can click <img src="https://qcloudimg.tencent-cloud.cn/raw/99ee5bb1067d04d1661ef02be39e2caf.png" style="zoom:50%;" /> in the top-right corner of the instance list to export the entire list.

## API
You can use an API to get the TencentDB instance list. For more information, see [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/240/34702).

| API | Description |
| ------------------------------------------------------------ | -------------------- |
| [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/240/34702) | Queries TencentDB instance list |
| [RenameInstance](https://intl.cloud.tencent.com/document/product/240/34697) | Renames instance         |


