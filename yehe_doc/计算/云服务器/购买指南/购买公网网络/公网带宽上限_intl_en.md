This document describes the outbound and inbound bandwidth cap of CVM instances, and compares the peak bandwidth in different billing modes.

## Outbound Bandwidth Cap (Downstream Bandwidth)

The public network bandwidth cap refers to the upper limit of outbound bandwidth, i.e. the bandwidth going out from CVM instances. The public bandwidth cap varies by network billing mode. See below for details:
- The following rules apply to instances created after 00:00, February 24, 2020 (UTC +8):
<table>
<tbody><tr><th rowspan="2" style="width: 20%;">Network Billing Method</th><th colspan="2">Instance</th><th rowspan="2" style="width:35%">Maximum Bandwidth Cap Range (Mbps)</th></tr>
<tr><th style="width: 20%;">Instance Billing Method</th><th style="width: 25%;">Instance Configuration</th></tr>
<tr><td>Bill-by-traffic</td><td>Pay-as-you-go instances</td><td>All</td><td>0-100</td></tr>
<tr><td>Bill-by-bandwidth</td><td>Pay-as-you-go instances</td><td>All</td><td>0-100</td></tr>
<tr><td>Bandwidth package</td><td colspan="2">All</td><td>0-2000</td></tr>
</tbody></table>

- The following rules apply to instances created before 00:00, February 24, 2020 (UTC +8):
<table>
<tbody><tr><th rowspan="2" style="width: 20%;">Network Billing Method</th><th colspan="2">Instance</th><th rowspan="2" style="width:35%">Maximum Bandwidth Cap Range (Mbps)</th></tr>
<tr><th style="width: 20;">Instance Billing Method</th><th style="width: 25%;">Instance Configuration</th></tr>
<tr><td>Bill-by-traffic</td><td>Pay-as-you-go instances</td><td>All</td><td>0-100</td></tr>
<tr><td>Bill-by-bandwidth</td><td>Pay-as-you-go instances</td><td>All</td><td>0-100</td></tr>
<tr><td>Bandwidth package</td><td colspan="2">ALL</td><td>0-1000</td></tr>
</tbody></table>



## Inbound Bandwidth Cap (Upstream Bandwidth)

The public network inbound bandwidth refers to the bandwidth that flows into CVM instances.
- Bill-by-traffic public IP:
 - If the bandwidth you purchased is less than or equals to 10 Mbps, Tencent Cloud will assign 10 Mbps public network inbound bandwidth.
 - If the bandwidth you purchased is greater than 10 Mbps, Tencent Cloud will assign a public network inbound bandwidth equals to the purchased bandwidth.
- Bill-by-bandwidth package public IP:
Tencent Cloud will assign a public network inbound bandwidth equals to the purchased bandwidth.

## Peak Bandwidth
The peak bandwidth is applicable to both bill-by-traffic and bill-by-bandwidth, but it means differently in these two cases as follows:

<table>
       <tbody><tr>
			 <th width="17%">Billing Mode</th>
			 <th>Difference</th>
			 <th>Description</th>
       </tr>
			 <tr>
			 <td>Bill-by-traffic</td>
			 <td>The peak bandwidth is only regarded as the <strong>maximum peak bandwidth</strong>, and not as the committed bandwidth. When bandwidth resources are contested, the peak bandwidth may be limited.</td> 
			 <td>The sum of peak bandwidth of all the running bill-by-traffic instances (such as CVMs, EIPs, elastic IPv6 addresses) cannot exceed 5 Gbps in one region. If your application requires a guaranteed or higher bandwidth, choose bill-by-bandwidth.</td> 
			 </tr>
       <tr>          
            <td>Bill-by-bandwidth<br/>(including monthly bandwidth subscription and hourly bandwidth)</td>
            <td>This peak bandwidth is the committed bandwidth, and is guaranteed in case of bandwidth competition.</td>
						<td>The sum of peak bandwidth of all the running instances such as CVMs and EIPs that are billed at a fixed bandwidth (including monthly-subscribed bandwidth and hourly bandwidth) cannot exceed 50 Gbps in one region. If you require a higher bandwidth, contact your sales rep.

</td> 
            </tr> 
</tbody></table>


## See Also
- [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517)
