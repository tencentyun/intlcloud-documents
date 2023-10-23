
## Standard Edition
New billing rules for Tencent Cloud Anti-DDoS Pro (Standard) has officially taken effect since **March 24, 2022**.

### Billing mode
 The Anti-DDoS Pro (Standard) guarantees an all-out protection capability. Integrating the local cleansing capability, the all-out protection aims to spare no effort to successfully defend against each DDoS attack. In addition, the all-out protection will be enhanced along with the advance of Tencent Cloud network capabilities, and for which no extra upgrade costs are required.

>! Tencent Cloud reserves the right to restrict the traffic if the DDoS attacks on your application affect the infrastructure in the Tencent Cloud Anti-DDoS cleansing center. If the traffic of your Anti-DDoS Pro (Standard) instance is restricted, your application may suffer the problems such as limited or blocked access traffic.

 Anti-DDoS Pro (Standard) is billed by application bandwidth and the number of protected IPs on a yearly basis. The supported validity periods are 1 year, 2 years, and 3 years. The instance unit prices vary by specification, which you can choose as needed. The protection service is currently available in Beijing, Shanghai, and Guangzhou.

<table>
<thead>
<tr>
<th width="10%">Parameter</th>
<th width="10%">Billing mode</th>
<th width="10%">Payment mode</th>
<th width="70%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Number of protected IPs</td>
<td>Monthly subscription</td>
<td>Postpaid</td>
<td>Please select the number of application IPs to be protected by an Anti-DDoS Pro (Standard) instance. Options: 10 (default), 50, and 100. If you need protection for more IPs, extra fees will be charged. The number can only be increased but not decreased.</td>
</tr>
<tr>
<td rowspan=2>Application bandwidth</td>
<td rowspan=2>Monthly subscription</td>
<td>Postpaid</td>
<td>The application bandwidth refers to the normal bandwidth of the protected application. It is billed based on monthly 95th percentile by either the outgoing or incoming traffic (whichever is higher). For the price, see <a href="https://www.tencentcloud.com/document/product/1029/55300#yw">Pricing of application bandwidth</a>. Anti-DDoS Pro (Standard) allows you to exceed your plan’s limit, but the all-out protection capability will become not available and only the basic protection capability remains when the limit has been exceeded for 36 hours accumulatively in a month.</td>
</tr>
<tr> 
<td>Postpaid</td>
<td>When elastic application bandwidth is enabled, the amount of bandwidth exceeding the specified amount will be billed.</td>
</tr>
</tbody></table>

>?
>- To use an Anti-DDoS Pro (Standard) instance, please select the same instance region as your other Tencent Cloud resources such as CVM or CLB instances, and bind it to your application IP first.
>- 95th percentile bandwidth: In each calendar month, the inbound/outbound bandwidth is sampled every 5 minutes and the maximum is taken as the peak bandwidth on each day. At the end of the month, the sampled values are sorted from highest to lowest, and the top 5% are removed. The 95th largest value is the billable bandwidth of the month.

#### Calculation formula for elastic application bandwidth
Fee on elastic application bandwidth = (95th percentile of the monthly peak bandwidth - Prepaid application bandwidth) x Unit price of application bandwidth

### Pricing

An Anti-DDoS Pro (Standard) instance protects application IPs in the same region by default, and the number of protected IPs can be increased. If you need protection for multiple IPs in different regions, you need to purchase multiple instances. If you find the specifications are not ideal, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>? Discount for yearly subscription is not available together with other discounts. The maximum discount is applied automatically at the time of purchase.

#### Pricing of application bandwidth[](id:yw)
<table>
<thead>
<tr>
<th  width="20%" rowspan=2>Application bandwidth</th>
<th colspan=1>Unit price (postpaid)</th>
</tr>
<tr>
<th>Monthly list price</td>

</tr>
</thead>
<tbody>
<tr>
<td>0-1 Gbps (inclusive)</td>
<td>14 USD/Mbps/month</td>
</tr>
<tr>
<td>1-3 Gbps (inclusive)</td>
<td>10 USD/Mbps/month</td>
</tr>
<tr>
<td>3-10 Gbps (inclusive)</td>
<td>7 USD/Mbps/month</td>
</tr>
<tr>
<td>10 Gbps above</td>
<td>4 USD/Mbps/month</td>
</tr>
</tbody></table>

#### Pricing of protected IPs	
<table>
<thead>
<tr>
<th  width="20%" and rowspan=2>Number of protected IPs</th>
<th  width="80%" and  colspan=1 >Monthly subscription price (USD)</th>
</tr>
<tr>
<th>List price</th>
</tr>
</thead>
<tbody>
<tr>
<td>10 IPs</td>
<td>8890</td>
</tr>
<tr>
<td>50 IPs</td>
<td>17780</td>
</tr>
<tr>
<td>100 IPs</td>
<td>33333.33</td>
</tr>
</tbody></table>

<dx-alert infotype="explain" title="">
- For a 10-IP plan, 50 Mbps of application bandwidth is offered for free by default.
- For a 50-IP plan, 300 Mbps of application bandwidth is offered for free by default.
- For a 100-IP plan, 1,000 Mbps of application bandwidth is offered for free by default.
</dx-alert>

#### [CC protection cap](id:txfh)

<table>
<thead>
<tr>
<th width="20%">Region</th>
<th width="80%">CC protection cap</th>
</tr>
</thead>
<tbody><tr>
<td>Guangzhou</td>
<td>300,000 QPS</td>
</tr>
<tr>
<td>Shanghai</td>
<td>700,000 QPS</td>
</tr>
<tr>
<td>Beijing</td>
<td>300,000 QPS</td>
</tr>
</tbody></table>
