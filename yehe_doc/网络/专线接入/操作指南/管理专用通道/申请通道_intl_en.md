Dedicated tunnels are network linkage segmentation of a connection. You can create dedicated tunnels that connect to different direct connect gateways to enable communication between your local IDC and multiple VPCs. This document introduces how to apply for a dedicated tunnel.

<span id ="background"></span>

## Background

A new dedicated tunnel no longer supports the shared connection feature since August 1, 2020 00:00:00 (UTC+8). If you have enabled this feature on an existing dedicated tunnel, you can continue using it. However, if you delete the dedicated tunnel, you cannot enable this feature on a new dedicated tunnel after August 1, 2020 00:00:00.

## Use Limits on a Large IP Range

To ensure the fine-grained scheduling capability of your network, do not publish the following routes:
10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 100.64.0.0/10.
You can split the preceding extensive routes as follows for distribution:

- 10.0.0.0/8            
  split into 10.0.0.0/9 + 10.128.0.0/9.
- 172.16.0.0/12      
  split into 172.16.0.0/13 + 172.24.0.0/13.
- 192.168.0.0/16    
  split into 192.168.0.0/17 + 192.168.128.0/17.
- 100.64.0.0/10      
  split into 100.64.0.0/11 + 100.96.0.0/11.


## Direction

1. Log in to the [Direct Connect - Dedicated Tunnels](https://console.cloud.tencent.com/dc/dcConn) console.
2. On the **Dedicated Tunnels** page, click **+New** and complete the following configurations.
3. In the **Basic Configuration** tab, configure the name, connection type, access network, gateway region, and direct connect gateway.

<table>
	<thead>
	<tr>
	<th>Parameter</th>
	<th>Description</th>
	<th>Remarks</th>
	</tr>
	</thead>
	<tr>
	<td align="center" style="white-space:nowrap">Name</td>
	<td>Enter the name of your dedicated tunnel.</td>
	<td>-</td>
	</tr>
	<tr>
	<td align="center" style='white-space:nowrap'>Connection Type</td>
	<td>
	<ul>
	<li>Connections: a connection that is under your account.</li>
	<li>Shared Connections: a connection that is under another account. By using a shared connection, you do not share the bandwidth of the connection, but share the Tencent Cloud connection port, as tenants are isolated using the 802.1q VLANs technology.</li>
	</ul>
	</td>
	<td>If you want to enable the **Shared Connections** feature, take notice of the <a href="#background">background</a>, select **Shared Connections** in the **Basic Configuration** tab, and enter **Provider Account ID** and **Shared Connection ID**.</td>
	</tr>
	<tr>
	<td align="center" style='white-space:nowrap'>Access Network</td>
	<td>Select one from <a href="https://intl.cloud.tencent.com/document/product/215">VPC</a>, BM Network and <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a></td>
	<td>With CCN, you can connect to multiple VPCs through one dedicated tunnel.</td>
	</tr>
	<tr>
	<td>VPC/BM Network</td>
	<td>Select the network ID to which the dedicated tunnel will connect.</td>
	<td>Currently, BM network only supports standard direct connect gateways.</td>
	</tr>
	<tr>
	<td align="center" style='white-space:nowrap'>Gateway Region</td>
	<td>For **CCN**, gateway region is the CCN direct connect gateway region, which is the same as the public cloud region to which the connection access point belongs.</td>
	<td>For the shared connection mode, you need to ask the connection owner for information on the region of the connection access point.</td>
	</tr>
	<tr>
	<td align="center" style='white-space:nowrap'>Direct Connect Gateway</td>
	<td>VPC direct connect gateway and the VPC are in the same region. CCN direct connect gateway and the connection access point are in the same public cloud region.</td>
	<td>Currently, CCN direct connect gateways do not support the NAT feature.</td>
	</tr>
	</table>


4. In the **Advanced Configuration** tab, complete the following configurations.
 ![Advanced configuration](https://main.qcloudimg.com/raw/caf316d4dc39bfc7e193426b3970d931.png)

 <table>
 <thead>
 <tr>
 <th>Parameter</th>
 <th>Description</th>
 <th>Remarks</th>
 </tr>
 </thead>
 <tr>
 <td align="center" style='white-space:nowrap'>VLAN ID</td>
 <td>VLAN ID = 0: the connection does not enable subinterface and only one dedicated tunnel can be created.</td>
 <td>To enable a MSTP connection to pass through multiple VLANs, you need to enable the Trunk mode for your ISP line.</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>Bandwidth</td>
 <td>Bandwidth indicates the maximum rate, which can be changed later in "Change Tunnel". In the monthly 95th percentile billing mode, this parameter does not represent the billable bandwidth.</td>
 <td>-</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>Peer IP</td>
 <td>This IP can be user-defined or randomly assigned by Tencent Cloud. After submitting a ticket for tunnel creation, you can go to the details page of the tunnel to get the peer IP.<ul><li>"Cloud Peer IP" is the IPs for interconnection on Tencent Cloud.</li><li>"CPE Peer IP" is the IPs for interconnection on the user (or ISP) side, which must be manually configured.</li></ul></td>
 <td>If you choose to publish the peer IP to direct connect gateway, plan your IPs in advance to avoid any IP conflicts.</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>Routing Mode</td>
 <td>Select either **BGP** or **Static**.</td>
 <td>Tencent Cloud ASN: 45090</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>BGP ASN</td>
 <td>For **BGP**, this parameter is optional. Enter the AS number of the BGP neighbor on the CPE side, otherwise a random one will be assigned.</td>
 <td>-</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>BGP Key</td>
 <td>For **BGP**, this parameter is optional. Enter the MD5 of the BGP neighbor. The default value is “tencent". If this parameter is left empty, it indicates that no BGP key is required.</td>
 <td>-</td>
 </tr>
 </table>

5. Configure IDC devices:
    You can download the CPE configuration guide which provides common configuration methods.
![](https://main.qcloudimg.com/raw/f5480a8e21884a3bbf1cd38c109f23bc.png)
<table>
<thead><tr>
<th>Parameter</th>
<th>Description</th>
<th>Remarks</th>
</tr></thead>
<tr>
<td align="center" style='white-space:nowrap'>CPE IP Range</td>
<td>For **Static**, enter the IP range of the CPE. Note that it cannot conflict with the VPC IP range for non-NAT direct connect gateway.</td>
<td>You can update the IP range later in the "Change Tunnel" page on the console.</td>
</tr>
</table>

## Connection Status

A dedicated tunnel may have the following status:

- **Applying**
  The system has received your application for a new dedicated tunnel and is ready to start the creation.
- **Pending accepted**
  The connection owner is reviewing the application. Once the application is "accepted" to the connection owner, the dedicated tunnel can be created without Tencent Cloud’s approval.
- **Configuring**
  The system is delivering the configuration. If the status has been stuck at "Configuring" for a long time, the configuration delivery encountered a problem. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- **Configured**
  The system has completed the configuration based on the specified parameters, but has not been able to ping through your IDC. A dedicated tunnel in this status can be deleted.
- **Connected**
  The system pings to your IDC device successfully. However, this does not mean that your business is connected. Instead, you must go to the [route table](https://console.cloud.tencent.com/vpc/route?rid=1) of the VPC or CCN instance to complete the configuration and connection.
- **Deleting**
  The system is deleting your application. If the status has been stuck at "Deleting" for a long time, the system encountered a problem when deleting the configuration. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

