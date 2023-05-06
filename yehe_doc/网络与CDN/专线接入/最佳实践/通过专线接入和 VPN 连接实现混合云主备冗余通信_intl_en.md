If your business is deployed in both a local IDC and a Tencent Cloud VPC, you can connect them via Direct Connect or VPN. To improve the business availability, you set up both DC and VPN connections and configure them as the primary and secondary linkage for redundant communication. This document guides you through how to configure the DC and VPN connection as primary/secondary linkages to connect your IDC to the cloud.
>?
>- Currently, the route priority feature is in beta testing. To use this feature, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
>- The next hop type determines the route priority in the VPC route table. The default route priority sequence from high to low is CCN, direct connect gateway, VPN gateway, and others.
>- Currently, the route priority cannot be adjusted in the console. If you want to adjust the route priority, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
>- Currently, automatic switching is not supported. When a fault occurs, you must manually switch the route in the VPC.
>



## Scenarios
You have deployed businesses in a Tencent Cloud VPC and an IDC. To interconnect them, you need to configure network connection services for high-availability communications as follows:
+ Direct Connect (primary): connects the local IDC to a VPC-based direct connect gateway through a connection. When the connection linkage is normal, all data traffic between the IDC and the VPC is forwarded through the connection.
+ VPN connection (secondary): establishes an IPsec VPN tunnel to interconnect the local IDC and the Tencent Cloud VPC. When the connection linkage fails, traffic will be forwarded using this linkage to ensure the business availability.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jVKT137_PRELIM__%E4%B8%93%E7%BA%BF%E6%8E%A5%E5%85%A5_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US.svg)

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
	

## Flowchart
<dx-steps>
- [Connect IDC to VPC through Direct Connect](#step1)
- [Connect IDC to VPC through a VPN connection](#step2)
- [Configure network probes](#step3)
- [Configure an alarm policy](#step4)
- [Switch between the primary and secondary routes](#step5)
  </dx-steps>

## Directions

### [](id:step1)Step 1: Connect IDC to VPC through Direct Connect
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Connections** on the left sidebar to create a connection.
2. Click **Direct Connect Gateway** on the left sidebar and then click **+New** to create a direct connect gateway. In this example, we create a standard direct connect gateway that connects to a VPC. If the IP range of your IDC conflicts with the IP range of the VPC, you can create a direct connect gateway of the NAT type.
3. Click **Exclusive virtual interface** in the left sidebar and then click **+ New** to create a dedicated tunnel. Enter a tunnel name and select the connection type and the direct connect gateway that is created. Configure the IP addresses on the Tencent Cloud and IDC sides, select the static route, and enter the IDC IP range. After the configuration is complete, click **Download configuration guide** and complete the IDC device configurations as instructed in the guide.
4. In the route table associated with the VPC subnet for communication, configure a routing policy with the direct connect gateway as the next hop and IDC IP range as the destination.
>?For detailed configurations, see [Getting Started](https://www.tencentcloud.com/document/product/216/7557).
>


###  [](id:step2)Step 2: Connect IDC to VPC through a VPN connection
1. Log in to the [VPN Gateway console](https://console.cloud.tencent.com/vpc/vpnGw?rid=1) and click **+New** to create a VPN gateway for which the value of **Associate Network** is **Virtual Private Cloud**.
2. Click **Customer Gateway** on the left sidebar and then click **+New** to configure a customer gateway. A customer gateway is a logical object of the VPN gateway on the IDC side. Enter the public IP address of the VPN gateway on the IDC side, such as `202.xx.xx.5`.
3. Click **VPN Tunnel** on the left sidebar and then click **+New** to complete configurations such as SPD policy, IKE, and IPsec.
4. Configure the same VPN tunnel as the step 3 on the local gateway device of the IDC to ensure a normal connection.
5. In the route table associated with the VPC subnet for communication, configure a routing policy with the VPN gateway as the next hop and IDC IP range as the destination.
>?For detailed directions, see [Connecting VPC to IDC (Route Table)](https://www.tencentcloud.com/document/product/1037/39675).
>

###  [](id:step3)Step 3: Configure network probes
>?After the first two steps, there are two VPC routes to IDC. That is, both direct connect gateway and VPN gateway act as the next hop. By default, the direct connect gateway route has a higher priority, making it the primary path and the VPN gateway the secondary path.

To stay on top of the primary/secondary connection quality, configure two network probes separately to monitor the key metrics such as latency and packet loss rate and check the availability of primary/secondary routes.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/detection?rid=1).
2. Click **+New** to create a network probe. Enter a probe name and destination IP, select a VPC and a subnet, and then set **Source Next Hop** to direct connect gateway.
3. Repeat the [step 2](#step2) and set the **Source Next Hop** to VPN gateway. After the configuration is complete, you can check the probed network latency and packet loss rate of the direct connect gateway and VPN connection.
>? For detailed configurations, see [Network Probe](https://www.tencentcloud.com/document/product/215/35522).
>

### [](id:step4)Step 4: Configure an alarm policy
You can configure an alarm policy for linkages. When a linkage has an exception, alarm notifications are sent to you automatically via emails and SMS message, alerting you of the risks in advance.
1. Log in to the Tencent Cloud Observability Platform console and go to the [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy) page.
2. Click **Create**. Enter a policy name, select VPC/Network Probe for the policy type, and specify the network probe instances as the alarm object. Then, configure trigger conditions, alarm notifications, and other information and click **Complete**.

### [](id:step5)Step 5: Switch between primary and secondary routes
After receiving the exception alarms about the direct connect gateway, you need to manually disable the primary route, and forward traffic to the secondary route VPN gateway.
1. Log in to the VPC console and go to the [Route Tables](https://console.cloud.tencent.com/vpc/route?rid=1) page.
2. Locate the route table associated with the VPC subnet for communication, click the **ID/Name** to enter its details page. Click <img src="https://main.qcloudimg.com/raw/af79ad3ab5488ea94ead43a8fba3486f.png" width="3%" /> to disable the primary route with the CCN as the next hop. Then the VPC traffic destined to IDC will be forwarded to the VPN gateway, instead of the direct connect gateway.
