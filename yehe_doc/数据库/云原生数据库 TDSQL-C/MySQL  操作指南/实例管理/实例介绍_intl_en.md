
## Instance Overview
Cluster is the basic management unit of TDSQL-C, which can contain instances of two types: read-write instance and read-only instance.
A cluster can contain only one read-write instance and multiple read-only instances.
>! Currently, a cluster can contain up to 15 read-only instances.

## Access Address
TDSQL-C supports read-write and read-only addresses. The read-write address is used to provide the read/write service of a TDSQL-C primary instance (read-write instance). The read-only address corresponds to one or multiple read-only instances on the backend for load balancing.

## Viewing Instance List
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Instance List** tab to view the list of all instances in the current cluster.
 - The instance list displays the **Instance ID/Name**, **Monitoring**, **AZ**, **Private/Public Network Address**, **Expiration Time**, **Instance Type**, and **Instance Status** by default.
 - You can also enter an instance ID or name keyword in the search box on the right to quickly locate the target instance.

![](https://qcloudimg.tencent-cloud.cn/raw/3b751ab14906c0cc52e72db106ca4ba8.png)

