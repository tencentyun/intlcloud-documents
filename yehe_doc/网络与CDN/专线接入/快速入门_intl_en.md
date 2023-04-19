A VPC-based direct connect gateway can be used to interconnect one Tencent Cloud VPC with one or more local IDCs. This document describes how to use a VPC-based direct connect gateway to build the Direct Connect network architecture that connects a VPC in Beijing to an IDC in Guangzhou.

## Background
The following figure shows you how to interconnect a Tencent Cloud VPC (`172.21.0.0/24`) and a local IDC (`192.168.0.0/24`) with a bandwidth of 2 Mbps.
<img src="https://main.qcloudimg.com/raw/92fffb3c128b9f8cf523d360e97cdc6b.png" width="80%" />

Follow the steps below:
<dx-steps>
- [Create a connection](#dc): connects customer’s local IDC to Tencent Cloud.
- [Create a direct connect gateway](#dcgw): as the traffic entry of the Direct Connect, connects a Tencent Cloud VPC to connections (dedicated tunnels).
- [Create a dedicated tunnel](#conn): acts as the network segmentations of a connection.
- [Configure the route table](#route): configures a routing policy in the route table of a VPC subnet to enable connection.
- [Set alarms](#alarm): configures recipients for alarm policies automatically created together with the connection and dedicated tunnel.
</dx-steps>

## Prerequisites
- You have built a Tencent Cloud VPC in the Beijing region as instructed in [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).

## How It Works
### Step 1: create a connection[](id:dc)
To create a connection, you need to first confirm the information and submit an application in the console, and then the carrier will start the engineering investigation and wiring. This process takes about 2-3 months. For more information, see [Connection Overview](https://intl.cloud.tencent.com/document/product/216/38524). Perform the following steps to apply for a connection in the console.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc).
2. Click **Connections** on the left sidebar to access the **Connections** page. Click **+New**.
3. In the pop-up window, read **Tencent Cloud Direct Connect Service Level Agreement**, select **Read and Agreed**, and click **Next**.
4. Complete the following configurations and click **OK**。
<table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td>Connection Name</td><td>Enter a name for the connection, such as "Connection to Beijing IDC".</td></tr>
    <tr><td>Region</td><td>Select <b>Beijing</b>.</td></tr><tr>
<td>Access point</td>
<td>We recommend you first search for access points and check their distances to your IDC, and then select the nearest access point. For more information, see <a href="https://intl.cloud.tencent.com/document/product/216/41429">Connection Access Point</a>.</td></tr>
<tr>
<td>Connection provider</td>
<td>Select an eligible carrier, such as <b>CTCC</b>.</td></tr>
<tr>
<td>Cloud port</td>
<td>Ports in 1, 10, and 100 Gbps are available. To use a 100 Gbps port, please submit a ticket. Select <b>1 Gbps</b> as an example.</td></tr>
<tr>
<td>Port type</td>
<td>Choose fiber optic port or electrical port as needed. The available ports vary with the port type. For example, 1 Gbps ports include fiber optic port and electrical port, while 10 Gbps ports only include fiber optic port. Select <b>Fiber optic port</b> as an example.</td></tr>
<tr>
<td>Bandwidth Cap</td><td>Select <b>998 Mbps</b> as an example.</td></tr>
</table>

<dx-alert infotype="explain" title="">
For more information on parameter configurations, see [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244)
</dx-alert>

5. After your application is submitted, Tencent Cloud Direct Connect representative will comprehensively assess Direct Connect resources and then check with you the service details over the phone. After the connection is confirmed to be accessible, you should complete the payment in the console.

### Step 2: create a direct connect gateway[](id:dcgw)
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc).
2. Select **Beijing** in the region at the top of the **Direct Connect Gateway** page, and click **+New**.
3. Complete the configurations in the pop-up window and click **OK**.
<table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>Name</td><td>Enter a name for the direct connect gateway, such as "Beijing VPC - Guangzhou IDC".</td></tr>
<tr>
<td>Associate Network</td><td>Select <b>VPC</b>.</td></tr>
<tr>
<td>Network</td><td>Select an existing VPC instance.</td></tr>
<tr>
<td>Gateway type</td>
<td>Select <b>Standard</b> as an example.<ul><li><b>Standard</b>: does not support the network address translation feature.</li><li><b>NAT Type</b>: supports the network address translation feature. You should also configure the <a href="https://intl.cloud.tencent.com/document/product/216/19257">network address translation (NAT)</a> if you want to use a NAT direct connect gateway.</li></ul></td></tr>
</table>

### Step 3: create a dedicated tunnel[](id:conn)
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc).
2. Click **Dedicated Tunnels** on the left sidebar to access the **Dedicated Tunnels** page. Click **+New**.
3. Complete basic configurations such as name, connection type, access network, region and associated direct connect gateway, and click **Next**.
<table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>Name</td><td>Enter a name for the dedicated tunnel, such as "Beijing VPC - Guangzhou IDC".</td></tr>
<tr>
<td>Connection</td><td>Select the connection created in <a href="#dc">Step 1</a>.</td></tr>
<tr>
<td>Access Network</td><td>Select <b>VPC</b>.</td></tr>
<tr>
<td>VPC</td><td>Select an existing VPC instance.</td></tr>
<tr>
<td>Direct Connect Gateway</td><td>Select the direct connect gateway created in <a href="#dcgw">Step 2</a>.</td></tr>
</table>
<dx-alert infotype="explain" title="">
For more information on the parameter configurations, see [Creating a Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/19250)
</dx-alert>
4. Configure the following parameters in the **Advanced Configuration** tab, and click **Next**.
<table>
<tr>
<th>Parameter</th>
<th>Definition</th>
</tr>
<tr>
<td>VLAN ID</td>
<td>A VLAN corresponds to a tunnel. Enter a value within the range of 0-3000. Entering <b>0</b> means one dedicated tunnel can be created. Enter “0” as an example.</td>
</tr>
<tr>
<td>Peer IP</td>
<td>Peer IP addresses need to be manually configured by default.</td>
</tr>
<tr>
<td>Bandwidth</td>
<td>Specify the bandwidth cap of the dedicated tunnel, which cannot exceed the maximum bandwidth of the associated connection. Set it to “2 Mbps” as an example.</td>
</tr>
<tr>
<td>Tencent Cloud Primary IP</td>
<td>Enter the connection IP address on the Tencent Cloud side. Set it to “172.21.0.0/24” as an example.</td>
</tr>
<tr>
<td>Tencent Cloud Secondary IP</td>
<td>Enter the secondary IP address of the connection on the Tencent Cloud side. Set it to “172.21.0.2/24” as an example.</td>
</tr>
<tr>
<td>CPE Peer IP</td>
<td>Configure the connection IP address on the user (or carrier) side. Set it to “172.21.0.1/24” as an example.</td>
</tr>
<tr>
<td>Routing Mode</td>
<td>Select <b>Static</b>.</td>
</tr>
<tr>
<td>Health Check</td>
<td>Health check is disabled by default. To enable it, see <a href="https://intl.cloud.tencent.com/document/product/216/46292">Dedicated tunnel health check</a>.</td>
</tr>
<tr>
<tr>
<td>CPE IP range</td><td>Select <b>192.168.0.0/24</b> as an example.</td></tr>
</table>

5. Configure IDC devices. You can click **Download configuration guide** to download related files and complete the configurations as instructed in the guide.
<table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>CPE IP range</td><td>Enter the customer IP range if <b>Static</b> is selected as the routing mode. This parameter cannot conflict with the VPC IP range in a non-NAT mode.</td></tr>
</table>
6. Click **Submit**.

### Step 4: configure the route table[](id:route)
To use a VPC-based direct connect gateway, configure a routing policy with direct connect gateway as the next hop and IDC IP range as the destination in the route table of the VPC subnet to enable communication.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
2. Select **Route Tables** on the left sidebar, and click the **ID/Name** of the target VPC to enter its details page.
3. Click **+New routing policies** on the **Basic Information** page.
4. In the pop-up window, enter “192.168.0.0/24” for the **Destination**, select “Direct Connect Gateway” for the **Next hop type**, locate the direct connect gateway created in [Step 2](#dcgw) for the **Next hop**, and click **Create**.
5. Click **Confirm**.

### Step 5: set alarms[](id:alarm)
After a connection and a dedicated tunnel are created, Cloud Monitor will automatically create a default alarm policy for each service. This default alarm policy does not configure recipient information, so you can only view alarms on the console. To configure a recipient, take the following steps.
<dx-fold-block title="What is a default alarm policy?">
- Default alarm policy for connections
<table>
<tr><th>Metric</th><th>Statistical Period</th><th>Condition</th><th>Condition Value</th><th>Consecutive Periods</th><th>Policy</th></tr>
<tr>
<td>Bandwidth utilization </td><td>1 minute</td><td>>=</td><td>80%</td><td>5 periods</td><td>Alarm once a day</td></tr>
</table>
- Default alarm policy for dedicated tunnels: available event alarms are DirectConnectTunnelDown, DirectConnectTunnelBFDDown, DirectConnectTunnelBGPSessionDown, and DirectConnectTunnelRouteTableOverload.
</dx-fold-block>

1. Log in to the cloud monitor console. View [Monitoring Overview](https://console.cloud.tencent.com/monitor/overview)
2. Select **Alarm Configuration** > **Alarm Policy** on the left sidebar. Click **Advanced Filter**, select **All** for **Monitoring Type**, and select the relevant product for **Policy type**.
3. Click the name of the target default policy in the **Alarm Management** list.
4. On the **Manage alarm policy** page, select a notification template.
Click **Edit Recipient** to configure alarm recipients in the template. If existing templates are not suitable, you can click **Create Template** and configure the template to create as prompted. Then you can select the template to configure alarm recipients.

