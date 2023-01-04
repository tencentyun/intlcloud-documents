This document describes what a TDSQL-C for MySQL cluster is and how to view the cluster list and manipulate a cluster.

## Cluster overview
A cluster is a group of network resources containing read-write and read-only instances. As the basic management unit of TDSQL-C for MySQL, a cluster can have up to one read-write instance and 15 read-only instances.

## Cluster management overview
| Cluster Configuration Item | Description | Operation Method |
|---------|---------|---------|
| Renaming a cluster | <li>You can rename a cluster. <li>The cluster name can contain up to 60 letters, hyphens, underscores, and dots. | [Renaming Cluster](https://intl.cloud.tencent.com/document/product/1098/44621) |
| Modifying the cluster project | You can set and modify the project of a cluster. | [Modifying Cluster Project](https://intl.cloud.tencent.com/document/product/1098/44620) |
| Deleting a cluster | You can delete a cluster when it is no longer used. | [Deleting Cluster](https://intl.cloud.tencent.com/document/product/1098/44619) |
| Restoring a cluster | <li>You can restore an isolated cluster as needed. <li>The recycle bin displays the period during which the cluster can be restored. </li> | [Restoring Cluster](https://www.tencentcloud.com/document/product/1098/51182) |

## Viewing the cluster list
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region and MySQL engine at the top to view the cluster list.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5uM8196_11.png)
