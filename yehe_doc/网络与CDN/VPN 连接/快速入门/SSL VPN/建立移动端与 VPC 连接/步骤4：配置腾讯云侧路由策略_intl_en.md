This document describes how to configure the routing and forwarding policies for the mobile client to access Tencent Cloud VPC.


## Directions
1. Log in to the [VPC console] (https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Route Tables** on the left sidebar to enter the admin page.
3. Click **+New**.
4. Configure the following parameters in the pop-up window.
![]()
<table>
<tr>
<th width="12%">Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Destination</td>
<td>Enter the mobile client IP range</td>
</tr>
<tr>
<td>Next Hop Type</td>
<td>Select **VPN Gateway**</td>
</tr>
<tr>
<td>Next Hop</td>
<td>Select an existing VPN gateway</td>
</tr>
</table>
5. Click **Create**.
![]()
