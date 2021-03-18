This document describes the public network prices under different billing modes and helps you choose the billing plan that best suits your business.

## Monthly Bandwidth Subscription
For the monthly bandwidth subscription plan, you pay for a fixed bandwidth in advance. Monthly bandwidth subscription is suitable for long-term scenarios with stable traffic.
>? The monthly subscription mode is currently in beta. To use it, please [contact sales](https://intl.cloud.tencent.com/contact-sales).

**Pricing**

<table>
<thead>
<tr>
<th rowspan="2" width="10%">Region</th>
<th colspan="3"  style="text-align:center;">Price (unit: USD/Mbps/month)</th>
</tr>
<tr>
<th>Bandwidth ≤ 2 Mbps</th>
<th>2 Mbps < Bandwidth ≤ 5 Mbps</th>
<th>Bandwidth > 5 Mbps</th>
</tr>
</thead>
<tbody><tr>
<td>Guangzhou<br>Qingyuan<br>Shanghai<br>Beijing<br>Hong Kong, China<br>Singapore</td>
<td>2.86   </td>
<td>3.57</td>
<td>12.86</td>
</tr>
<tr>
<td>Chengdu<br>Chongqing</td>
<td>2.57</td>
<td>3.15</td>
<td rowspan="5">11.43</td>
</tr>
<tr>
<td>Toronto<br>Silicon Valley<br>Virginia<br>Bangkok<br>Mumbai<br>Moscow</td>
<td colspan="2">4.29   </td>
</tr>
<tr>
<td>Seoul<br>Frankfurt</td>
<td colspan="2">2.86</td>
</tr>
<tr>
<td>Tokyo</td>
<td colspan="2">3.57</td>
</tr>
</tbody></table>

**Billing example**

Suppose you purchase an EIP in Guangzhou region and choose monthly bandwidth subscription billing mode. If you purchase a fixed bandwidth of 15 Mbps for 2 months, the fees will be: (2.86 USD/Mbps/month) × 2 Mbps + 3.57 USD/Mbps/month × 3 Mbps + 12.86 USD/Mbps/month × 10 Mbps) × 2 months = 290.06 USD.

## Bill-by-traffic
 
Fees are pay-as-you-go on an hourly billing cycle based on the public network traffic used. Bill-by-traffic is suitable for scenarios where the peak business traffic fluctuates greatly at varying times.
**Pricing**
<table>
<thead>
<tr>
<th>Region</th>
<th>Price (unit: USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>Chinese mainland (not including Hong Kong, Macao, and Taiwan), Seoul, Hong Kong (China)</td>
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

> ?Public network traffic is the traffic data based on the number of downstream bytes, which is the application-layer data. During actual data transfer, the traffic generated over the network is around 5-15% more than the application-layer traffic, so the traffic counted by Tencent Cloud may be about 10% more than that counted by users themselves on the server.
> - Consumption by TCP/IP headers: in TCP/IP-based HTTP requests, each packet has a maximum size of 1,500 bytes and includes TCP and IP headers of 40 bytes, which generate traffic during transfer but cannot be counted by the application layer. The overhead of this part is around 3%.
> - TCP retransmission: during normal data transfer over the network, around 3-10% of packets are lost on the Internet and retransmitted by the server. This type of traffic cannot be counted by the application layer and accounts for 3-7% of the total traffic.
> 


## Bandwidth Package
Tencent Cloud Bandwidth Package (BWP) is a multi-IP aggregated billing method. This mode greatly saves your public network fees when your public network instances have traffic peaks at different times.
For detailed pricing, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/684/15255).


## Documentation
- [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578)
- [Public Network Bandwidth Cap](https://intl.cloud.tencent.com/document/product/213/12523)
