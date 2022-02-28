This document describes how to configure and manage instance networks in the TencentDB for PostgreSQL console. You can add, delete, and modify instance networks based on your business needs.

## Overview
Tencent Cloud supports **classic network** and **VPC**, which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services as shown below to help you configure and manage network connectivity with ease.
- **Changing network**
 - Switch from classic network to VPC: a single TencentDB source instance can be switched from classic network to VPC.
 - Switch from VPC A to VPC B: a single primary or read-only TencentDB instance can be switched from VPC A to VPC B.
- **Customizing access IP address**
 - Custom primary instance IP: you can specify the IP address when adding a network on the instance details page of the primary instance.
 - Custom read-only instance IP: you can specify the IP address when adding a network on the instance details page of a read-only instance.
 
## Notes
- The change from classic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or classic network.
- After you change a primary instance's network, the networks of read-only instances associated with the primary instance won't be automatically switched; that is, you need to separately switch them.
- A new network added to an instance does not affect the IP address in the original network configuration.

## Directions
### Adding network
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance details page, click **Add Network** in **Basic Info** > **Network**.
![](https://qcloudimg.tencent-cloud.cn/raw/55a5f543d7e9fa529cdb4f7931d56464.png)
3. In the pop-up window, select a network. You can let the system automatically set an IP or manually specify an IP. After confirming that everything is correct, click **OK**.
>?
>- You can configure one or two networks for each instance.
>- If an instance has two networks, both are controlled by the security group associated with the instance.
>- You can only select a new VPC and subnet in the same region and AZ where the instance resides.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/a4cd02d67817ff8ddc99a62ea3c5f0cf.png"  style="zoom:80%;">
4. After the instance status changes from **Changing network** to **Running**, you can query the changed instance network on the instance details page.

### Deleting network
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance details page, click **Delete Network** in **Basic Info** > **Network**.
![](https://qcloudimg.tencent-cloud.cn/raw/adfa87be226a11db2a941327d1d94bda.png)
3. In the pop-up window, select the network to be deleted and click **OK**.
>?
>- You can configure one or two networks for each instance.
>- You must confirm that a network is no longer required before deleting it, as you will not be able to access an instance over a deleted network.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/9a6b2119f55fef8a573fffea4b3ad2d5.png"  style="zoom:100%;">
4. After the instance status changes from **Changing network** to **Running**, you can query the changed instance network on the instance details page.

### Modifying network
If you want to change the current network of the instance, for example, from the classic network to a VPC or from VPC A to VPC B, you can add and delete a network as detailed above for this need.

#### Example 1: changing from classic network to VPC
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance details page, click **Add Network** in **Basic Info** > **Network**, select the target VPC, and click **OK**.
2. After the instance status becomes **Running**, click **Delete Network** after the instance network, select the classic network, and click **Delete**. At this point, the instance network has changed from the original classic network to the new VPC.

#### Example 2: changing from VPC A to VPC B
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance details page, click **Add Network** in **Basic Info** > **Network**, select VPC B, and click **OK**.
3. After the instance status becomes **Running**, click **Delete Network** after the instance network, select VPC A, and click **Delete**. At this point, the instance network has changed from VPC A to VPC B.
>!After a network is deleted, you cannot access the instance over it. Make sure that a network is no longer needed before deleting it.
