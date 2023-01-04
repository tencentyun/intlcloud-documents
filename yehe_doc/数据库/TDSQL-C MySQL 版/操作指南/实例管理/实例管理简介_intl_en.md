
This document describes what an instance is and how to view the instance list and manipulate an instance.

## Instance overview
An instance is a database resource in Tencent Cloud. A cluster is the basic management unit of TDSQL-C for MySQL, which can contain multiple instances of two types: read-write instance and read-only instance.

The types and number of instances supported by a cluster are as described below:

| Instance Type | Maximum Instances | Supported IP |
|---------|---------|---------|
| Read-write instance | 1 | The private read-write address is enabled by default, and you can enable the public read-write address manually. |
| Read-only instance | 15 | The private read-only address is enabled by default, and you can enable the public read-only address manually. |


## Access address
TDSQL-C for MySQL supports read-write and read-only addresses. The former corresponds to the read/write service of a TDSQL-C for MySQL read-write instance, while the latter corresponds to one or multiple read-only instances on the backend for load balancing.

## Instance management overview
You can configure and manage instances in a cluster in the console, with the following configuration items:

| Instance Configuration Item | Description | Operation Method |
|---------|---------|---------|
| Instance Name | a. You can rename read-write/read-only instances in the cluster. <br>b. The instance name can contain up to 60 letters, digits, hyphens, underscores, and dots. | [Renaming Instance](https://intl.cloud.tencent.com/document/product/1098/44633) |
| Character Set | a. You can modify the character set of an instance. <br>b. The following character sets are supported: UTF-8, GBK, Latin-1, and UTF8MB4. | [Modifying Character Set](https://intl.cloud.tencent.com/document/product/1098/44630) |
| Adjust Configurations | a. You can adjust the instance configuration as needed. <br>b. You can adjust the computing specification and storage space of an instance. | [Adjusting Computing Configuration](https://www.tencentcloud.com/document/product/1098/50176)<br>[Adjusting Storage Space](https://intl.cloud.tencent.com/document/product/1098/50175) |
| Maintenance Time | a. You can set the maintenance time and window of an instance to schedule maintenance operations. <br>b. The maintenance window can be continuous or discontinuous days between Monday and Sunday.<br>c. You can set the maintenance start time and duration. | [Modifying Instance Maintenance Window](https://www.tencentcloud.com/document/product/1098/44631) |
| Restart Instance | a. You can restart an instance for routine maintenance or to clear the database buffer. <br>b. To avoid affecting normal business operations, make sure that the instance has no ongoing tasks. | [Restarting Instance](https://intl.cloud.tencent.com/document/product/1098/44629) |
| Delete Instance | You can delete an instance when it is no longer used. | [Deleting Instance](https://intl.cloud.tencent.com/document/product/1098/44628) |
| Restore Instance | a. You can restore an isolated instance as needed. <br>b. The recycle bin displays the period during which the instance can be restored. | [Restoring Instance](https://intl.cloud.tencent.com/document/product/1098/44627) |

## Viewing the instance list
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Instance List** tab to view the list of read-write and read-only instances in the cluster.
 - The instance list displays the **instance ID/name**, **monitoring data**, **AZ**, **private/public network addresses**, **expiration time**, **instance type**, **instance status**, **instance configuration**, and **operations** by default.
 - If there are many instances in the cluster, you can also enter an instance ID or name keyword in the search box on the right to quickly find the target instance.
 - Click the instance ID to enter the instance details page, where you can monitor the instance and query operation logs.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/tUTg561_8.png)
