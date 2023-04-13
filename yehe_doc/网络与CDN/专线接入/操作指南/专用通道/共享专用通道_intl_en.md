A dedicated tunnel is a network linkage segmentation of a connection. You can create dedicated tunnels that connect to different direct connect gateways to enable communication between your on-premises IDC and multiple VPCs. This document describes how to create a shared dedicated tunnel.

## Background
CTCC, CMCC, CUCC, CITIC and other partners with A14 and A26 telecommunications qualifications have pre-established connections with Tencent connection access points. You can access Tencent Cloud by sharing the partners' connections according to your actual needs.

A shared dedicated tunnel is a dedicated tunnel created using the partner's connection. It is applicable for scenarios where there is no need for high-bandwidth access and the cloudification time is short.
The procedure for enabling a shared dedicated tunnel is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/1b2bc5e18ecb6cb7477e580a2204c3ba.jpg)

## Prerequisites
- Obtain the connection instance ID for the shared dedicated tunnel and Tencent Cloud entity accounts' UINs of the connection provider from the supplier.
- Create a direct connect gateway as instructed in [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).


## Directions
### Step 1: Apply for a dedicated tunnel
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/conn) console.
2. On the **Dedicated Tunnels** page, click **+ New**, complete basic configurations such as name, connection type, access network, gateway region and associated direct connect gateway, and click **Next**.
![]()
<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>Name</td>
<td>Enter a name for your dedicated tunnel.</td>
</tr>
<tr>
<td>Connection type</td>
<td>Select the shared connection.</td>
</tr>
<tr>
<td>Direct Connect</td>
<td>Provides a connection provider that establishes a pre-connection with Tencent: <ul><li>Currently, only suppliers with A14 and A26 telecommunication qualifications (such as CTCC, CMCC, CUCC, and CITIC) are supported to create a shared tunnel.</li><li>If you need to share your connection with a subsidiary or your other Tencent Cloud accounts, please contact Tencent technical support for assistance.</li><li>The fee of sharing the tunnel shall be borne by the tunnel user.</li></ul></td>
</tr>
<tr>
<td>Shared tunnel ID</td>
<td>Enter the ID of the connection instance used to create the shared tunnel.</td>
</tr>
<tr>
<td>Access Network</td>
<td><ul><li>When the tunnel type is `1.0` and `2.0`, you can select a CCN or VPC.</li></ul></td>
</tr>
<tr>
<td>Region</td>
<td><ul><li>If you select <b>CCN</b>, the region defaults to the region where the CCN-based direct connect gateway is located.</li><li>If you select <b>VPC</b>, for a dedicated tunnel 2.0, you can only select the region where the connection is located; for a dedicated tunnel 1.0, you can select any region.</li></ul></td>
</tr>
<tr>
<td>VPC</td>
<td>Select the VPC instance to be connected to by the dedicated tunnel.</td>
</tr>
<tr>
<td>Direct Connect Gateway</td>
<td>Associate an existing direct connect gateway with the dedicated tunnel. A 2.0 tunnel does not support a NAT-type direct connect gateway.</td>
</tr>
</table>
3. Configure the following parameters on the **Advanced Configuration** page.
![]()
<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>VLAN ID</td>
<td>One VLAN corresponds to one tunnel. Valid range: [0，3000).<ul><li>If the value is 0, only 1 tunnel can be created. Use physical layer 3 interfaces for the connection.</li><li>If the value is between 1 and 2999, multiple tunnels can be created. Use layer 3 sub-interfaces for the connection. When only the layer 2 connection is supported, please disable the STP protocol under the interface at the IDC side. In the case of multiple dedicated tunnels, when the MSTP connection passes through multiple VLANs, the carrier line needs to enable the Trunk mode./li></ul></td>
</tr>
<tr>
<td>Bandwidth</td>
<td>Specify the bandwidth cap of the dedicated tunnel, which cannot exceed the maximum bandwidth of the associated connection. If the billing mode is pay-as-you-go by monthly 95th percentile, this parameter does not mean the billable bandwidth.</td>
</tr>
<tr>
<td>Tencent Cloud Primary IP1</td>
<td>Enter the connection IP address on the Tencent Cloud side. Do not use the following IP ranges or IP addresses: 169.254.0.0/16, 127.0.0.0/8, 255.255.255.255, 224.0.0.0 - 239.255.255.255, 240.0.0.0 - 255.255.255.254.</td>
</tr>
<tr>
<td>Tencent Cloud Primary IP2</td>
<td>Enter the secondary IP address of the connection on the Tencent Cloud side. The secondary IP will be automatically used to ensure the normal operation of your business when the Tencent Cloud primary IP fails and becomes unavailable. This field is not supported when the mask of the secondary IP address is 30 or 31.</td>
</tr>
<tr>
<td>CPE Peer IP</td>
<td>Configure the connection IP address on the user (or carrier) side.</td>
</tr>
<tr>
<td>Routing Mode</td>
<td>Select:<ul><li>BGP Routing: Applicable to the exchange of routing information and network accessibility across autonomous systems (AS).</li><li>Static Routing: Applicable to a simper network environment.</li></ul></td>
</tr>
<tr>
<td>Health Check</td>
<td>Health check is enabled by default. BFD and NQA modes are provided. For details, see <a href="https://intl.cloud.tencent.com/document/product/216/46292">Dedicated tunnel health check</a>.</td>
</tr>
<tr>
<td>Check mode</td>
<td>BFD and NQA modes are provided</td>
</tr>
<tr>
<td>Health Check Interval</td>
<td>The interval between two health checks.</td>
</tr>
<tr>
<td>Number of Failed Health Checks</td>
<td>Switch the route after the configured consecutive failed health checks.</td>
</tr>
<tr>
<td>BGP ASN</td>
<td>Enter the BGP neighbor ASN on the CPE side. Note that the Tencent Cloud ASN is 45090. If this field is left empty, a random ASN will be assigned.</td>
</tr>
<tr>
<td>BGP Key</td>
<td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It does not support [?&"\+] and spaces.</td>
</tr>
</table>

>? [](id:Breakup)If **Static** is selected as the routing mode, do not directly publish the following routes: `9.0.0.0/8, `10.0.0.0/8`, `11.0.0.0/8`, `30.0.0.0/8`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12` and `192.168.0.0/16` when configuring IDC IP ranges. Instead, you need to first split them as follows.
>- `9.0.0.0/8` is split into `9.0.0.0/9` + `9.128.0.0/9`.
>- `10.0.0.0/8` is split into `10.0.0.0/9` + `10.128.0.0/9`.
>- `11.0.0.0/8` is split into `11.0.0.0/9` + `11.128.0.0/9`.
>- `30.0.0.0/8` is split into `30.0.0.0/9` + `30.128.0.0/9`.
>- `100.64.0.0/10` is split into `100.64.0.0/11` + `100.96.0.0/11`.
>- `131.87.0.0/16` is split into `131.87.0.0/17` + `131.87.128.0/17`.
>- `172.16.0.0/12` is split into `172.16.0.0/13` + `172.24.0.0/13`.
>- `192.168.0.0/16` is split into `192.168.0.0/17` + `192.168.128.0/17`.
>
4. Configure IDC devices. You can click **Download configuration guide** to download related files and complete the configurations as instructed in the guide.
![]()
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
<th>Notes</th>
</tr>
<tr>
<td>CPE IP Range</td>
<td>Enter the customer IP range if <b>Static</b> is selected as the routing mode. This parameter cannot conflict with the VPC IP range in a non-NAT mode.</td>
<td>You can update the IP range later via "Change Tunnel" in the console.</td>
</tr>
</table>
5. Click **Submit**.
After being created, the shared dedicated tunnel is in **Pending accepted** status. It will turn to be **Connected** after being approved by the connection provider.

### Step 2: Set the alarm recipient
After a dedicated tunnel is created, Tencent Cloud automatically configures four event alarms such as `DirectConnectTunnelDown`, `DirectConnectTunnelBFDDown`, `DirectConnectTunnelBGPSessionDown`, and `DirectConnectTunnelRouteTableOverload`, helping you monitor and manage your dedicated tunnels. For more information on the event alarms, see [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403).
The automatically created default alarm policy is not configured with recipient information, and only supports console alarms. You can configure alarm recipients. For details, see [Configuring Alarm Policies](https://intl.cloud.tencent.com/ document/product/216/38402).
