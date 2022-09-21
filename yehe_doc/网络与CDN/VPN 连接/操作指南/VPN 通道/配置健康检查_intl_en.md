Tencent Cloud VPN Connections provides a complete solution to guarantee the high availability of your business. Not only the VPN gateway itself supports a high availability, but also primary/secondary tunnels are supported. The VPN gateway uses health check to identify the tunnel status and triggers the traffic switch between the primary and secondary tunnels based on their status. This document describes how to configure health check.
>?We recommend you use a route-based tunnel for health check. If you use an SPD policy-based tunnel, you need to configure an SPD policy for `0.0.0.0/0`.
>

## How health check works
VPN tunnel health check uses the NQA mechanism and the `ping` command by default. In this way, the VPN gateway regularly uses the local address of health check to ping (encrypted in the tunnel) the peer address, so as to determine the connectivity. If the ping fails multiple times in a row, the VPN gateway will consider the tunnel as abnormal and switch the traffic from the primary tunnel to the secondary tunnel. At the same time, the customer gateway also needs to implement a similar mechanism to switch the traffic to the secondary tunnel. To this end, you need to configure two IP addresses that are mutually pingable in the tunnel or adopt such two IP addresses automatically assigned by the system for health check. The IP ranges of the two addresses cannot conflict with those of the VPC and IDC. 

## Prerequisites
- You have [created a VPN gateway](https://intl.cloud.tencent.com/document/product/1037/39688) and [configured the customer gateway](https://intl.cloud.tencent.com/document/product/1037/39691), and the VPN gateway is on v3.0 or later.
- You have created the primary and secondary tunnels.
- You have planned health check addresses or use the addresses automatically assigned by the system.

## Option 1. Configure the health check when creating a VPN tunnel
This section only introduces the parameters for health check. For information on how to create a VPN tunnel, see [Creating VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/39635).
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** on the left sidebar.
3. In the **VPN Connections** page, click **Create**.
4. In the pop-up window, enable Health Check and configure the IPs for health check.
![]()
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>VPN gateway IP for health check</td>
<td>It defaults to an IP within the range of `169.254.128.0/17`. You can also specify `0.0.0.0` or an IP within `224.0.0.0`–`239.255.255.255` but outside the VPC IP range.</td>
</tr>
<tr>
<td>Customer gateway IP for health check</td>
<td>It defaults to an IP within the range of `169.254.128.0/17`. You can also specify an available on-premises IP.</td>
</tr>
</table>
5. Click **Next**. We recommend you select **Destination route** for the communication mode. If **Destination route** is unavailable, we recommend you enter `0.0.0.0/0` for the local and peer IP ranges in the SPD policy to ensure that the communication between the local and peer health check IPs is encrypted based on the VPN tunnel.
6. The health check configuration takes effect upon the tunnel creation.

## Option 2. Configure the health check after creating a VPN tunnel
You can also configure the health check on the VPN tunnel details page after the tunnel is created.
>? Note that your business may be interrupted for a short time.
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** on the left sidebar.
3. In the **VPN Tunnels** page, locate and click the target VPN tunnel, and click **Edit** on the **Basic Information** tab.
![]()
4. Enable the health check and configure the relevant parameters.
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>VPN gateway IP for health check</td>
<td>It defaults to an IP within the range of `169.254.128.0/17`. You can also specify `0.0.0.0` or an IP within `224.0.0.0`–`239.255.255.255` but outside the VPC IP range.</td>
</tr>
<tr>
<td>Customer gateway IP for health check</td>
<td>It defaults to an IP within the range of `169.254.128.0/17`. You can also specify an available on-premises IP.</td>
</tr>
</table>
5. We recommend you select **Destination route** for the communication mode. If **Destination Route** is unavailable, we recommend you enter `0.0.0.0/0` for the local and peer IP ranges in the SPD policy to ensure that the communication between the local and peer health check IPs is encrypted based on the VPN tunnel.
6. Click **Save**.
