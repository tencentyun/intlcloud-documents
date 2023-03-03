An SSL VPN gateway is an egress gateway for VPC to establish an SSL VPN connection. It is used with an SSL VPN client (on mobile devices) to establish an encrypted communication between a Tencent Cloud VPC and a mobile client.


## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Select **VPN Connections** > **VPN Gateway** in the left sidebar to enter the admin page.
3. Click **+New**.
4. Configure the following gateway parameters in the pop-up window. 
<table>
<tr>
<th width="12%">Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Gateway name</td>
<td>Enter the VPN gateway name (up to 60 characters).</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the VPN gateway.</td>
</tr>
<tr>
<td>AZ</td>
<td>Select the availability zone.</td>
</tr>
<tr>
<td>Protocol Type</td>
<td>Select <b>SSL</b>.</td>
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Set a reasonable bandwidth cap for the VPN gateway according to the actual application scenarios.</td>
</tr>
<tr>
<td>Associated Network</td>
<td>Select the network type for accessing resources in the cloud. VPC is used as an example here.</td>
</tr>
<tr>
<td>Network</td>
<td>Select the VPC associated with the VPN gateway.</td>
</tr>
<tr>
<td>SSL VPN Connections</td>
<td>Set the number of SSL VPN connections on the mobile clients.
<dx-alert infotype="explain" title="">
This number indicates the maximum number of clients allowed for simultaneous connection, that is, the maximum number of clients that the gateway can be associated with. After the gateway is created, this parameter cannot be modified. Therefore, set this parameter with caution.
</dx-alert>
</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>Bill-by-traffic is used by default.</td>
</tr>
</table>


5. Click **Create**.
