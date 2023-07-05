This document describes the public network prices under different billing modes and helps you choose the billing plan that best suits your business.
>? Note that the network fees mentioned in the document are only applied to general BGP IPs. For the prices of premium BGP IPs and accelerated IPs,  see [Bandwidth Package](#bwp).
>
## [Bill-by-Traffic](id:by-traffic)
Fees are pay-as-you-go on an hourly billing cycle based on the public network traffic used. Bill-by-traffic is suitable for scenarios where the peak business traffic fluctuates greatly at varying times.
**Pricing**
<table>
<thead>
<tr>
<th rowspan="2" width="65%">Region</th>
<th colspan="2" style="text-align:center;">Price (USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>Chinese mainland, Hong Kong (China), Jakarta, Seoul</td>
<td>0.12</td>
</tr>
<tr>
<td>Tokyo</td>
<td>0.13</td>
</tr>
<tr>
<td>Singapore</td>
<td>0.081</td>
</tr>
<tr>
<td>São Paulo</td>
<td>0.15 </td>
</tr>
<tr>
<td>Frankfurt, Silicon Valley, Toronto</td>
<td>0.077</td>
</tr>
<tr>
<td>Mumbai, Bangkok</td>
<td>0.1</td>
</tr>
<tr>
<td>Virginia</td>
<td>0.075</td>
</tr>
</tbody></table>



**Billing example**
Suppose you purchase an EIP in Guangzhou region in bill-by-traffic mode and use a total of 10 GB traffic between 07:00:00-07:59:59, then at 8:00:00, the payable fees will be 0.12 USD/GB * 10 GB = 1.2 USD.

> ?
> - The traffic units are 1024-based, which means 1 TB = 1,024 GB, and 1 GB = 1,024 MB.
> - Public network traffic refers to the downstream (i.e., outbound) traffic in bytes. During actual data transfer, the traffic generated over the network is around 5-15% more than the application-layer traffic, so the traffic calculated on the Tencent Cloud side may be about 10% more than that calculated on the customer side.
>  - TCP/IP headers: If TCP/IP is used, a packet has a header of 40 bytes. The traffic consumed for the headers is not counted on the application layer. The overhead of this part is around 3% of the traffic.
>  - TCP retransmission: During normal data transfer over the network, around 3-10% of packets are lost and retransmitted. The traffic consumed for the re-transmission is not counted on the application layer. It accounts for 3-7% of the total traffic.
> 


## [Bandwidth Package](id:bwp)
Tencent Cloud Bandwidth Package (BWP) is a multi-IP aggregated billing method. This mode greatly saves your public network fees when your public network instances have traffic peaks at different times.
Different IP line types correspond to different BWP types and fees as shown below:
<table>
<thead>
<tr>
<th>IP Line Type</th>
<th>BWP Type</th>
</tr>
</thead>
<tbody><tr>
<td>General BGP IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">BGP bandwidth package</a></td>
</tr>
<tr>
<td>Premium BGP IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">Premium BGP bandwidth package</a></td>
</tr>
<tr>
<td>Accelerated IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">AIA BGP bandwidth package</a></td>
</tr>
</tbody></table>

## References
- [Public Network Bandwidth Cap](https://intl.cloud.tencent.com/document/product/213/12523)
