
## Instance Overview
Cluster is the basic management unit of TDSQL-C, which can contain instances of two types: read-write instance and read-only instance.
A cluster can contain only one read-write instance and multiple read-only instances.
>! Currently, a cluster can contain up to three read-only instances.

## Access Address
TDSQL-C supports read-write and read-only addresses. The read-write address is used to provide the read/write service of a TDSQL-C primary instance (read-write instance). The read-only address corresponds to one or multiple read-only instances on the backend for load balancing.

## Viewing Instance List
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb?dbType=POSTGRESQL) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Instance List** tab to view the list of all instances in the current cluster.
 - The instance list displays the **Instance ID/Name**, **Monitoring**, **AZ**, **Expiration Time**, **Instance Type**, **Instance Status**, **Instance Configuration**, and **Operation** by default.
 - You can also enter an instance ID or name keyword in the search box on the right to quickly locate the target instance.


