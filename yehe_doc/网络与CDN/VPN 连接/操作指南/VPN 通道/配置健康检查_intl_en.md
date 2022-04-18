This document introduces how to configure health check for a VPN tunnel to ensure high business availability.

## How Health Check Works
Set up a tunnel between the VPN gateway and the on-premises gateway by specifying their IPs. The IP of VPN gateway can not be within the VPC IP range, and the IP of the on-premises gateway do not overlap with the VPN gateway IP. If the two IPs are interconnected, the VPN tunnel is healthy; if they are not, the VPN tunnel is unhealthy, and the traffic will be forwarded to a standby line.

## Prerequisites
- You have created a VPN gateway on Tencent Cloud as instructed in [Creating VPN Gateways](https://intl.cloud.tencent.com/document/product/1037/39688) and configure the on-premises gateway as instructed in [Adding Customer Gateways](https://intl.cloud.tencent.com/document/product/1037/39691).
- The IP range of the VPN gateway and on-premises gateway don't overlap.
- The customer gateway is configured with a static public IP.

## Configuring the Health Checks When Creating VPN Tunnels
This section only introduces the parameters for health checks. For information about creating a VPN tunnel, see [Creating a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/39635).
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** in the left sidebar.
3. In the **VPN Connections** page, click **+New**.
4. In the pop-up window, enable Health Check and configure the IPs for health check.
![]()
<table>
<tr>
<th width="20%">Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>VPN gateway IP for health check</td>
<td>It defaults to an IP within the range of `169.254.128.0/17`. You can also specify `0.0.0.0` or an IP within `224.0.0.0-239.255.255.255` but outside the VPC IP range.</td>
</tr>
<tr>
<td>Customer gateway IP for health check</td>
<td>It defaults to an IP within the range of `169.254.128.0/17`. You can also specify an available on-premises IP.</td>
</tr>
</table>
5. Click **Next** to configure the SPD policy for the health check.
Besides the SPD policies for the two sides of VPN tunnel, you also need to configure an SPN policy to check whether the IPs for health check on the two sides can communicate.
 ![]()
6. The health check configuration takes effect upon the tunnel creation. 

## Configuring the Health Check After Creating VPN Tunnels
You can also configure the health check on the VPN tunnel details page after the tunnel is created.
>? Note that your business may be interrupted for a short time. 
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** in the left sidebar.
3. In the **VPN Tunnels** page, locate and click the target VPN tunnel to , and click **Edit** on the **Basic Information** tab.
![]()
4. Enable the health check and configure the relevant parameters.
<table>
<tr>
<th width="20%">Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>VPN gateway IP for health check</td>
<td>It defaults to an IP within the range of `169.254.128.0/17`. You can also specify `0.0.0.0` or an IP within `224.0.0.0-239.255.255.255` but outside the VPC IP range.</td>
</tr>
<tr>
<td>Customer gateway IP for health check</td>
<td>It defaults to an IP within the range of `169.254.128.0/17`. You can also specify an available on-premises IP.</td>
</tr>
</table>
5. Click **Edit** in the **SPD Policy** section, and configure the SPD policy for health check.
![]()
6. Click **Save**.
