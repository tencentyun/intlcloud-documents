
[](id:01)
### What's the billing mode for VPN connections?
- VPN tunnels and customer gateways are free of charge, but VPN gateways are charged.
- VPN gateways can be billed in pay-as-you-go mode. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1037/32685).

For more information about VPC pricing, see [Purchase Guide](https://www.tencentcloud.com/document/product/215/35500).

[](id:02)
### Why can't I renew or upgrade VPN gateways?
A VPN gateway cannot be renewed and upgraded at the same time. If you have an unpaid renewal or upgrade order, other renewal or upgrade operations cannot be performed. The system invalidates unpaid renewal or upgrade orders at 24:00 every day, after which you must re-submit your order.

[](id:03)
### Will I receive a reminder when my VPN gateway expires?
For more information, please see [Expiration Notifications](https://intl.cloud.tencent.com/document/product/1037/32687).

[](id:07)
### Is an SSL VPN connection still charged after it is terminated?
After an SSL VPN connection is terminated, no traffic fees will be incurred. However, the VPN gateway instance fee and SSL connection fee are fixed and will also be charged. Please delete any resources that you no longer need in time.



[](id:08)
### Why is a VPN connection charged immediately after it is created?
The billing items vary based on the VPN product type:
- The billing items of IPsec VPN include the gateway instance and public network traffic. A fixed fee is charged for the gateway instance.
- The billing items of SSL VPN include the gateway instance, SSL connections, and public network traffic. Fixed fees are charged for the gateway instance and SSL connections, and the public network traffic is charged in pay-as-you-go mode.

For more information about billing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1037/32685).

[](id:09)
### Why is a pay-as-you-go VPN connection still charged after it is deleted?
A VPN connection is hourly postpaid in pay-as-you-go billing mode (billed hourly; time less than an hour is counted as an hour). If you use a connection during 12:02–13:20, fees will be incurred for two hours (12:00–13:00 and 13:00–14:00). In addition, the billing time in pay-as-you-go mode is not fixed and may be delayed; for example, fees for 13:00–14:00 may be billed after 14:00 or 15:00.

[](id:10)
### Do I need to pay for VPN tunnels and customer gateways?
VPN tunnels and customer gateways can be used for free.

[](id:11)
### Why cannot I delete an overdue gateway?
You can delete an overdue gateway only after you delete the resources associated with the gateway.

[](id:12)
### If I use an SSL VPN connection only from 8:00 to 12:00 in the morning, is the connection charged for other time periods?
In time periods with no traffic, only the VPN gateway instance fee and the SSL connection fee are charged.

[](id:13)
### How do I enable auto-renewal?
In the Tencent Cloud console, click **Cost** in the upper right corner, and click **Renewal management** in the left sidebar. On the **Auto Renewal** tab, enable auto-renewal for required resources.

[](id:14)
### Why does the fee still be automatically deducted even when the VPN tunnel is not connected or has been deleted?
The outbound traffic of the VPN gateway will be charged. Delete the unused VPN gateway to avoid fee deduction.

[](id:15)
### Can I upgrade or downgrade my VPN gateway configurations?
- In terms of quota, the VPN gateway bandwidth can only be adjusted in specific bandwidth ranges. Please properly plan the bandwidth for your business.
  - Pay-as-you-go: The VPN gateway bandwidth can only be adjusted in the current bandwidth range ([5 Mbps, 100 Mbps] or [200 Mbps, 1000 Mbps]). Cross-range adjustment is not supported.
  - The bandwidth of 1000 Mbps SSL VPN gateways and 3000 Mbps IPsec VPN gateways cannot be downgraded. Please properly plan the bandwidth for your business.

