Dedicated tunnels are network link segmentation of a connection. You can create dedicated tunnels that connect to different direct connect gateways to enable communication between your on-premises IDC and multiple VPCs. This document describes how to apply for a dedicated tunnel. After a dedicated tunnel is created, its event alarms will be automatically configured to facilitate your monitoring and OPS.
<span id ="background"></span>

> ?The shared connection feature of new dedicated tunnels has stopped accepting new applications since August 1, 2020 at 00:00:00. If you are using a shared connection, it will not be affected by this change, but if you delete it, you will not be able to apply for new dedicated tunnels with shared connection after August 1, 2020 at 00:00:00.
> 

## Prerequisites
- You have applied for a connection as instructed in [Applying for a Connection](https://intl.cloud.tencent.com/document/product/216/19244).
- You have created a direct connect gateway as instructed in [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).

## Directions

### Step 1: apply for a dedicated tunnel

1. Log in to the [Direct Connect - Dedicated Tunnel](https://console.cloud.tencent.com/dc/dcConn) console.
2. Click **+New** at the top of the **Dedicated Tunnel** page, complete the basic configurations such as name, connection type, access network, region and associated direct connect gateway, and click **Next**.
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
    <td>Connection</td>
    <td>Select a connection you have applied for.</td>
    </tr>
     <tr>
    <td>Access Network</td>
    <td>Select from CCN, VPC and BM Network.</td>
    </tr>
     <tr>
    <td>Region</td>
    <td>Select the region of the VPC or BM VPC or the region where the CCN-based direct connect gateway resides.</td>
    </tr>
     <tr>
    <td>Virtual Private Cloud</td>
    <td>Select the VPC or BM network instance to be connected to by the dedicated tunnel.</td>
    </tr>
     <tr>
    <td>Direct Connect Gateway</td>
    <td>Associate an existing direct connect gateway with the dedicated tunnel.</td>
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
<td>A VLAN represents a tunnel. Enter a value in the range of 0-3000. Entering “0” means one dedicated tunnel can be created. MSTP connection passthrough to multiple VLANs requires the carrier's line to enable the Trunk mode.</td>
</tr>
<tr>
<td>Bandwidth</td>
<td>Bandwidth is the bandwidth cap, which can be changed later in "Change Tunnel". If the billing mode is pay-as-you-go by monthly 95th percentile, this parameter does not mean the billable bandwidth.</td>
</tr>
<tr>
<td>Tencent Cloud Primary Edge IP</td>
<td>Enter the connection secondary IP address on the Tencent Cloud side.</td>
</tr>
<tr>
<td>Tencent Cloud Backup Edge IP</td>
<td>Enter the connection secondary IP address on the Tencent Cloud side.</td>
</tr>
<tr>
<td>CPE Peer IP</td>
<td>Configure the connection IP on the user (or carrier) side.</td>
</tr>
</tr>
<tr>
<td>Routing Mode</td>
<td>Select <b>BGP</b> or <b>Static</b>.<br><ul><li>BGP: applies to the exchange of routing information and network accessibility across autonomous systems (AS).</li><li>Static: applies to a simper network environment.</li></ul></td>
</tr>
</tr>
<tr>
<td>BGP ASN</td>
<td>Enter the BGP neighbor AS number on the CPE side. Note that 45090 is Tencent Cloud ASN. If this field is left empty, a random ASN will be assigned.</td>
</tr>
</tr>
<tr>
<td>BGP Key</td>
<td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain special characters such as ?, &, space, ", \, and +.</td>
</tr>
</tr>
<tr>
<td>CPE IP Range</td>
<td>Enter the IP ranges of your IDC, with one IP range per line.</td>
</tr>
</table>

> ?When configuring a IP range route, do not directly publish the following routes: `9.0.0.0/8`, `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12` and `192.168.0.0/16`. Instead, you need to first split them.
>
> - `9.0.0.0/8` should be split into `9.0.0.0/9` + `9.128.0.0/9`.
> - `10.0.0.0/8` should be split into `10.0.0.0/9` + `10.128.0.0/9`.
> - `172.16.0.0/12` should be split into `172.16.0.0/13` + `172.24.0.0/13`.
> - `192.168.0.0/16` should be split into `192.168.0.0/17` + `192.168.128.0/17`.
> - `100.64.0.0/10` should be split into `100.64.0.0/11` + `100.96.0.0/11`.
> - `131.87.0.0/16` should be split into `131.87.0.0/17` + `131.87.128.0/17`.
> - `172.16.0.0/12` should be split into `172.16.0.0/13` + `172.24.0.0/13`.
> - `192.168.0.0/16` should be split into `192.168.0.0/17` + `192.168.128.0/17`.

4. Configure IDC devices.
   You can download the CPE configuration guide for your devices, which provides several common configuration guidelines.
<table>
<tr>
<th width="20%">Parameter</th>
<th width="40%">Description</th>
<th width="40%">Remarks</th>
</tr>
<tr>
<td>CPE IP Range</td>
<td>Enter the customer IP range if <b>Static</b> is selected for the <b>Routing Mode</b>. This parameter cannot conflict with VPC IP range in a non-NAT mode.</td>
<td>You can update the IP range via <b>Change Tunnel</b> in the console.</td>
</tr>
</table>
5. Click **Submit**.

### Step 2: set the alarm recipient
After a dedicated tunnel is created, Tencent Cloud automatically configures four event alarms such as `DirectConnectTunnelDown`, `DirectConnectTunnelBFDDown`, `DirectConnectTunnelRouteTableOverload`, and `DirectConnectTunnelBFDDown`, helping you monitor and manage your dedicated tunnels. For more information on the event alarms, please see the “Event Alarms” section in [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403).

This default alarm policy is not provided with a recipient, so you can only view alarms in the console Message Center. To configure a recipient, perform the following steps.
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and select **Alarm Configuration** > **Alarm Policy** in the left side bar.
2. Select **Dedicated Line channel** for the **Product Type** in the top right of the **Alarm Policy** page.
3. Perform the following operations as needed.
   - Configure alarm recipient objects
    1. Click the name of the target default policy in the alarm policy list.
    2. Click **Edit** under the **Alarm Recipient Object** and select object from the list in the pop-up window. You can also click **Add Recipient Group** to configure new user groups.
   - Modify an alarm policy
    1. Click the name of the target default policy in the alarm policy list.
    2. Click **Edit** next to the **Hit Condition** and modify the trigger conditions in the pop-up window. For more information on the event alarm, please see the “Event Alarms” section in [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403). After completing the modification, click **Save**.
   - Set a default policy
     If the default alarm policy cannot meet your needs, you can select a custom alarm policy and click **Set Default** under the **Policy Type** column. Then the selected alarm policy will automatically apply to dedicated tunnels being created afterwards.
  
## Connection Status
After the dedicated tunnel is created, it will be displayed on the **Dedicated Tunnels** page in the **Applying** connection status.
The possible connection statuses of a dedicated channel include the following:
- **Applying**
  The system has received your application for a new dedicated tunnel and is ready to start the creation.
- **Configuring**
  The system is delivering the configuration. If this status lasts for a long time, there may be an exception. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- **Configured**
  The system has completed the configuration based on the specified parameters, but has not been able to ping through the IP address of your IDC. A dedicated tunnel in this status can be deleted.
- **Connected**
  The system pings to your IDC device successfully. However, this does not mean that your business is connected. You have to configure the [route table](https://console.cloud.tencent.com/vpc/route?rid=1) of the VPC or CCN instance to implement the connection.
- **Deleting**
  If you delete your dedicated tunnel in the console, the connection status of the dedicated tunnel becomes **Deleting**. If this status lasts for a long time, there may be an exception. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
