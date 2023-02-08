A security group is a firewall provided by Tencent Cloud for controlling inbound traffic of TencentDB. You can associate a security group with a cluster when purchasing it or later in the console.

This document describes how to configure a security group for TDSQL-C for MySQL in the console.
>!
>- Currently, security groups can be configured only for TDSQL-C for MySQL instances in VPCs.
>- TDSQL-C for MySQL allows you to configure separate security groups for the read-write and read-only addresses, which don't affect each other.

## Configuring a Security Group
### During cluster purchase
1. Log in to the [purchase page](https://buy.cloud.tencent.com/cynosdb?regionId=8#/).
2. Configure the database and basic information, configure the security group in **Advanced Configuration**, and click **Buy Now**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/kjDU265_14.png)

### In the console
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Security Group** tab, select the target read-write instance or read-only instance, and click **Configure Security Group**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yh7N015_15.png)
4. In the **Configure Security Group** window, select a security group rule (or search for the target security group by ID) and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CtjH139_16.png)
>?
>- You can configure up to five security group rules.
>- You can configure different access addresses with different security groups, which will control only sources that access the current address.

## Adjusting the Priority of a Security Group
If multiple security groups are bound to a TDSQL-C for MySQL instance, they will be executed based on their priorities such as 1 and 2. You can adjust the priorities as follows.

1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Security Group** tab, select the target read-write instance, database proxy, or read-only instance, and click **Edit** below the bound security group.
4. In the **Security Group** column, adjust the priority of the security group by using the ![](https://qcloudimg.tencent-cloud.cn/raw/0796ce4fc98c14bfcb924b1da3083149.png) icons and click **Save**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9F25795_18.png)

