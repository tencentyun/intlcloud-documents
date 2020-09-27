Dedicated tunnels are network link segmentation of a connection. You can create dedicated tunnels that connect to different Direct Connect gateways to enable communication between your on-premises IDC and multiple VPCs. This document describes how to apply for a dedicated tunnel.

<span id ="background"></span>

## Background

The shared connection feature of new dedicated tunnels has stopped accepting new applications at 00:00, August 1, 2020. If you are using a shared connection, it will not be affected by this change, but if you delete it, you will not be able to apply for new dedicated tunnels with shared connection after 00:00, August 1, 2020.

## Use Limits on Large IP Range

To ensure the fine-grained scheduling capability of your network, do not publish the following routes:
9.0.0.0/8, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16,  100.64.0.0/10, 131.87.0.0/16, 172.16.0.0/12, 192.168.0.0/16.
>!If a large IP range route is published, the direct connect gateway will directly reject it.

 You can split the above routes as follows for distribution:
- 9.0.0.0/8
should be split into `9.0.0.0/9` + `9.128.0.0/9`.
- 10.0.0.0/8            
should be split into `10.0.0.0/9` + `10.128.0.0/9`.
- 172.16.0.0/12      
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
- 192.168.0.0/16    
should be split into `192.168.0.0/17` + `192.168.128.0/17`.
- 100.64.0.0/10      
should be split into `100.64.0.0/11` + `100.96.0.0/11`.
- 131.87.0.0/16      
should be split into `131.87.0.0/17` + `131.87.128.0/17`.
- 172.16.0.0/12      
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
- 192.168.0.0/16      
should be split into `192.168.0.0/17` + `192.168.128.0/17`.

## Directions

1. Log in to the [Direct Connect - Dedicated Tunnel](https://console.cloud.tencent.com/dc/dcConn) Console.
2. Click **+Create** at the top of the "Dedicated Tunnel" page and configure the following information.
3. Configure the basic items, such as name, connection type, access network, region, and associated Direct Connect gateway.

<table>
	<thead>
	<tr>
	<th>Parameter</th>
	<th>Description</th>
	<th>Remarks</th>
	</tr>
	</thead>
	<tr>
	<td align="center" style="white-space:nowrap">Dedicated tunnel name</td>
	<td>Enter your dedicated tunnel name.</td>
	<td>-</td>
	</tr>
	<tr>
	<td align="center" style='white-space:nowrap'>Connection type</td>
	<td>
	<ul>
	<li>My connection: a connection that uses the current account</li>
	<li>Shared connection: a connection that uses another account. A shared connection does not mean sharing the bandwidth of a connection; instead, it means sharing Tencent Cloud connection ports, and different tenants are isolated from each other through the 802.1Q VLANs technology. </li>
	</ul>
	</td>
	<td>To use the shared connection feature, please see <a href="#background">Background</a>. Then, select **Shared Connection** on the "Basic Information" page and configure the connection provider's account, connection ID, and other information. </td>
	</tr>
	<tr>
	<td align="center" style='white-space:nowrap'>Access network</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/215">VPC</a>, BM VPC, and <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a> are supported.</td>
	<td>CCN: it enables connection to multiple VPCs through one tunnel.</td>
	</tr>
	<tr>
	<td>VPC/BM VPC</td>
	<td>Select the ID of the network instance to be connected to by the dedicated tunnel.</td>
	<td>BM VPC currently supports only Standard Direct Connect gateways.</td>
	</tr>
	<tr>
	<td align="center" style='white-space:nowrap'>Gateway region</td>
	<td>If **CCN** is selected as the access network, this parameter means the CCN-based Direct Connect gateway region, which is the same as the public cloud region where the connection access point is located. </td>
	<td>For the shared connection mode, you need to get the connection access point region information from the connection owner.</td>
	</tr>
	<tr>
	<td align="center" style='white-space:nowrap'>Direct Connect gateway</td>
	<td>The VPC-based Direct Connect gateway region is the same as the VPC region, while the CCN-based Direct Connect gateway region is the same as the public cloud region where the connection access point is located.</td>
	<td>CCN-based Direct Connect gateways currently don't support the NAT feature.</td>
	</tr>
	</table>


4. Configure the following parameters on the "Advanced Configuration" page.


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
 <td>If VLAN ID is 0, it means that this connection does not enable subinterfaces; therefore, only one tunnel can be created.</td>
 <td>MSTP connection passthrough to multiple VLANs requires the ISP's line to enable the Trunk mode.</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>Bandwidth</td>
 <td>Bandwidth is the maximum rate, which can be changed later in "Tunnel Change". With postpaid monthly 95th percentile billing mode, the "bandwidth" parameter does not represent the billable bandwidth.</td>
 <td>-</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>IP</td>
 <td>This IP can be customized by you or provided randomly by Tencent Cloud. You can get the randomly assigned IP address in tunnel details after your application is submitted. <ul><li>"Tencent Cloud perimeter IP" is the perimeter IP at the Tencent Cloud side of the connection. </li><li>"User perimeter IP" is the IP at the user (or ISP) side of the connection, which you must configure on your own.</li></ul></td>
 <td>If you choose to publish the IP to the Direct Connect gateway, please plan IP segmentation well to avoid IP conflicts.</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>Routing method</td>
 <td>BGP routing and static routing are supported.</td>
 <td>Tencent Cloud ASN: 45090.</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>BGP ASN</td>
 <td>For **BGP routing**, this parameter is optional. Enter the BGP neighbor AS number at the CPE side. If it is left empty, the number will be assigned by the system randomly.</td>
 <td>-</td>
 </tr>
 <tr>
 <td align="center" style='white-space:nowrap'>BGP key</td>
 <td>For **BGP routing**, this parameter is optional. Enter the MD5 value of the BGP neighbor, which is "tencent" by default. If it is left empty, it means that no BGP key is required. It cannot contain ?, &, space, ", \, and +.</td>
 <td>-</td>
 </tr>
 </table>

5. Configure IDC devices.
    You can download the CPE configuration guide, which provides the configuration methods for several common vendors.

<table>
<thead><tr>
<th>Parameter</th>
<th>Description</th>
<th>Remarks</th>
</tr></thead>
<tr>
<td align="center" style='white-space:nowrap'>User IDC IP range</td>
<td>For **static routing**, enter your CPE IP range, which should not conflict with the VPC IP range if not in NAT mode.</td>
<td>Change is supported: you can update the IP range in "Tunnel Change" in the console subsequently.</td>
</tr>
</table>

## Connection Status

The possible statuses of a dedicated tunnel include the following:

- **Applying**
  The system has received your directive to apply for a new dedicated tunnel and is ready to start a creation task.
- **Pending approval**
  The connection owner is reviewing the application. Once the application is "approved" by the connection owner, the dedicated tunnel can be created without Tencent Cloud approval.
- **Configuring**
  The system is delivering the configuration. If the status has been stuck at "Configuring" for a prolonged time, the configuration delivery might run into a problem. Please contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- **Configured**
  The system has completed the configuration based on the parameters you provided but has not been able to ping the IP address of your IDC. Deletions can be performed in this status.
- **Connected**
  The system is able to ping the IP address of your IDC device. However, this does not mean that your business is connected. You must go to VPC or CCN [route table](https://console.cloud.tencent.com/vpc/route?rid=1) to complete the configuration and connection.
- **Deleting**
  The system is deleting your application. If the status has been stuck at "Deleting" for a prolonged time, the system is having a problem with deleting the configuration. Please contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

