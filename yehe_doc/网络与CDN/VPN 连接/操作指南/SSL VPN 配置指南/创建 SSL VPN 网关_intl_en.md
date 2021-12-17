An SSL VPN gateway works as the egress of an SSL VPN connection on the VPC side. It helps establish the secure and reliable encrypted network communication between Tencent Cloud VPC and mobile clients.

## Prerequisite
You’ve created a VPC. See [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805).

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Gateway** in the left directory to enter the admin page.
3. Click **+New**.
4. Configure the following gateway parameters in the pop-up window.
![]()
<table>
<tr>
<th width="12%">Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Gateway Name</td>
<td>Enter the VPN gateway name (up to 60 characters)</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the VPN gateway</td>
</tr>
<tr>
<td>Protocol Type</td>
<td>Select **SSL**</td>
</tr>
<tr>
<td>SSL VPN Connections</td>
<td>Number of SSL VPN connections on the mobile clients</td>
</tr>
<tr>
<td>Associated Network</td>
<td>Select **VPC**</td>
</tr>
<tr>
<td>Network</td>
<td>Select the VPC associated with the VPN gateway</td>
</tr>
<tr>
<td>Bandwidth Cap</td>
<td>Set a reasonable bandwidth cap for the VPN gateway according to the actual application scenarios</td>
</tr>
</table>
5. Click **Create**
![]()
