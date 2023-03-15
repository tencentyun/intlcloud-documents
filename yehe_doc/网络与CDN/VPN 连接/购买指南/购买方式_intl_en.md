This document describes how to purchase the VPN service.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **VPN Gateway** in the left sidebar to enter the admin page.
3. Select a region and VPC, and then click **+New**.
<img src="" width="50%">
4. Configure the following parameters in the pop-up dialog box, and click **Create**.
>?The bandwidth of a VPN gateway can be adjusted only in specific bandwidth ranges. Please properly plan the bandwidth for your business.
>  - Pay-as-you-go: The VPN gateway bandwidth can only be adjusted in the current bandwidth range ([5 Mbps, 100 Mbps] or [200 Mbps, 1000 Mbps]). Cross-range adjustment is not supported.
>  - The bandwidth of 1000 Mbps SSL VPN gateways and 3000 Mbps IPsec VPN gateways cannot be downgraded.
> 
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Gateway name</td>
<td>Enter the VPN gateway name (up to 60 characters).</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region where the selected VPN resources reside.</td>
</tr>
<tr>
<td>AZ</td>
<td>Select the availability zone where your resources reside.</td>
</tr>
<tr>
<td>Protocol Type</td>
<td>IPsec and SSL protocols are supported.</td>
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Select the gateway bandwidth based on your needs.</td>
</tr>
<tr>
<td>Network</td>
<td>CCN and VPC are supported. Select CCN if you have cross-VPC access requirements.</td>
</tr>
<tr>
<td>Network</td>
<td>If the network type is VPC, select a VPC instance.
If the network type is CCN, associate a CCN instance on the details page after you create a gateway. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1037/46429">Associating a CCN instance</a>.</td>
</tr>
<tr>
<td>SSL VPN Connections</td>
<td>If the protocol type is SSL, you must set this parameter. The number of supported SSL VPN connections vary based on the gateway. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1037/32682">Use Limits</a>.</td>
</tr>
<tr>
<td>Tag</td>
<td>Customize a tag to facilitate resource categorization. Currently, only IPSec VPN gateways support tags.</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>Select the billing mode. IPsec VPN gateways and SSL VPN gateways support the pay-as-you-go billing mode.<ul><li>Pay-as-you-go: This mode is suitable for scenarios where the bandwidth fluctuates greatly.</li></ul></td>
</table>
