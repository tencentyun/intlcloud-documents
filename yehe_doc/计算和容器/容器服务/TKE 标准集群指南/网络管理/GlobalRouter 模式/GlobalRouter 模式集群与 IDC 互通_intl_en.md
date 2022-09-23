## Overview

Currently, a container cluster can communicate with your IDC mainly through two methods: **Direct Connect** and **IPsec VPN**.
>! 
>- The directions in this document are based on an existing cluster with nodes. For how to create a cluster, see [Quickly Creating a Standard Cluster](https://intl.cloud.tencent.com/document/product/457/40029).
> - Make sure that the VPC where TKE resides is successfully connected to your IDC through Direct Connect or VPN Connections. If no tunnel is established, you can establish one as instructed in [Features](https://intl.cloud.tencent.com/document/product/1037/32709).

## Directions

### Communication over Direct Connect

1. Apply for a connection as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).
2. Apply for a tunnel as instructed in [Creating a Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/19250).
3. Create a Direct Connect gateway as instructed in [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).
4. Verify that the container node can communicate with the IDC.
>! When performing this step, please make sure that the container node can communicate with the IDC and the verification is successful.
6. Prepare information such as the region, `appID`, cluster ID, `vpcID`, and Direct Connect gateway ID and [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to open up the container network.
7. Select the mode of operation based on the type of protocol used by the IDC.
 - If the IDC uses the BGP protocol, the container IP address range route will be automatically synchronized.
 - If other protocols are used, you need to configure the next hop of the container IP address range in the IDC to be routed to the Direct Connect gateway.
8. Verify that the container can communicate with the IDC.

### Communication over VPN

#### Configuring an SPD Policy

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
2. On the left sidebar, click **VPN Connections** > **[VPN Tunnel](https://console.cloud.tencent.com/vpc/vpnConn)** to enter the VPN tunnel management page.
3. [](id:step3)Click the ID/name of the local VPN tunnel for which to configure the SPD policy.
4. On the VPN tunnel details page, click **Edit** in the **SPD Policy** column to add the container IP address range.
5. [](id:step5)Click **Save**.
6. Repeat [step 3](#step3) to [step 5](#step5) to configure the SPD policy for the opposite VPN tunnel.

#### Adding a Container IP Address Range

>! One subnet can be bound to only one routing table. If multiple routing tables are associated, they will be replaced with the last bound one.
>
1. On the left sidebar, click **[Route Table](https://console.cloud.tencent.com/vpc/route)** to enter the route table management page.
2. [](id:addCIDRStep2)Find the route table configured when you [set intra-region cross-cluster interconnection](https://intl.cloud.tencent.com/document/product/457/44483) or [set cross-region cross-cluster interconnection](https://intl.cloud.tencent.com/document/product/457/44483). Click the ID/name of the route table to enter the route table details page.
3. Click **+ New routing policies** to add the container IP range.
4. [](id:addCIDRStep4)Select the **Associated Subnets** tab and click **Create Associated Subnet** to associate with the subnet where the CVM instance is.
5. Repeat [step 2](#addCIDRStep2) to [step 4](#addCIDRStep4) to add the IP address range where the Tencent Cloud container is located to the opposite routing device.

#### Expected Result

Containers can communicate with the peer CVM instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b89ee1a882fdace4ff5037f09984b1c3.png)
Containers can communicate with VPN opposite servers.

>? If you want your cloud containers to communicate with your IDC over an IPsec VPN, you need to set the **SPD policy** and **routing table**.





