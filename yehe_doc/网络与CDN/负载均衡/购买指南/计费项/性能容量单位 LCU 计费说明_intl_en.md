An [LCU](https://intl.cloud.tencent.com/document/product/214/32394) measures the metrics on which that CLB processes traffic. This document describes how the LCU charge is calculated.
>?
>+ Only LCU-supported CLB instances will incur LCU usage fees. LCU-supported CLB instances are only available to beta users. To use it, please [submit an application](https://intl.cloud.tencent.com/apply/p/fj5bwo9e6rj).
>+ Shared CLB instances are free of LCU charges.


## Pay As You Go
In the pay-as-you-go model, you will pay for the LCUs consumed based on the following CLB performance metrics:
<table>
<tr>
<th width="15%">Metric</th>
<th>Description</th>
</tr>
<tr>
<td>New connections</td>
<td>Number of newly established connections per second.</td>
</tr>
<tr>
<td>Concurrent connections</td>
<td>Number of concurrent connections.</td>
</tr>
<tr>
<td>Processed traffic</td>
<td>Number of bytes (both outbound and inbound) processed by the CLB instance in Gigabytes (GB).</td>
</tr>
<tr>
<td>Rule evaluations (only for HTTP/HTTPS)</td>
<td>It is the product of number of rules processed by your CLB instance and queries per second (QPS). The first 10 processed rules are free:<ul><li>For over 10 processed rules, rule evaluations = QPS × (number of processed rules – 10 free rules).</li><li>For 10 or fewer processed rules, rule evaluations = QPS.</li></ul></td>
</tr>
</table>

>?
+ The number of LCUs consumed for one hour is calculated based on the above four metrics and the maximum consumed across the four metrics will be charged.
+ LCU unit price: 0.0072 USD/hour
+ In the pay-as-you-go model, LCU-billing CLB instances provide the highest performance specification. The metrics are:
  + Concurrent connections: 1,000,000
  + New connections: 100,000
  + QPS: 50,000
  + Bandwidth: 10 Gbps
>

The performance specification per LCU varies depending on the protocol. 
<table>
<thead>
<tr>
<th width="30%">Protocol</th>
<th>Performance Specification Per LCU</th>
</tr>
</thead>
<tbody><tr>
<td>HTTP/HTTPS</td>
<td>
	<ul>
		<li>25 new connections per second</li>
		<li>3,000 concurrent connections per minute</li>
		<li>1 GB of traffic per hour</li>
		<li>1,000 rule evaluations per second</li>
	</ul>
</td>
</tr>
<tr>
<td>TCP</td>
<td>
	<ul>
		<li>800 new connections per second</li>
		<li>100,000 concurrent connections per minute</li>
		<li>1 GB of traffic per hour</li>
	</ul>
</td>
</tr>
<tr>
<td>UDP/QUIC</td>
<td>
	<ul>
		<li>400 new UDP flows</li>
		<li>50,000 active UDP flows</li>
		<li>1 GB of traffic per hour</li>
	</ul>
</td>
</tr>
<tr>
<td>TCP SSL</td>
<td>
	<ul>
		<li>800 new connections per second</li>
		<li>100,000 concurrent connections per minute</li>
		<li>50 new TLS flows</li>
		<li>3,000 active TLS flows</li>
		<li>1 GB of traffic per hour</li>
	</ul>
</td>
</tr>
</tbody>
</table>

### Pricing examples
<dx-tabs>
::: Example 1: HTTP/HTTPS
Assume that your CLB instance receives an average of 100 new connections per second, each lasting 3 minutes. A client sends an average of 4 requests per second per connection, and 1,000 KB of requests and responses are processed per second in total. You have configured an HTTP (80) listener and an HTTPS (443) listener, with 20 forwarding rules to route your client requests. You are charged on the following metrics:
+ New connections (per second): Each LCU provides 25 new connections per second. Since your CLB instance receives 100 new connection per second, this translates to 4 LCUs (100 connections / 25 connections).
+ Concurrent connections (per minute): Each LCU provides 3,000 concurrent connections per minute. Since your CLB instance receives 100 new connection per second (that is, 6,000 new connections per minute), each lasting 3 minutes, this translates to 18,000 concurrent connections (6,000 new connections * 3 minutes), or 6 LCUs (18,000 concurrent connections / 3,000 concurrent connections).
+ Processed traffic (per hour): Each LCU provides 1 GB per hour. Since your CLB instance processes 1,000 KB of data per second, this translates to 3.6 GB per hour or 3.6 LCUs (3.6 GB / 1 GB).
+ Rule evaluations (per second): Each LCU provides 1,000 rule evaluations per second. Since your CLB instance receives 100 new connections per second and a client sends an average of 4 requests per second per connection, your CLB instance receives a total of 400 requests per second. Therefore, 20 forwarding rules for each request results in 4,000 rule evaluations per second (20 forwarding rules – 10 free rules) * 400 or 4 LCUs (4,000 rule evaluations / 1,000 rule evaluations).
 
In this example, the concurrent connections translate to 6 LCUs, the maximum LCUs among the four metrics, resulting in a total charge of 0.0432 USD/hour (6 LCUs * 0.0072 USD per LCU) or 31.104 USD/month (0.00432 USD * 24 hours * 30 days).

:::

::: Example 2: TCP/UDP
Assume that your CLB instance receives 100 new TCP connections (each lasting 3 minutes) and transfers 1,000 processed bytes while receives 100 new UDP flows (each lasting 2 minutes) and transfers 1,000 processed bytes. Your monthly CLB bill will be calculated as follows:
	 **TCP traffic**
   + New connections: Each LCU provides a maximum of 800 new TCP connections per second. Since your CLB instance receives 100 new TCP connections per second, this translates to 0.125 LCUs (100 new connections per second / 800 new connections per second).
   + Concurrent connections: Each LCU provides a maximum of 100,000 TCP concurrent connections. Since your CLB instance receives 100 new TCP connections per second (that is 18,000 concurrent connections per minute), each lasting 3 minutes, this translates to 0.18 LCUs (18,000 concurrent connections / 100,000 concurrent connections).
   + Processed bytes: Each LCU provides 1 GB per hour. Since your CLB instance transfers an average of 1,000 processed bytes to each TCP client, this translates to 0.36 GB (100 connections per second * 60 seconds * 60 minutes * 1,000 bytes) or 0.36 LCUs (0.36 GB / 1 GB).
  
**UDP traffic**
   + New flows: Each LCU provides 400 new UDP flows per second. Since your CLB instance uses 100 new UDP flows per second, this translates to 0.25 LCUs (100 flows per second / 400 flows per second).
   + Active flows: Each LCU provides 50,000 active UDP flows per minute. Since your CLB instance receives 100 new UDP flows per second, each lasting 120 seconds, this translates to 12,000 active flows or 0.24 LCUs (12,000 active flows / 50,000 active connections).
   + Processed bytes: Each LCU provides 1 GB per hour. Since your CLB instance transfers an average of 1,000 processed bytes to each UDP client, that is 0.36 GB per hour (100 connections per second * 60 seconds * 60 minutes * 1,000 bytes), which translates to 0.36 LCUs (0.36 GB / 1GB).
  
Using these values, the hourly bill for each protocol is calculated by taking the maximum LCUs consumed among the three metrics.
 + In the example with TCP traffic, the LCU usage for processed bytes (0.36 LCUs) is greater than new connections (0.125 LCUs) and concurrent connections (0.18 LCUs), resulting in a total charge of 0.002592 USD/hour (0.36 LCUs * 0.0072 USD per LCU) or 1.86624 USD/month (0.002592 USD * 24 hours * 30 days).
 + In the example with UDP traffic, the LCU usage for processed bytes (0.36 LCUs) is greater than new flows (0.25 LCUs) and active flows (0.24 LCUs), resulting in a total charge of 0.002592 USD/hour (0.36 LCUs * 0.0072 USD per LCU) or 1.86624 USD/month (0.002592 USD * 24 hours * 30 days).
 
In this case, your LCU charge is 0.005184 USD/hour (0.002592 USD for TCU traffic and 0.002592 USD for UDP traffic)
:::
</dx-tabs>

