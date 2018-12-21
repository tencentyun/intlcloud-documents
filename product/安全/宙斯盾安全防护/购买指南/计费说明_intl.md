## Billing Method

Tencent Cloud Aegis Anti-DDoS uses a mixed billing model. Base protection bandwidth is prepaid on a monthly basis, while elastic protection bandwidth is pay-per-use on a daily basis.

### **DDoS Protective IP**
DDoS protective IP is divided into the following parts for billing:
<table>

<tr>
<th colspan="2">Billable item</th>
<th>Billing method</th>
<th>Payment mode</th>
<th>Billing description</th>
</tr>

<tr>
<td colspan="2">Base protection bandwidth</td>
<td>Monthly</td>
<td>Frozen prepayment</td>
<td>This provides basic protection bandwidth at a price determined by the base protection bandwidth and the length of purchase. After the purchase is made, the prepayment will be frozen and deducted on the 1st day of the following month. If the base protection is upgraded, extra fees will be charged on top of the original fees, and the protection level can be upgraded but not downgraded. </td>
</tr>

<tr>
<td colspan="2">Elastic protection bandwidth</td>
<td>Daily</td>
<td>Pay as you go</td>
<td>Elastic protection can be enabled free of charge. After the elastic protection is triggered, it is billed based on the bandwidth range on that day, and the bill is generated the following day. If elastic protection is not triggered, no fees will be charged. </td>
</tr>

<tr>
<td colspan="2">Forwarding port</td>
<td>USD7.70/month/port</td>
<td>Frozen prepayment</td>
<td>By default, 60 forwarding ports are provided per IP/package free of charge. If extra ports are configured, each additional port costs USD7.70 per month. Up to 500 forwarding ports can be configured. </td>
</tr>


<tr>
<td rowspan="2">Forwarded business traffic</td>
<td>Bill-by-bandwidth</td>
<td>Daily</td>
<td>Pay as you go</td>
<td rowspan="2">The business traffic forwarded to the real server by the protective IP or package is measured in the direction from the real server to Tencent Cloud. This is free of charge if below 100 Mbps, and if above 100 Mbps, the excessive portion is pay-per-use and billed on the following day. BGP protective IP and non-BGP protective IP are charged at different prices and their costs are calculated separately. </td>
</tr>

<tr>
<td>Bill-by-traffic</td>
<td>Daily</td>
<td>Pay as you go</td>

</tr>
</table>


### **DDoS Protection Pack**

DDoS protection pack is divided into the following parts for billing:

<table>

<tr>
<th colspan="2">Billable item</th>
<th>Billing method</th>
<th>Payment mode</th>
<th>Billing description</th>
</tr>



<tr>
<td colspan="2">Base protection bandwidth</td>
<td>Monthly</td>
<td>Frozen prepayment</td>
<td>This provides basic protection bandwidth at a prepaid price determined by the base protection bandwidth and the length of purchase. After the purchase is made, the prepayment will be frozen and deducted on the 1st day of the following month. If the base protection is upgraded, extra fees will be charged on top of the original fees, and the protection level can be upgraded but not downgraded. </td>
</tr>


<tr>
<td rowspan="2">Elastic billing method</td>
<td>Elastic traffic pack</td>
<td>Usage</td>
<td>Prepaid</td>
<td>Elastic traffic packs are purchased in advance, and after elastic protection is triggered, traffic is deducted from the purchased traffic packs based on the applicable elastic protection bandwidth range. One elastic traffic pack is valid for three years. </td>
</tr>

<tr>
<td>Elastic bandwidth</td>
<td>Daily</td>
<td>Pay as you go</td>
<td>Elastic protection can be enabled free of charge. After the elastic protection is triggered, it is billed based on the bandwidth range on that day, and the bill is generated the following day. If elastic protection is not triggered, no fees will be charged. </td>
</tr>
</table>

