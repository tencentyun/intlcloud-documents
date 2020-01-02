## Operation Scenario

Currently, a container cluster can communicate with your IDC mainly through two methods: **Direct Connect** and **IPsec VPN**.
>- This document uses a cluster that has been created and a node that has been added as an example. For more information about how to create a cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/11741).
> - Please make sure that the VPC where your TKE service is located has been successfully connected with your IDC via a Direct Connect line or VPN. 

## Directions

### Communication over Direct Connect

1. Apply for a physical Direct Connect line as instructed in [Applying for a Physical Direct Connect Line](<https://intl.cloud.tencent.com/document/product/216/19244>).
2. Apply for a tunnel as instructed in [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250).
3. Create a Direct Connect gateway as instructed in [Creating a Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).
4. Verify that the container node can communicate with the IDC.
> When performing this step, please make sure that the container node can communicate with the IDC and the verification is successful.
6. Prepare information such as the region, appID, cluster ID, vpcID, and Direct Connect gateway ID and [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to open up the container network.
7. Select the mode of operation based on the type of protocol used by the IDC.
 - If the IDC uses the BGP protocol, the container IP address range route will be automatically synchronized.
 - If other protocols are used, you need to configure the next hop of the container IP address range in the IDC to be routed to the Direct Connect gateway.
8. Verify that the container can communicate with the IDC.

### Communication over VPN

#### Configuring an SPD Policy

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
2. In the left sidebar, click **VPN** > **[VPN tunnel](https://console.cloud.tencent.com/vpc/vpnConn)** to go to the VPN tunnel management page.
3. <span id="step3">Click the ID/name of the local VPN tunnel for which the SPD policy needs to be configured. See the figure below: </span>
![](https://main.qcloudimg.com/raw/8f377cd3e88e06f86c18470e0b98ec10.png)
4. On the VPN tunnel details page, click **Edit** in the "SPD policy" column to add the container IP address range. See the figure below:
![Configure an SPD policy](https://main.qcloudimg.com/raw/16a126780ad8d9f73158c46098cd1e82.png)
5. <span id="step5">Click **Save**. </span>
6. Repeat [step 3](#step3) to [step 5](#step5) to configure the SPD policy for the opposite VPN tunnel.

#### Adding a Container IP Address Range

>One subnet can be bound to only one routing table. If multiple routing tables are associated, they will be replaced with the last bound one.

1. In the left sidebar, click **[Routing Table](https://console.cloud.tencent.com/vpc/route)** to go to the routing table management page.
2. <span id="addCIDRStep2">Find the routing table configured when [setting intra-region cross-cluster communication](https://intl.cloud.tencent.com/document/product/457/30645) or [setting cross-region cross-cluster communication](https://intl.cloud.tencent.com/document/product/457/30646). Click the ID/name of the routing table to go to the routing table details page. </span>
3. Click **+ Create a routing policy** to append the container IP address range.
4. <span id="addCIDRStep4">Select the **Associate a subnet** tab and click **Create an associated subnet** to associate the subnet where the server is located. </span>
5. Repeat [step 2](#addCIDRStep2) to [step 4](#addCIDRStep4) to add the IP address range where the Tencent Cloud container is located to the opposite routing device.

#### Expected Result

Containers can communicate with opposite servers. See the figure below:
![](https://main.qcloudimg.com/raw/c6e951242ab093b72cd74ad15b1a0b75.png)
Containers can communicate with VPN opposite servers.

>If you want your cloud containers to communicate with your IDC over an IPsec VPN, you need to set the **SPD policy** and **routing table**.
