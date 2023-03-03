
[](id:01)
### What's the billing mode for VPN connections?
- VPN tunnels and customer gateways are free of charge, but VPN gateways are charged.
- VPN gateways can be billed in pay-as-you-go mode. You can choose the desired billing mode. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1037/32685).

For more information about VPC pricing, see [Purchase Guide](https://intl.cloudwww.tencentcloud.com/document/product/215/35500).

[](id:02)
### Why can't I renew or upgrade VPN gateways?
A VPN gateway cannot be renewed and upgraded at the same time. If you have an unpaid renewal or upgrade order, other renewal or upgrade operations cannot be performed. The system invalidates unpaid renewal or upgrade orders at 24:00 every day, after which you must re-submit your order.

[](id:03)
### Will I receive a reminder when my VPN gateway expires?
For more information, please see [Expiration Notifications](https://intl.cloud.tencent.com/document/product/1037/32687).


[](id:07)
### Is an SSL VPN gateway still charged after it is disconnected?
After an SSL VPN gateway is disconnected, the gateway is no longer charged by traffic. The VPN gateway instance fee and SSL connection fee are fixed and not affected by traffic. If you no longer need the VPN gateway instance and SSL connection, you can delete the resources to stop the charges.



[](id:08)
### Why is a VPN charged immediately after it is created?
The billing items vary based on the VPN product type:
- The billing items of an IPsec VPN include the gateway instance and public network traffic. A fixed fee is charged for the gateway instance.
- The billing items of an SSL VPN include the gateway instance, SSL connections, and public network traffic. Fixed fees are charged for the gateway instance and SSL connections, and the public network traffic is charged in pay-as-you-go mode.

For more information about billing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1037/32685).

[](id:09)
### Why is a pay-as-you-go VPN still charged after it is deleted?
A VPN connection is hourly postpaid in pay-as-you-go billing mode (billed hourly; time less than an hour is counted as an hour). If you use a connection during 12:02–13:20, fees will be incurred for two hours (12:00–13:00 and 13:00–14:00). In addition, the billing time in pay-as-you-go mode is not fixed and may be delayed; for example, fees for 13:00–14:00 may be billed after 14:00 or 15:00.

[](id:10)
### Are VPN tunnels and customer gateways charged?
VPN tunnels and customer gateways can be used for free.

[](id:11)
### Why am I unable to delete an overdue gateway?
You can delete an overdue gateway only after you delete the resources associated with the gateway.

[](id:12)
### If I use the SSL VPN from 8:00 to 12:00 in the morning, is the SSL VPN charged for other time periods?
If no traffic is generated, only the VPN gateway instance and SSL connections are charged.

[](id:13)
### How do I enable auto-renewal?
In the Tencent Cloud console, click <b>Fee</b> in the upper right corner, and click <b>Fee Management</b> in the left sidebar. On the <b>Auto-renewal</b> tab, enable auto-renewal for resources.

[](id:14)
### Why does the fee still be automatically deducted even when the VPN tunnel is not connected or has been deleted?
The outbound traffic of the VPN gateway will be charged. Delete the unused VPN gateway to avoid fee deduction.

[](id:15)
### Does Tencent Cloud VPN support bandwidth configuration adjustment?
- Currently, you can increase or decrease the bandwidth quota in the ranges of **5-100 Mbps** and **200-1000 Mbps**. The quota of monthly bandwidth can only be increased.
