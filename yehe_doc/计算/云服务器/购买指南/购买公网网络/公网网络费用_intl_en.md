This document describes the public network prices under different billing modes and helps you choose the billing plan that best suits your business.

## Bill-by-traffic
>? Fees are pay-as-you-go on an hourly billing cycle based on the public network traffic used. Bill-by-traffic is suitable for scenarios where the peak business traffic fluctuates greatly at varying times.

**Pricing**
<table>
<thead>
<tr>
<th>Region</th>
<th>Price (unit: USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>Chinese mainland (not including Hong Kong, Macao, and Taiwan), Seoul, Hong Kong (China), Jakarta</td>
<td>0.12</td>
</tr>
<tr>
<td>Singapore</td>
<td>0.081</td>
</tr>
<tr>
<td>Toronto, Silicon Valley, Frankfurt</td>
<td>0.077</td>
</tr>
<tr>
<td>Moscow, Tokyo</td>
<td>0.13</td>
</tr>
<tr>
<td>Virginia</td>
<td>0.075</td>
</tr>
<tr>
<td>Bangkok, Mumbai</td>
<td>0.1</td>
</tr>
</tbody></table>


**Billing example**
Suppose you purchase an EIP in Seoul region with the bill-by-traffic billing mode and use a total of 10 GB traffic between 07:00:00-07:59:59, then at 8:00:00, the payable fees will be: 0.12 USD/GB × 10 GB = 1.2 USD.

> ?
> - The traffic units are 1024-based. For example, 1 TB = 1,024 GB, and 1 GB = 1,024 MB.
> - Public network traffic refers to the downstream traffic (in bytes), which is the application-layer data. During actual data transfer, the traffic generated over the network is around 5-15% more than the application-layer traffic, so the traffic calculated by Tencent Cloud may be about 10% more than that calculated by users themselves on the server.
>  - Consumption by TCP/IP headers: in TCP/IP-based HTTP requests, each packet has a maximum size of 1,500 bytes and includes TCP and IP headers of 40 bytes, which generate traffic during transfer but cannot be counted by the application layer. The overhead of this part is around 3%.
>  - TCP retransmission: during normal data transfer over the network, around 3-10% of packets are lost on the Internet and retransmitted by the server. This type of traffic, which accounts for 3-7% of the total traffic,  cannot be counted at the application layer.


## Bandwidth Package
Tencent Cloud Bandwidth Package (BWP) is a multi-IP aggregated billing method. This mode greatly saves your public network fees when your public network instances have traffic peaks at different times.
For detailed pricing, please see [Billing Modes](https://intl.cloud.tencent.com/document/product/684/15255).


## Reference
- [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578)
- [Public Network Bandwidth Cap](https://intl.cloud.tencent.com/document/product/213/12523)
