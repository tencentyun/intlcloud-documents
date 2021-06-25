A dedicated tunnel is a network link segmentation of a connection. You can create dedicated tunnels that connect to different direct connect gateways to enable communication between your on-premises IDC and multiple VPCs. After a dedicated tunnel is created, its event alarms will be automatically configured to facilitate your monitoring and OPS of it. This document describes how to apply for a dedicated tunnel.
[](id:background)
> ?The shared connection feature of new dedicated tunnels has stopped accepting new applications since August 1, 2020 at 00:00:00. If you are using a shared connection, it will not be affected by this change, but if you delete it, you will not be able to apply for new dedicated tunnels with shared connection after August 1, 2020 at 00:00:00.
## Prerequisites
- You have applied for a connection as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).
- You have created a direct connect gateway as instructed in [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).

## Directions
### Step 1: apply for a dedicated tunnel
1. Log in to the [Direct Connect - Dedicated Tunnel](https://console.cloud.tencent.com/dc/dcConn) console.
2. Click **+New** at the top of the **Dedicated Tunnels** page, complete the basic configurations such as name, connection type, access network, region and associated direct connect gateway, and click **Next**.
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
<td>Tunnel</td>
<td>Set to<b>1.0</b> or <b>2.0</b> depending on the associated connection you select.</td>
</tr>
<tr>
<td>Connections</td>
<td>Select a connection you have applied for.</td>
</tr>
<tr>
<td>Access Network</td>
<td><ul><li>For a 1.0 tunnel, select from <b>CCN</b>, <b>BM Network</b> and <b>Virtual Private Cloud</b>.</li><li>
 For a 2.0 tunnel, select either <b>CCN</b> or <b>Virtual Private Cloud</b>.</li></ul></td>
</tr>
<tr>
<td>Region</td>
<td><ul><li>If **CCN** is selected as the access network, the region is where the CCN-based direct connect gateway resides by default.</li><li>
 If **VPC** is selected as the access network, you can only select the region where the connection resides for a 2.0 tunnel and select any region for a 1.0 tunnel.</li><li>If **BM Network** is selected as the access network, you can select any region for a 1.0 tunnel.</li></ul></td>
</tr>
<tr>
<td>Virtual Private Cloud</td>
<td>Select the VPC instance to be connected to by the dedicated tunnel.</td>
</tr>
<tr>
<td>Direct Connect Gateway</td>
<td>Associate an existing direct connect gateway with the dedicated tunnel. A 2.0 tunnel does not support a NAT-type direct connect gateway.</td>
</tr>
</table>
3. Configure the following parameters on the **Advanced Configuration** page.
<table>
<tr>
 <th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>VLAN ID</td>
<td>A VLAN corresponds to a tunnel. Enter a value within the range of 0-3000. Entering “0” means one dedicated tunnel can be created. If MSTP connection passes through to multiple VLANs, the carrier needs to enable the Trunk mode.</td>
</tr>
<tr>
<td>Bandwidth</td>
<td>Specify the bandwidth cap of the dedicated tunnel, which cannot exceed the maximum bandwidth of the associated connection. If the billing mode is pay-as-you-go by monthly 95th percentile, this parameter does not mean the billable bandwidth.</td>
</tr>
<tr>
<td>Tencent Cloud Primary IP</td>
<td>Enter the connection IP address on the Tencent Cloud side. DO NOT use the following IP ranges or addresses: <code>169.254.0.0/16</code>, <code>127.0.0.0/8</code>, <code>255.255.255.255</code>, <code>224.0.0.0</code> - <code>239.255.255.255</code>, and <code>240.0.0.0</code> - <code>255.255.255.254</code>.</td>
</tr>
<tr>
<td>Tencent Cloud Secondary IP</td>
<td>Enter the secondary IP address of the connection on the Tencent Cloud side. This field is not supported when the mask of the secondary IP address is 30 or 31.</td>
</tr>
<tr>
<td>CPE Peer IP</td>
<td>Configure the connection IP address on the user (or carrier) side.</td>
</tr>
<tr>
<td>Routing Mode</td>
<td>Select <b>BGP</b> or <b>Static</b>.<br><ul><li>BGP: applies to the exchange of routing information and network accessibility across autonomous systems (AS).</li><li>Static: applies to a simper network environment.</li></ul></td>
</tr>
<tr>
<td>BGP ASN</td>
<td>Enter the BGP neighbor ASN on the CPE side. Note that the Tencent Cloud ASN is 45090. If this field is left empty, a random ASN will be assigned.</td>
</tr>
<tr>
<td>BGP Key</td>
<td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain 6 special characters such as ?, &, space, ", \, and +.</td>
</tr>
<tr>
<td>CPE IP Range</td>
<td>Enter the IP ranges of your IDC, with one IP range per line.</td>
</tr>
</table>
<dx-alert infotype="explain" title="">
If **Static** is selected as the routing mode, do not directly publish the following routes: `9.0.0.0/8, `10.0.0.0/8`, `11.0.0.0/8`, `30.0.0.0/8`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12` and `192.168.0.0/16` when configuring IDC IP ranges. Instead, you need to first split them as follows
 - `9.0.0.0/8` is split into `9.0.0.0/9` + `9.128.0.0/9`.
 - `10.0.0.0/8` is split into `10.0.0.0/9` + `10.128.0.0/9`.
 - `11.0.0.0/8` is split into `11.0.0.0/9` + `11.128.0.0/9`.
 - `30.0.0.0/8` is split into `30.0.0.0/9` + `30.128.0.0/9`.
 - `100.64.0.0/10` is split into `100.64.0.0/11` + `100.96.0.0/11`.
 - `131.87.0.0/16` is split into `131.87.0.0/17` + `131.87.128.0/17`.
 - `172.16.0.0/12` is split into `172.16.0.0/13` + `172.24.0.0/13`.
 - `192.168.0.0/16` is split into `192.168.0.0/17` + `192.168.128.0/17`.
</dx-alert>


4. Configure IDC devices. You can click **Download configuration guide** to download related files and complete the configurations as instructed in the guide.
<table>
<tr>
<th width="20%">Parameter</th>
<th width="40%">Description</th>
<th width="40%">Remarks</th>
</tr>
<tr>
<td>CPE IP Range</td>
<td>Enter the customer IP range if **Static** is selected as the routing mode. This parameter cannot conflict with the VPC IP range in a non-NAT mode.</td>
<td>You can update the IP range later via “Change Tunnel” on the console.</td>
</tr>
</table>
5. Click **Submit**.

### Step 2: set the alarm recipient
After a dedicated tunnel is created, Tencent Cloud automatically configures four event alarms such as `DirectConnectTunnelDown`, `DirectConnectTunnelBFDDown`, `DirectConnectTunnelBGPSessionDown`, and `DirectConnectTunnelRouteTableOverload`, helping you monitor and manage your dedicated tunnels. For more information on the event alarms, please see the “Event Alarms” section in [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403).
This default alarm policy does not configure recipient information, so you can only view alarms on the console. To configure a recipient, take the following steps.
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and choose **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. In the upper-right corner of the **Alarm Policy** page, click **Advanced Filter** to select **All** for **Monitor Type** and **Dedicated Line channel** for **Policy type**.
3. Perform the following operations as needed.
 - Configure alarm objects
     1. Click the name of the target default policy in the “Alarm Policy” list.
     2. Click **Edit** next to **Alarm Object**, and select the objects to monitor. You can also click **Add Object** to create more alarm objects.
 - Modify an alarm policy
     1. Click the name of the target default policy in the “Alarm Policy” list.
     2. Click **Edit** next to the **Alarm Rule** and modify the trigger conditions for metric alarms and event alarms in the pop-up window. For more information on alarms, please see [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403). After the modification, click **Save**.
 - Set a default policy
     If the default alarm policy cannot meet your needs, you can select a custom alarm policy and click **Set to Default Policy** in the **Operation** column. Then the selected alarm policy will automatically apply to dedicated tunnels being created afterwards.

## Connection Status
After the dedicated tunnel is created, it will be displayed on the **Dedicated Tunnels** page in the **Applying** connection status.

The possible connection statuses of a dedicated channel include:
![](https://main.qcloudimg.com/raw/11b697a5399930b24682ab6e8387dde8.png)
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

