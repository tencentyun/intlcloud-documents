This document describes how to publish the IP range to CCN for connecting the VPN to the CCN.
>?If the communication mode of the VPN tunnel is "destination route", then you don't need to publish the IDC IP range to the CCN.
>

## Prerequisites
- You have created a CCN-based IPsec VPN gateway as instructed in [Creating VPN Gateways](https://intl.cloud.tencent.com/document/product/1037/39688) and bound it to a CCN instance as instructed in [Associating a CCN Instance](https://intl.cloud.tencent.com/document/product/1037/46429).
- You've configured a SPD policy for the VPN tunnel. For more information, see [Creating VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/39635)

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **VPN Gateway** in the left directory to enter the admin page.
3. Click the ID of the target VPN gateway to go to the details page.
![]()
4. Public the IP range to the CCN in the **Publish IP Range** tab.
![]()
The IP range here is the IP range of the customer gateway in configuring the SPD policy for the VPN tunnel.