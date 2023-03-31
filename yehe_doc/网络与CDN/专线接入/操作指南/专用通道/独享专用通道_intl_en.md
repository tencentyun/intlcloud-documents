## Prerequisites
- Apply for a connection. See [Applying for a Connection](https://intl.cloud.tencent.com/document/product/216/19244).
- Create a direct connect gateway. See [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).

## Directions
### Step 1: Apply for a dedicated tunnel
1. Log in to the [Direct Connect - Dedicated Tunnel console](https://console.cloud.tencent.com/dc/dcConn).
2. On the left sidebar, click **Dedicated tunnels > Exclusive virtual interface**, click **+ New**, complete basic configurations such as name, connection type, access network, gateway region and associated direct connect gateway, and click **Next**.
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
<td>Tunnel Type</td>
<td>Set to <b>1.0</b> or <b>2.0</b> depending on the associated connection you select.</td>
</tr>
<tr>
<td>Connections</td>
<td>Select a connection you have applied for.</td>
</tr>
<tr>
<td>Access Network</td>
<td><ul><li>For a 1.0 tunnel, select from CCN and VPC.</li><li>
 For a 2.0 tunnel, select either <b>CCN</b>、<b>Virtual Private Cloud</b> and <b>NAT network</b>.</li></ul></td>
</tr>
<tr>
<td>Region</td>
<td><ul><li>If <b>CCN</b> is selected as the access network, the region is where the CCN-based direct connect gateway resides by default.</li><li>
 If <b>VPC</b> is selected as the access network, you can only select the region where the connection resides for a 2.0 tunnel and select any region for a 1.0 tunnel.</li>
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
<img src="" width="85%"> 
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
<td>Interconnection Method</td>
<td><ul><li>By default, <b>Manual allocation</b> is selected for 2.0 tunnels.</li><li>Both <b>Manual allocation</b> and <b>Automatic Assignment</b> are supported for 1.0 tunnels. If <b>Automatic Assignment</b> is selected, there is no need to configure <b>Tencent Cloud Primary Edge IP</b> and <b>CPE Peer IP</b>.</li></ul></td>
</tr>
<tr>
<td>Tencent Cloud Primary IP</td>
<td>Enter the connection IP address on the Tencent Cloud side. Do not use the following IP ranges or IP addresses: 169.254.0.0/16, 127.0.0.0/8, 255.255.255.255, 224.0.0.0 - 239.255.255.255, 240.0.0.0 - 255.255.255.254.</td>
</tr>
<tr>
<td>Tencent Cloud Primary IP</td>
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
<td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain 6 special characters including ?, &, space, ", \, and +.</td>
</tr>
</table>
<dx-alert infotype="explain" title="">
[](id:Breakup)If **Static** is selected as the routing mode, do not directly publish the following routes: `9.0.0.0/8, `10.0.0.0/8`, `11.0.0.0/8`, `30.0.0.0/8`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12` and `192.168.0.0/16` when configuring IDC IP ranges. Instead, you need to first split them as follows.
 - `9.0.0.0/8` is split into `9.0.0.0/9` + `9.128.0.0/9`.
 - `10.0.0.0/8` is split into `10.0.0.0/9` + `10.128.0.0/9`.
 - `11.0.0.0/8` is split into `11.0.0.0/9` + `11.128.0.0/9`.
 - `30.0.0.0/8` is split into `30.0.0.0/9` + `30.128.0.0/9`.
 - `100.64.0.0/10` is split into `100.64.0.0/11` + `100.96.0.0/11`.
 - `131.87.0.0/16` is split into `131.87.0.0/17` + `131.87.128.0/17`.
 - `172.16.0.0/12` is split into `172.16.0.0/13` + `172.24.0.0/13`.
 - `192.168.0.0/16` is split into `192.168.0.0/17` + `192.168.128.0/17`.
</dx-alert>
4. Configure IDC devices. You can click **Download configuration guide** to download related files and complete the configurations as instructed in the guide. <p><img src=""></img></p>
<table>
<tr>
<th width="20%">Parameter</th>
<th width="40%">Configuration</th>
<th width="40%">Remarks</th>
</tr>
<tr>
<td>CPE IP Range</td>
<td>Enter the customer IP range if <b>Static</b> is selected as the routing mode. This parameter cannot conflict with the VPC IP range in a non-NAT mode.</td>
<td>You can update the IP range later via "Change Tunnel" in the console.</td>
</tr>
</table>
5. Click **Submit**.

### Step 2: Set the alarm recipient
After a dedicated tunnel is created, Tencent Cloud automatically configures four event alarms such as `DirectConnectTunnelDown`, `DirectConnectTunnelBFDDown`, `DirectConnectTunnelBGPSessionDown`, and `DirectConnectTunnelRouteTableOverload`, helping you monitor and manage your dedicated tunnels. For more information on the event alarms, see [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403).
The automatically created default alarm policy is not configured with recipient information, and only supports console alarms. You can configure alarm recipients by yourself. For details, see [**Configuring Alarm Policies**](https://intl.cloud.tencent.com/ document/product/216/38402).

## Connection Status
After the dedicated tunnel is created, it will be displayed on the **Dedicated Tunnels** page in the **Applying** status.
The possible connection statuses of a dedicated channel include:
![](https://qcloudimg.tencent-cloud.cn/raw/d7a7d15a93d8de373f186870a3b23f42.jpg)

- **Applying**
  The system has received your application for a new dedicated tunnel and is ready to start the creation.
- **Configuring**
  The system is delivering the parameter configuration. If this status lasts for a long time, a failure may occur. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- **Configured**
  The system has completed the configuration based on the specified parameters but is unable to ping to the IP address of your IDC. A dedicated tunnel in this status can be deleted.
- **Connected**
  The system pings to your IDC device successfully. However, this does not mean that your business is connected. You have to configure the [route table](https://console.cloud.tencent.com/vpc/route?rid=1) of the VPC or CCN instance to implement the connection.
- **Deleting**
  If you delete your dedicated tunnel on the console, the connection status of the dedicated tunnel becomes **Deleting**. If this status lasts for a long time, a failure may occur. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
