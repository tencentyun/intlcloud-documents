### How is a VPN gateway implemented? What about its availability?
- VPN gateway is implemented with software virtualization based on the redundancy provided by two VSR servers. A dual-server hot backup mechanism is used, which means when a server fails, another one takes over its work seamlessly, without affecting the operation of business.
- VPN tunnels run in the public network, therefore the congestion and jitter of the public network can affect the VPN network condition. If your business is sensitive to delay and jitter, it is recommended to connect to VPC via Direct Connect.

### What needs to be done when a VPN tunnel fails to establish a connection between its both ends?
A connection can be established successfully via a VPN tunnel only when the same negotiation information is configured for both ends. You need to check the consistency of configuration between two ends. For more information, see [What needs to be done when a VPN tunnel fails to establish a connection between its both ends?](/document/product/215/17010).

### How can I configure VPN?
IPsec VPN can be fully customized in the console. For more information, see [Getting Started](/document/product/215/4956#.E5.BF.AB.E9.80.9F.E5.85.A5.E9.97.A8).

### How can I create a VPN gateway?
You can create a VPN gateway in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Creating a VPN Gateway](/document/product/215/4956#.E5.BF.AB.E9.80.9F.E5.85.A5.E9.97.A8).

### How can I create a VPN tunnel?
You can create a VPN tunnel in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Creating a VPN Tunnel](/document/product/215/4956#.E5.BF.AB.E9.80.9F.E5.85.A5.E9.97.A8).

### How can I view VPN connection monitoring data?
You can view VPN connection monitoring data in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Viewing Monitoring Data](/document/product/215/4956#.E6.9F.A5.E7.9C.8B.E7.9B.91.E6.8E.A7.E6.95.B0.E6.8D.AE).

### How can I set VPN connection alarms?
You can set VPN connection alarms in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Setting Alarm](/document/product/215/4956#.E8.AE.BE.E7.BD.AE.E5.91.8A.E8.AD.A6).

### How can I view VPN gateway details?
You can view VPN gateway details in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Viewing VPN Gateway Details](/document/product/215/4956#.E6.9F.A5.E7.9C.8B-vpn-.E7.BD.91.E5.85.B3.E8.AF.A6.E7.BB.86.E4.BF.A1.E6.81.AF).

### How can I modify VPN tunnel configuration?
You can modify VPN tunnel configuration in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Modifying VPN Tunnel Configuration](/document/product/215/4956#.E4.BF.AE.E6.94.B9-vpn-.E9.80.9A.E9.81.93.E9.85.8D.E7.BD.AE).

### How can I enable gateway traffic control details?
You can enable gateway traffic control details in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Enabling Gateway Traffic Control Details](/document/product/215/4956#.E5.BC.80.E5.90.AF.E7.BD.91.E5.85.B3.E6.B5.81.E6.8E.A7.E6.98.8E.E7.BB.86).

### How can I set gateway traffic control details?
You can set gateway traffic control details in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Setting Gateway Traffic Control Details](/document/product/215/4956#.E8.AE.BE.E7.BD.AE.E7.BD.91.E5.85.B3.E6.B5.81.E6.8E.A7.E6.98.8E.E7.BB.86).

### How can I view gateway traffic control details?
You can view gateway traffic control details in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Viewing Gateway Traffic Control Details](/document/product/215/4956#.E6.9F.A5.E7.9C.8B.E7.BD.91.E5.85.B3.E6.B5.81.E6.8E.A7.E6.98.8E.E7.BB.86).

### How can I bind a high defense package?
You can bind a high defense package in [Tencent Cloud Console](https://console.cloud.tencent.com/). For more information, see [Binding a High Defense Package](/document/product/215/4956#.E7.BB.91.E5.AE.9A.E9.AB.98.E9.98.B2.E5.8C.85).

#### How can I allow users to manage VPN resources?
This policy allows the user to view all VPC resources, but only allows he/she to add, delete, modify, and query VPNs. For more information, see [FAQ for new users](/document/product/215/12248).




