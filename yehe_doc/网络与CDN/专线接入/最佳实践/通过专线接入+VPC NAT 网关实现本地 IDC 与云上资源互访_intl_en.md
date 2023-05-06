This document describes how to achieve resource access between an Internet Data Center (IDC) and VPC by using Direct Connect and the SNAT and DNAT features of a VPC NAT gateway.
>?
>- V3R2 NAT direct connect gateway is in beta testing. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- VPC NAT gateway is in beta testing. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

## Scenarios
You can use Direct Connect and a VPC NAT gateway to build direct connections for resource access between Tencent Cloud and your IDC without causing conflicts between specified IP addresses.
![](https://qcloudimg.tencent-cloud.cn/raw/eed46c83d8dcb6747d2a2bc26f85168c.png)

## Prerequisites
- You have built a connection. For more information, see [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).
- You have [created a VPC](https://intl.cloud.tencent.com/document/product/215/31805).

## Notes
- You must configure network address mappings for the NAT gateway.
- When you configure routing rules for a VPC NAT gateway, SNAT-Local-Layer-3, SNAT-Local-Layer-4, and DNAT-Peer-Layer-4 rules are mapped automatically. Peer-Layer-3 rules cannot be mapped. In addition, VPC CIDR is not published by default. Therefore, if you specify only Peer-Layer-3 rules, you must manually configure VPC CIDR routing for your IDC. We recommend that you use a Peer-Layer-3 rule with a Local-Layer-3 or Local-Layer-4 rule.

## Directions
### Step 1: Create a VPC NAT gateway[](id:step1)
1. Log in to the [NAT Gateway console](https://console.cloud.tencent.com/vpc/nat?rid=1).
2. In the left sidebar, choose **NAT Gateway** > **VPC NAT Gateway**, select the region and the VPC in which the gateway resides, and click **Create**.
3. Specify parameters and click **Activate now**. See the following figure:
>?For more information about the configuration, see [NAT Gateway](https://www.tencentcloud.com/document/product/1015).
>


### Step 2: Create an NAT direct connect gateway
1. Log in to the [**Direct Connect Gateway console**](https://console.cloud.tencent.com/vpc/dcgw?rid=8).
2. In the **Create a direct connect gateway** window, enter a gateway name, select the zone, select **NAT** for **Associated Network**, and select an NAT instance to which the direct connect gateway associates.
3. Agree to the redundant gateway cleanup agreement and click **OK**.
>?For more information about parameter configuration, see [Creating a Direct Connect Gateway](https://www.tencentcloud.com/document/product/216/19256)
>

### Step 3: Create a dedicated tunnel
The tunnels created on the connections vary depending on the access method. You can create tunnels of one of the following types as needed:
- The tunnels created on your own connections are exclusive dedicated tunnels, which are applicable to scenarios with requirements for high-bandwidth access and exclusive access. For details, see [Exclusive Dedicated Tunnel](https://www.tencentcloud.com/document/product/216/48574).
- The tunnels created on our partners' connections pre-established in Tencent are shared dedicated tunnels, which are applicable to scenarios where there is no need for high-bandwidth access and the cloudification time is short. For details, see [Shared Dedicated Tunnel](https://www.tencentcloud.com/document/product/216/48575).

### [](id:step4)Step 4: Configure SNAT and DNAT routing rules for the VPC NAT gateway
1. Log in to the [NAT Gateway](https://console.cloud.tencent.com/vpc/nat?rid=1) console and click **VPC NAT Gateways** in the left sidebar. On the page that appears, click the ID of the created VPC NAT gateway.
2. On the details page of the VPC NAT gateway, configure SNAT and DNAT rules on the **SNAT** and **DNAT** tabs respectively. This document uses SNAT rules as an example.
3. On the **SNAT** tab, click **Create**. On the **Create SNAT rule** page, select **Layer-3** for **Mapping type**, enter the VPC IP address in the **Source IP** field, and enter an IP address or IP address pool in the **Mapped IP/Mapped IP pool** field as needed.
You can click **+ New line** to configure multiple SNAT routing rules.
4. Click **OK**.
For more information about parameter configuration, see [Operation Overview](https://www.tencentcloud.com/document/product/647/35109).
>

### [](id:step5)Step 5: Configure routing policies in the VPC route table
1. Log in to the VPC console and go to the [Route Tables](https://console.cloud.tencent.com/vpc/route?rid=1) page.
2. On the **Route tables** page, find the route table corresponding to your VPC and click the table name.
3. On the details page of the route table, click **+ New routing policies**. In the pop-up window, configure the routing policy.
Specify the IP range of your IDC for **Destination**, **VPC NAT gateway** for **Next hop type**, and the name of the VPC NAT gateway created in [Step 1](#step1) for **Next hop**.
>?For more information about other VPC routing policies, see [Managing Routing Policies](https://intl.cloud.tencent.com/document/product/215/40080).
>


### Step 6: Configure the local IDC
Download the CPE configuration guide and follow the instructions for configuration.
>?For more information about parameter configuration, see [Exclusive Virtual Interface](https://intl.cloud.tencent.com/document/product/216/48574#step4).
>

### Step 7: Test connectivity
Test whether CVM instances and your local IDC are connected.
1. Log in to an CVM instance in your VPC.
2. Run the ping command to test the IP address of the server in your local IDC. If ICMP packets are returned, the CVM instance is connected to the IDC.
   3. Run the packet capture command on the server in your local IDC. You can see that the source IP address of the packets is the specified IP address after SNAT.
>?If no packets are returned, perform the following operations for troubleshooting:
>- Check the VPC route table. Ensure that you have specified the VPC NAT gateway for next hop. For more information, see [Step 5](#step5).
>- Check whether you have configured an SNAT or DNAT rule. If no rules are configured, the connection fails. For more information, see [Step 4](#step4).
>- Ensure that the status of the dedicated tunnel is **Connected**. The BGP status of Dedicated Tunnel 2.0 must be **established**.
>- If you have tried all above operations and the issue persists, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
>
3. Log in to the server in your local IDC and run the `ssh root@NAT IP` command.
   If packets are returned, the connection succeeds.
