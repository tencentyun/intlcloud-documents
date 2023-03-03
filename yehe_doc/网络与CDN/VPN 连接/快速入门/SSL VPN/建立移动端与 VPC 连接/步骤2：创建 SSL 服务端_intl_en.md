This document describes how to create an SSL VPN server on Tencent Cloud to provide SSL services for clients.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Select **VPN Connections** > **SSL VPN Server** in the left sidebar to enter the admin page.
3. Click **+New**.
4. Configure the following parameters in the pop-up window. 
<table>
<tr>
<th width="15%">Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Name</td>
<td>Enter the SSL VPN server name (up to 60 characters).</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the SSL VPN server.</td>
</tr>
<tr>
<td>VPN gateway</td>
<td>Select an existing VPN gateway.</td>
</tr>
<tr>
<td>Server IP range</td>
<td>Specify the IP range on Tencent Cloud that the mobile client can access, that is, the IP range of your VPC.</td>
</tr>
<tr>
<td>Client IP Range</td>
<td>Enter the IP range that is assigned to the mobile client for communication. The IP range must not conflict with the VPC CIDR block of Tencent or your local IP range.</td>
</tr>
<tr>
<td>Protocol</td>
<td>Transmission protocol of the server.</td>
</tr>
<tr>
<td>Port</td>
<td>Enter the SSL VPN server port used for data forwarding.</td>
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
<td>No.</td>
</tr>
<tr>
<td>Verification method</td>
<td><b>Certificate verification</b> and <b>Certificate verification+ Identity verification</b> are available. In this example, certificate verification is used.<ul><li>Certificate verification: In this verification method, the SSL VPN server can be accessed through all SSL VPN client connections by default.</li><li>Certificate verification + Identity verification: In this verification method, only connections that are allowed by the access control policy can be established. You can configure the access control policy for specific user groups or all users. If you select this option, you must select an EIAM application.</li></ul></td>
</tr>
</table>
5. Click **Create**.
