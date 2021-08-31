

## Billing Mode
Anti-DDoS Advanced billing includes the fees of base protection bandwidth (frozen fees payment), elastic protection bandwidth (pay-as-you-go), and application bandwidth (frozen fees payment).

<table>
<tr>
<th width = "15%">Billable Item</th>
<th width = "15%">Billing Mode</th>
<th width = "9%">Payment Method</th>
<th>Billing Description</th>
</tr>
<tr>
<td >Base protection bandwidth</td>
<td> Monthly subscription</td>
<td>Frozen fees payment</td>
<td>It provides base protection bandwidth. The amount of frozen fees is based on the base protection bandwidth and subscription plan period. Fees will be frozen at the time of successful purchase and settled on the 1st day of the next month.</td>
</tr>
<tr>
<td >Elastic protection bandwidth</td>
<td>Pay-as-you-go on a daily basis</td>
<td>Pay-as-you-go</td>
<td>If elastic protection is triggered, you will be billed on the following day based on the tiered price of the peak attack bandwidth of the current day. You will not be billed if elastic protection is not triggered. You can upgrade or downgrade the configuration.</td>
</tr>
<tr>
<td >Forwarding rules</td>
<td>Monthly subscription based on the rule quantity</td>
<td>Pay-as-you-go</td>
<td>60 forwarding rules are provided for free for each Anti-DDoS Advanced instance by default. 65 USD is charged per month for every additional 10 rules. Each Anti-DDoS Advanced instance can have up to 300 forwarding rules.</td>
</tr>
<tr>
<td >Application bandwidth</td>
<td>Bill-by-bandwidth on a monthly subscription basis</td>
<td>Frozen fees payment</td>
<td>The application bandwidth limit applies to both the inbound Anti-DDoS forwarding traffic and the outbound Anti-DDoS traffic. The application bandwidth needs to be higher than the peak bandwidth of the two, whichever is greater. If the actual application bandwidth is continuously higher than the application bandwidth selected when you purchased your Anti-DDoS Advanced instance, packet loss may occur. This might affect your service. We recommend adjusting your application bandwidth to avoid such occurrences.</td>
</tr>
</table>


### Base protection
Base protection is on the monthly frozen fees payment. The detailed pricing is as follows:

| Anti-DDoS Protection | Anti-CC Protection | Chinese mainland (USD/month) | Regions outside the Chinese mainland (USD/month)|
| -------------- | ------------ | ------------------ | ------------------ |
| 10 Gbps         | 20,000 QPS    | -                  | 2,500             |
| 20 Gbps         | 40,000 QPS    | 2,400              | 4,800             |
| 30 Gbps         | 70,000 QPS    | 3,500             | 7,000             |
| 40 Gbps         | 100,000 QPS   | -                  | 8,200             |
| 50 Gbps         | 150,000 QPS   | 9,500             | 10,500             |
| 60 Gbps         | 200,000 QPS   | -                  | 12,000             |
| 80 Gbps         | 250,000 QPS   | -                  | 15,000             |
| 100 Gbps        | 300,000 QPS   | 28,000             | 16,500             |

>?
>- Query Per Second (QPS) here is used to measure the number of CC attack requests per second that an Anti-DDoS Advanced instance can defend against.
>- Tencent Cloud provides up to TB-level protection capability. Contact your sales rep if necessary.

<span id="txfh"></span> 
### Elastic protection
You can enable elastic protection as needed.
- If elastic protection is not enabled for an instance, its base protection bandwidth will be the maximum protection bandwidth and no extra fees will be incurred.
- If elastic protection is enabled for an instance, its maximum protection bandwidth will be the elastic protection bandwidth.
 - If elastic protection is not triggered, no fees will be incurred.
 - If elastic protection is triggered and the attack traffic is higher than the base protection bandwidth but lower than the elastic protection bandwidth, you will be billed on the following day based on the tiered price of the peak attack bandwidth of the current day.

The detailed pricing of elastic protection is as follows:

| Anti-DDoS Protection Peak Bandwidth | Chinese mainland (USD/day) | Regions outside the Chinese mainland (USD/day)|
| -------------------- | ------------------- | ------------------- |
| 10 Gbps ≤ Peak attack bandwidth < 20 Gbps   | -                   | 320             |
| 20 Gbps ≤ Peak attack bandwidth < 30 Gbps   | 260              | 400              |
| 30 Gbps ≤ Peak attack bandwidth < 40 Gbps   | 450               | 700               |
| 40 Gbps ≤ Peak attack bandwidth < 50 Gbps   | 600               | 800               |
| 50 Gbps ≤ Peak attack bandwidth < 60 Gbps   | 800               | 1,200               |
| 60 Gbps ≤ Peak attack bandwidth < 70 Gbps   | 1,200               | 1,800              |
| 70 Gbps ≤ Peak attack bandwidth < 80 Gbps   | 1,500               | 2,200              |
| 80 Gbps ≤ Peak attack bandwidth < 90 Gbps   | 1,700               | 2,500              |
| 90 Gbps ≤ Peak attack bandwidth < 100 Gbps  | 1,900              | 2,700              |
| 100 Gbps ≤ Peak attack bandwidth < 120 Gbps | 2,100              | 2,900              |
| 120 Gbps ≤ Peak attack bandwidth < 150 Gbps | 2,300              | 3,200              |
| 150 Gbps ≤ Peak attack bandwidth < 200 Gbps | 2,700              | 4,000              |
| 200 Gbps ≤ Peak attack bandwidth < 250 Gbps | 4,800              | 4,800              |
| 250 Gbps ≤ Peak attack bandwidth < 300 Gbps | 5,600              | 5,600              |
| 300 Gbps ≤ Peak attack bandwidth < 400 Gbps | -                   | 6,600              |

### Forwarding rules
| Number of Forwarding Rules                      |  Price (USD/month/10 rules) |
| --------------------------- | ------------------ |
| Number of ports (or protected domain names) ≤ 60  | Free               |
| Number of ports (or protected domain names)  > 60 | 65                |

>?The number of forwarding rules is the total number of TCP/UDP ports (for non-website connections) and HTTP/HTTPS domain names (for website connections) that you configure for an Anti-DDoS Advanced instance.

### Application bandwidth
Application bandwidth is the bandwidth used for forwarding the application traffic that has been cleansed by the Tencent Cloud Anti-DDoS data center back to the data center on the real server.
It is on a monthly-subscribed frozen fees payment. **For non-Tencent Cloud users in the Chinese mainland, 100 Mbps forwarding bandwidth will be given free of cost after they purchase the base protection package.** The detailed pricing is as follows:

| Bandwidth | Price (USD/month) |
|-|-|
|50 Mbps|750|
|100 Mbps|1,500|
|150 Mbps|2,250|
|200 Mbps|3,000|
|500 Mbps|7,500|
|1 Gbps|15,000|
|2 Gbps|30,000|


The relationship between the application bandwidth and the number of layer-7 requests is as follows:

| Application Bandwidth | HTTP/HTTPS     |
| -------- | -------- |
|50 Mbps          |      5,000 QPS|
|100 Mbps       |      10,000 QPS|
|150 Mbps      |       15,000 QPS|
|200 Mbps      |       20,000 QPS|
|500 Mbps      |       50,000 QPS|
|1 Gbps          |      100,000 QPS|
|2 Gbps          |      200,000 QPS|

>!
>- The application bandwidth limit applies to both the inbound Anti-DDoS forwarding traffic and the outbound Anti-DDoS traffic. The application bandwidth needs to be higher than the peak bandwidth of the two, whichever is greater. If the actual application bandwidth is continuously higher than the application bandwidth selected when you purchased your [Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/15483) instance, packet loss may occur. This might affect your application. We recommend upgrading your application bandwidth in time.
>- The QPS metric used here is a general number of queries per second when there is no attack. If the actual QPS of your application is higher than the specification purchased, please [adjust the specification of your Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/34089) to prevent packet loss. You can refer to the relationship table above to increase the application bandwidth of your Anti-DDoS Advanced instance and the general HTTP/HTTPS QPS metric.

## Other Metrics
See the following table for descriptions of other metrics:
<table>
<tr>
<th width = "20%">Metric</th>
<th width = "30%">Specification</th>
<th>Description</th>
</tr>
<tr>
<td>Number of forwarding ports</td>
<td rowspan="2">60-300/Anti-DDoS Advanced instance</td>
<td rowspan="2">The total number of forwarding rules for TCP/UDP and HTTP/HTTPS. For TCP and UDP, if the same forwarding port number is used, two different forwarding rules need to be configured.</td>
</tr>
<tr>
<td>Number of supported domain names</td>
</tr>
<tr>
<td>Number of real server IPs</td>
<td> 20/instance</td>
<td>The total number of IP addresses for both layer-4 and layer-7 real servers.</td>
</tr>
<tr>
<td>Number of new connections per second</td>
<td>50,000/Anti-DDoS Advanced instance</td>
<td>The number of new connections per second for each Anti-DDoS Advanced instance.</td>
</tr>
<tr>
<td>Number of concurrent connections</td>
<td>200,000/Anti-DDoS Advanced instance</td>
<td>The number of concurrent connections per second for each Anti-DDoS Advanced instance.</td>
</tr>
</table>

>?The specifications above are only the ready-made ones. If you find the specifications are not ideal, please contact [Tencent Cloud technical support](https://intl.cloud.tencent.com/zh/support) to customize a higher specification.

## Billing Example
Anti-DDoS Advanced uses a combined billing method. Below is a fee calculation example:
A user purchases an Anti-DDoS Advanced instance in the Shanghai region, with "20 Gbps base protection bandwidth" and "50 Gbps elastic protection bandwidth".
One day, DDoS attacks occur with a peak attack bandwidth of 45 Gbps, which exceeds the base protection bandwidth and triggers elastic protection. The peak attack bandwidth falls in the billing tier between 40 Gbps and 50 Gbps, and the elastic protection fee generated that day is 600 USD.
Therefore, the user needs to pay a total of 3,000 USD, including 2,400 USD of the monthly base protection fee and 600 USD of the elastic protection fee generated that day.