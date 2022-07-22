Dear Tencent Cloud user,

From 00:00 on April 20, 2022 (UTC +8), for new NAT Gateway users, the EIP bandwidth cap will no longer be automatically adjusted when the following operations are performed:
- Bind a NAT gateway to an EIP in the Public IP console.
- Bind an EIP to a NAT gateway in the NAT Gateway console.
>? For information on the corresponding EIP bandwidth caps, see details displayed in the console.
>

The outbound traffic going to the public network is limited by both the bandwidth cap of the NAT gateway and that of the EIP. The lower one prevails. You can set a reasonable bandwidth cap for the NAT gateway and EIP according to your actual needs.
- **Adjust before binding**: You can set a reasonable bandwidth cap for the EIP to be bound to the NAT gateway in the public IP console. For details, see [Elastic IP](https://intl.cloud.tencent.com/document/product/213/16586#.E8.B0.83.E6.95.B4.E5.B8.A6.E5.AE.BD).
- **Adjust after binding**: You can adjust the bandwidth cap for the EIP bound to the NAT gateway in the NAT Gateway console. For details, see [Managing EIPs of NAT Gateway](https://intl.cloud.tencent.com/document/product/1015/30240).
- **Adjust during binding**: You can adjust the bandwidth cap on the purchase page of the NAT Gateway console. For details, see [Purchase Method](https://intl.cloud.tencent.com/document/product/1015/30249).
>? The purchase page is in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.


Thank you for your support.
Regards, 
Tencent Cloud Team
