This document describes how to create an SSL VPN server on Tencent Cloud side to provide SSL services for clients.


## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN Server** in the left directory to enter the admin page.
>? One VPN gateway supports only one SSL VPN server. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/1037/32682).
>
3. Click **+New**.
4. Configure the following parameters in the pop-up window.
<table>
<tr>
<th width="15%">Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Name</td>
<td>Enter the SSL VPN server name (up to 60 characters)</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the SSL VPN server</td>
</tr>
<tr>
<td>VPN gateway</td>
<td>Select an existing VPN gateway</td>
</tr>
<tr>
<td>Server IP range</td>
<td>Tencent Cloud IP ranges accessed by mobile clients.</td>
</tr>
<tr>
<td>Client IP Range</td>
<td>Enter the IP range assigned to the mobile client for communication. The IP range must not conflict with the VPC CIDR block of Tencent Cloud or your local IP range.</td>
</tr>
<tr>
<td>Protocol</td>
<td>Transmission protocol of the server</td>
</tr>
<tr>
<td>Port</td>
<td>Enter the SSL VPN server port used for data forwarding</td>
</tr>
<tr>
<td>Verification algorithm</td>
<td>Supported authentication algorithms: SHA1 and MD5.</td>
</tr>
<tr>
<td>Encryption algorithm</td>
<td>Supported encryption algorithms: AES-128-CBC, AES-192-CBC, and AES-256-CBC.</td>
</tr>
<tr>
<td>Compressed</td>
<td>No</td>
</tr>
<tr>
<td>Verification method</td>
<td><b>Certificate authentication</b> and <b>Certificate authentication + Identity authentication</b> are supported. In this example, <b>Certificate authentication</b> is used.<ul>
<li>Certificate authentication: The SSL VPN server can be accessed by SSL VPN clients.</li>
<li>Certificate authentication + Identity authentication: Only connections that comply with the access policies specified in the control policy are allowed. You can configure access policies for a specific user group or all users and select the corresponding Enterprise Identity and Access Management (EIAM) applications for an enabled policy.</li>
</ul></td>
</tr>
</table>
5. Click **Create**.
