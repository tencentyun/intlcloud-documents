After creating the SSL VPN gateway and server, you need to create an SSL VPN client certificate on Tencent Cloud. This certificate records the information about the SSL certificate assigned by Tencent Cloud to the client, and is used for mutual authentication between the server and the mobile client. You can download the certificate to the mobile terminal and use it to communicate with Tencent Cloud through OpenVPN.


## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **SSL VPN Client** in the left directory to enter the admin page.
3. Click **New**.
4. Configure the following parameters in the pop-up window.
![]()
<table>
<tr>
<th width="12%">Parameter</th>
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
<td>SSL VPN Server</td>
<td>Select an existing SSL VPN server.</td>
</tr>
</table>
5. Click **Create** after configuring the SSL VPN client parameters. When the **Certificate Status** becomes **Available**, the creation is completed.
![]()


