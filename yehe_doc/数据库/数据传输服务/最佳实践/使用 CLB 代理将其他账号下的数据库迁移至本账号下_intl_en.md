## Overview
This document describes how to use CLB as a proxy service to establish a network connection between the source database and DTS. This is suitable for migrating/syncing IDC-based self-built databases or databases in another cloud associated with another Tencent Cloud account to the current account and running various tasks. Below is an example:

- VPCs A and B are group company networks, VPC C is a subsidiary network, and account C has no permission to manipulate resources of A and B.
- A Direct Connect line is established under account A to connect to the self-built IDC network or third-party cloud vendor network, and account B is connected to VPCs A, B, and C through CCN. Therefore, networks in the dotted box have been interconnected, and account C can access the source database.
- Use account C for migration/sync through DTS.

For this scenario, you can associate the source database with a CLB instance. Because CLB can interconnect networks across accounts, you can use the CLB instance as a DTS proxy service for routing and forwarding. Key configuration principles are as follows:
1. Use account C to create a CLB instance.
2. Configure the real server in the CLB instance and bind the source database IP to the real server.
3. Create a migration/sync task and enter the CLB address and port as the IP address and port of the source database.

## Directions
### Creating a CLB instance with account C
1. Log in to the [CLB purchase page](https://buy.intl.cloud.tencent.com/lb) with account C.
2. Configure CLB instance parameters and select the **Pay as You Go** billing mode and the **Private Network** type.
3. Return to the **Instance Management** page to view the VIP, which will be used in the subsequent DTS configuration.
   ![](https://qcloudimg.tencent-cloud.cn/raw/ba3f69595bf2f21ae8df95e88bad5fdb.png)

### Binding the source database IP to the CLB real server
> ? The CLB operations in the following steps are for reference only, subject to the descriptions in [Hybrid Cloud Deployment](https://intl.cloud.tencent.com/document/product/214/38442).

1. On the **Instance Management** page in the CLB console, click the ID of the CLB instance just purchased.
2. On the **Basic Info** page, click **Configure** for enabling the feature of binding IPs in another VPC in the **Real Server** section.
   ![](https://qcloudimg.tencent-cloud.cn/raw/70adcb0459a06a353058098f23b25a5f.png)
3. In the pop-up window, click **Submit**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c00934610178e8b32719aee58a86c4a5.png) 
4. After enabling the feature, click **Add SNAT IP** newly displayed in the **Real Server** section.
   ![](https://qcloudimg.tencent-cloud.cn/raw/84735d9ce8f922c8fd3fd9a73b21dbdb.png)
5. In the pop-up window, select a subnet, click **Add** to assign an IP, and click **Save**.
6. After the SNAT IP is configured.
7. On the instance details page, click the **Listener Management** tab and click **Create** in the **TCP/UDP/TCP SSL/QUIC Listeners** section.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7dc7b16f1020912d5c8b57cc030cad26.png)
8. Configure a TCP listener in the pop-up window. You can choose whether to enable health check and session persistence as needed.
9. After configuring the listener, select it and click **Bind** on the right to bind the source database IP address.
   ![](https://qcloudimg.tencent-cloud.cn/raw/91b459e636f74b5df223efa75459a2e8.png)
10. In the pop-up window, select **Another private IP**, enter the source database IP address and port to be bound, set the weight, and click **OK**.
      ![](https://qcloudimg.tencent-cloud.cn/raw/0b54092cef7ff8884a9c3254eb433ce3.png)
11. Return to the **Real Servers Bound** section to view the bound source database IP.

### Configuring a DTS task
The configuration steps for a DTS task with CLB as an proxy are basically the same as those for [migration from MySQL to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/42645) or [sync from MySQL/MariaDB/Percona to MySQL](https://intl.cloud.tencent.com/document/product/571/47344), with only the following difference:

After purchasing a data migration/sync task with account C, in the **Set source and target databases** step, select **VPC** as the access method (you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable this option), select the VPC and subnet of account C, and enter the VIP address of the CLB instance as the host address.

![](https://qcloudimg.tencent-cloud.cn/raw/b0a64971c3df79f56f9d851c69e3c802.png)
