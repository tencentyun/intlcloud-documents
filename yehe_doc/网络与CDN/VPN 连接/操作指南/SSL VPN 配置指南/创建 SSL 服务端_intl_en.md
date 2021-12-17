This document describes how to create an SSL VPN server on Tencent Cloud side to provide SSL services for clients.


## Directions
1. Log in to the [VPC console] (https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN Server** in the left directory to enter the admin page.
3. Click **+New**.
4. Configure the following parameters in the pop-up window.
<img src="" width="70%">
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
<td>Displays the region of the SSL VPN server</td>
</tr>
<tr>
<td>VPN Gateway</td>
<td>Select an existing VPN gateway</td>
</tr>
<tr>
<td>Server IP range</td>
<td>Tencent Cloud IP ranges accessed by mobile clients.</td>
</tr>
<tr>
<td>Client IP Range</td>
<td>Enter the IP range assigned to the mobile client for communication. The IP range shall not conflict with the VPC CIDR block of Tencent.</td>
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
<td>Authentication Algorithm</td>
<td>Supported authentication algorithms: SHA1 and MD5.</td>
</tr>
<tr>
<td>Encryption Algorithm</td>
<td>Supported encryption algorithms: AES-128-CBC, AES-192-CBC, and AES-256-CBC.</td>
</tr>
<tr>
<td>Compressed</td>
<td>No</td>
</tr>
</table>
5. Click **Create**.
![]()
