If your business is deployed in both a local IDC and a Tencent Cloud VPC, you can connect them via Cloud Connect Network (CCN) or VPN. To improve the business availability, you set up both CCN and VPN connections and configure them as the primary and secondary linkage for redundant communication. This document guides you through how to configure the CCN and VPN connection as primary/secondary linkages to connect your IDC to the cloud.
>?The route priority feature is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


## Scenarios
Suppose you have deployed your business in both Tencent Cloud VPC and an IDC. To interconnect them, you need to configure network connection services for high-availability communications as follows:
+ CCN (primary): connects the local IDC to a CCN-based direct connect gateway through a physical connection, and adds both the direct connect gateway and the VPC to a CCN to enable interconnection. When the connection linkage is normal, all data traffic between the IDC and the VPC are forwarded over CCN through the physical connection.
+ VPN connection (secondary): establishes an IPsec VPN tunnel to interconnect the local IDC and the Tencent Cloud VPC. When the connection linkage fails, traffic will be forwarded using this linkage to ensure the business availability.

![](https://main.qcloudimg.com/raw/ce97fc610f1119e92094f72027a3aa9b.png)

## Prerequisites
+ Your local IDC gateway device should support the IPsec VPN feature and can act as a customer gateway to create a VPN tunnel with the VPN gateway.
+ The IDC gateway device has configured with a static IP address.
+ Sample data and configuration:
<table>
<th colspan="3">Configuration item</th>
<th>Sample value</th>
<tr>
<td rowspan="4">Network</td>
<td rowspan="2">VPC information</td>
<td>Subnet CIDR block</td>
<td>192.168.1.0/24 </td>
</tr>
<tr>
<td>Public IP of the VPN gateway</td>
<td>203.xx.xx.82</td>
</tr>
<tr>
<td rowspan="2">IDC information</td>
<td>Subnet CIDR block</td>
<td>10.0.1.0/24</td>
</tr>
<tr>
<td>Public IP of the gateway</td>
<td>202.xx.xx.5</td>
</tr>
</table>
​	

## Steps
<dx-steps>
- [Configure a Direct Connect instance](#step1)
- [Configure a VPN connection](#step2)
- [Configure network probes](#step3)
- [Configure an alarm policy](#step4)
- [Switch between the primary and secondary routes](#step5)
</dx-steps>

## Directions

### [](id:step1)Step 1: connect IDC to VPC through CCN
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Connections** on the left sidebar to create a connection.
2. Log in to the [VPC console](https://console.intl.cloud.tencent.com/vpc/vpc?rid=4) and click **Direct Connect Gateway** on the left sidebar. Click **+New** to create a direct connect gateway for which the **Associate Network** is **CCN**.
3. Click the **ID/Name** of the direct connect gateway just created to enter its details page. Select the **IDC IP Range** tab to enter the IDC IP range, such as `10.0.1.0/24`.
4. Go to the [CCN](https://console.cloud.tencent.com/vpc/ccn) page and click **+New** to create a CCN instance.
5. Go to the [Dedicated Tunnels](https://console.cloud.tencent.com/dc/dc) page and click **+New** to create a dedicated tunnel to connect the CCN-based direct connect gateway. Enter the tunnel name, select **CCN** for the **Access Network**, and then select the CCN-based direct connect gateway instance created earlier. Configure the IP addresses on both the Tencent Cloud and IDC sides, and select the BGP route. After the configuration is complete, click **Download configuration guide** and complete the IDC device configurations as instructed in the guide.
6. Associate the VPC and the CCN-based direct connect gateway with the CCN instance to interconnect the VPC and the IDC.
>? For detailed directions, see [Migrating IDC to the Cloud Through CCN](https://intl.cloud.tencent.com/document/product/216/41747).

###  [](id:step2)Step 2: connect IDC to VPC through a VPN connection
1. Log in to the [VPN Gateway console](https://console.cloud.tencent.com/vpc/vpnGw?rid=1) and click **+New** to create a VPN gateway for which the **Associate Network** is **Virtual Private Cloud**.
2. Click **Customer Gateway** on the left sidebar and click **+New** to configure a customer gateway (a logical object of the VPN gateway on the IDC side). Enter the public IP address of the VPN gateway on the IDC side, such as `202.xx.xx.5`.
3. Click **VPN Tunnel** on the left sidebar and click **+New** to complete configurations such as SPD policy, IKE, and IPsec.
4. Configure the same VPN tunnel as [the step 3](#step3) on the local gateway device of the IDC to ensure a normal connection.
5. In the route table associated with the VPC subnet for communication, configure a routing policy with the VPN gateway as the next hop and IDC IP range as the destination.
>?For detailed configurations of VPN gateways in different versions,
>+ For a VPN gateway v1.0 and v2.0, see [Connecting VPC to IDC (SPD Policy)](https://intl.cloud.tencent.com/document/product/1037/39683).
>+ For a VPN gateway v3.0, see [Connecting VPC to IDC (Route Table)](https://intl.cloud.tencent.com/document/product/1037/39675).

###  [](id:step3)Step 3: configure network probes
>?After the first two steps, there are two VPC routes to IDC. That is, both CCN and VPN gateway act as the next hop. The CCN route has a higher priority, making it the primary path and the VPN gateway the secondary path.
>
To stay on top of the primary/secondary connection quality, configure two network probes separately to monitor the key metrics such as latency and packet loss rate and check the availability of primary/secondary routes.
1. Go to the [Network Probe page](https://console.cloud.tencent.com/vpc/detection?rid=1) on VPC console.
2. Click **+New** to create a network probe. Enter a name and destination IP, select a VPC and subnet, and set the **Source Next Hop** to CCN.
3. Repeat the [step 2](#step2) and set the **Source Next Hop** to VPN gateway. After the configuration is complete, you can check the probed network latency and packet loss rate of the CCN and VPN connection.
>? For detailed configurations, see [Network Probe](https://intl.cloud.tencent.com/document/product/215/35522).
>

### [](id:step4)Step 4: configure an alarm policy
You can configure an alarm policy for linkages. When a linkage has an exception, alarm notifications are sent to you automatically via emails and SMS message, alerting you of the risks in advance.
1. Log in to the CM console and go to the [**Alarm Policy**](https://console.cloud.tencent.com/monitor/alarm2/policy) page.
2. Click **Create**. Enter the policy name, select VPC/Network Probe for the policy type, specify the network probe instances as the alarm object, and configure trigger conditions, alarm notifications, and other information. Then click **Complete**.

### [](id:step5)Step 5: switch between primary and secondary routes
After receiving a CCN network exception alarm, you need to manually disable the primary route, and forward traffic to the secondary route VPN gateway.
1. Log in to the VPC console and go to the [**Route Tables**](https://console.cloud.tencent.com/vpc/route?rid=1) page.
2. Locate the route table associated with the VPC subnet for communication, click the **ID/Name** to enter its details page. Click <img src="https://main.qcloudimg.com/raw/af79ad3ab5488ea94ead43a8fba3486f.png" width="3%" /> to disable the primary route with the CCN as the next hop. Then the VPC traffic destined to IDC will be forwarded to the VPN gateway, instead of the CCN.
