
A security group is an instance-level firewall provided by Tencent Cloud for controlling inbound traffic of TencentDB. You can associate a security group with a cluster when purchasing it or later in the console.
TDSQL-C for MySQL allows you to configure different security groups for the read-write and read-only addresses respectively, which don't affect each other.

>?
>- A TDSQL-C for MySQL instance can be associated with up to five security groups.
>- You can configure different access addresses with different security groups, which will control only sources that access the current address.

## Prerequisites
You have created security groups for TencentDB instances in the security group console. For more information, see [Managing Security Groups](https://intl.cloud.tencent.com/document/product/1098/44594).

## Associating Read-Write Address/Read-Only Address with Security Group
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb?dbType=POSTGRESQL) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Security Group** tab and select the target address. Here:
 - Private Read-Write Address for Cluster Connection: read-write access address of the database.
 - Private Read-Only Address for Cluster Connection: read-only address of the database.
3. Click **Configure Security Group**. In the pop-up window, select the target security group and click **OK**. 
![](https://qcloudimg.tencent-cloud.cn/raw/f9997cd9cb84ca170701424b687c6044.png)

