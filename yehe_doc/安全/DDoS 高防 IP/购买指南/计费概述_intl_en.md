## Billing Mode
Anti-DDoS Advanced adopts a combo billing mode, utilizing both monthly subscription and pay-as-you-go. Specifically, base protection bandwidth, application bandwidth, and forwarding rules are on monthly subscription, while elastic protection bandwidth is pay-as-you-go on a daily billing cycle.

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
<td>Pay-as-you-go</td>
<td>Provides base protection bandwidth. The fee is billed based on the base protection bandwidth limit and subscription plan period. Fees will be frozen at time of purchase and settled on the 1st day of the next month.</td>
</tr>
<tr>
<td >Elastic protection bandwidth</td>
<td>Pay-as-you-go; daily billing cycle</td>
<td>Pay-as-you-go</td>
<td>Once elastic protection is triggered, you will be billed on the following day based on the tiered price of the peak attack bandwidth for the current day.</br>No charges will incur if no elastic protection is triggered. You can adjust the elastic protection configuration as needed.</td>
</tr>
<tr>
<td >Forwarding rules</td>
<td> Monthly subscription</br>Billed by count</td>
<td>Pay-as-you-go</td>
<td>60 forwarding rules are provided for free for each Anti-DDoS Advanced instance by default. Every additional 10 rules costs USD 100 per month. Each instance can have up to 500 forwarding rules.</td>
</tr>
<tr>
<td >Application bandwidth</td>
<td>Monthly subscription</br>Billed by bandwidth</td>
<td>Pay-as-you-go</td>
<td>The application traffic limit applies to both the inbound anti-DDoS forwarding traffic and the outbound Anti-DDoS traffic. The application bandwidth needs to be higher than the peak bandwidth of the two, 
 whichever is greater. If the actual application bandwidth is continuously higher than the Application Bandwidth selected when you purchased your Anti-DDoS Advanced instance, packet loss may occur. This 
 might affect your service. We recommend adjusting your application bandwidth to avoid such occurrences.</td>
</tr>
</table>

### Base Protection
Base protection is billed based on your monthly subscription plan. See the following table for detailed prices.

| Anti-DDoS Capacity | CC Protection Bandwidth | Non-BGP | BGP | Outside Chinese mainland |
|---------|---------|----|---------|---------|
| 20 Gbps | 40,000qps | -  |1,000 USD/month  | 4,800 USD/month |
| 50 Gbps | 150,000qps | 4,000 USD/month</br>25,000 USD/year  | 4,500 USD/month</br>35,000 USD/year | 10,500 USD/month  |
| 100 Gbps | 300,000qps | 40,000 USD/year  | 50,000 USD/year | 198,000 USD/year |
| 300 Gbps| 700,000qps | 60,000 USD/year  | 65,000 USD/year | - |
| 500Gbps| - | -  | 40,088 USD/year| - |
| 800Gbps| - | -  | 67,800 USD/year| - |
| 1000Gbps| - |-  | 81,800 USD/year| - |

>
- “Non-BGP” refers to China Mobile/China Union/China Telecom network services. If purchased, you will be provided with three Anti-DDoS Advanced instances, one for each of them.
- “Outside Chinese mainland” refers to Tencent Cloud regions outside the Chinese mainland, namely, Hong Kong (China), Taiwan (China), Singapore, Seoul, Tokyo, and Virginia.


<span id="txfh"></span>
### Elastic Protection
You can enable elastic protection as needed.
- If elastic protection is not enabled for an instance, its maximum protection will be the base protection bandwidth, and no extra fees will incur.
- If elastic protection is enabled for an instance, its maximum protection will be the selected elastic protection bandwidth.
 - If elastic protection is not triggered, no charges will be incurred.
 - Elastic protection will be triggered when the peak attack traffic exceeds the base protection bandwidth. You will be billed on the following day based on the tiered price of the peak attack bandwidth for the current day.

See the following table for detailed prices.

| Billing Tier      |  Non-BGP (USD/day) | BGP (USD/day) | Outside Chinese mainland (USD/day)  |
| -------------------- | ------------------- | ------------------- |------------------- |
| 20 Gbps ≤ Peak attack bandwidth < 30 Gbps   | -               | 260               | 400               |
| 30G bps ≤ Peak attack bandwidth < 40 Gbps   | -               | 450               | 700               |
| 40 Gbps ≤ Peak attack bandwidth < 50 Gbps   | -               | 600               | 800               |
| 50 Gbps ≤ Peak attack bandwidth < 60 Gbps   | 800               | 800               | 1,200               |
| 60 Gbps ≤ Peak attack bandwidth < 70 Gbps   | 1,200               | 1,200               | 1,800              |
| 70 Gbps ≤ Peak attack bandwidth < 80 Gbps   | 1,500               | 1,500               | 2,200              |
| 80 Gbps ≤ Peak attack bandwidth < 90 Gbps   | 1,700               | 1,700               | 2,500              |
| 90 Gbps ≤ Peak attack bandwidth< 100 Gbps  | 1,900              | 1,900              | 2,700              |
| 100 Gbps ≤ Peak attack bandwidth < 120 Gbps | 2,100              | 2,100              | 2,900              |
| 120 Gbps ≤ Peak attack bandwidth < 150 Gbps | 2,300               | 2,300              | 3,200              |
| 150 Gbps ≤ Peak attack bandwidth < 200 Gbps | 2,700               | 2,700              | 4,000              |
| 200 Gbps ≤ Peak attack bandwidth < 250 Gbps | 4,800              | 4,800              | 4,800              |
| 250 Gbps ≤ Peak attack bandwidth < 300 Gbps | 5,600              | 5,600              | 5,600              |
| 300 Gbps ≤ Peak attack bandwidth < 400 Gbps | -             | 6,400                    | 6,600              |
| 400 Gbps ≤ Peak attack bandwidth < 600 Gbps | -           | 8,800                  | -            |
| 600 Gbps ≤ Peak attack bandwidth < 900 Gbps |  -              | 14,666                   | -            |
| 900 Gbps ≤ Peak attack bandwidth < 1.2 Tbps | -                 |  20,000                  | -            |

### Forwarding Rules
| Number of Rules                      |  Price (USD/month per 10 rules) |
| --------------------------- | ------------------ |
| Number of ports (or protected domains) ≤ 60  | Free               |
| Number of ports (or protected domains)  > 60 | 100                |

>The number of forwarding rules is the total number of TCP/UDP ports (for non-website connections) and HTTP/HTTPS domain names (for website connections) that you configure for an Anti-DDoS Advanced instance.

### Application Bandwidth
Application bandwidth is the bandwidth used for forwarding the application traffic that has been cleansed by the Tencent Cloud Anti-DDoS data center back to the data center on the real server.
It is billed by the monthly subscription plan. See the following table for detailed prices.

| Bandwidth | Price (USD/month) |
|-|-|
|50 Mbps|750 |
|100 Mbps|1,500 |
|150 Mbps|2,250 |
|200 Mbps|3,000|
|500 Mbps|7,500|
|1 Gbps|15,000|
|2 Gbps|30,000 |

The relationship between the application bandwidth and the number of Layer-7 requests is as shown in the following table.

| Application Bandwidth     |  HTTP/HTTPS    |
| -------- | -------- |
| 50Mbps    | 5,000QPS  |
| 100Mbps |  10,000QPS  |
| 150Mbps  | 15,000QPS  |
| 200Mbps  |  20,000QPS  |
| 500Mbps  |  50,000QPS  |
| 1Gbps    | 100,000QPS |
| 2Gbps    | 200,000QPS |

>
>- The application traffic limit applies to both the inbound anti-DDoS forwarding traffic and the outbound Anti-DDoS traffic. The application bandwidth needs to be higher than the peak bandwidth of the two, whichever is greater. If the actual application bandwidth is continuously higher than the **Application Bandwidth** selected when you purchased your Anti-DDoS Advanced instance, packet loss may occur. This might affect your service. We recommend adjusting your application bandwidth to avoid such occurrences.
>- QPS measures the number of normal application requests per second when there are no attacks. If this number is larger than the application bandwidth you selected when you purchased your Anti-DDoS Advanced instance, we recommend that you increase the HTTP/HTTPS QPS limit promptly to avoid affecting your business due to packet loss. To adjust the application bandwidth, refer to the table above.

## Other Metrics
See the following table for descriptions of other metrics.
<table>
<tr>
<th width = "20%">Metric</th>
<th width = "30%">Limit</th>
<th>Description</th>
</tr>
<tr>
<td>Forwarding ports</td>
<td rowspan="2">60-500/Anti-DDoS Advanced instance</td>
<td rowspan="2">Total number of forwarding rules for TCP/UDP and HTTP/HTTPS. For TCP and UDP protocols, if the same forwarding port number is used, two different forwarding rules need to be configured.</td>
</tr>
<tr>
<td>Domain names</td>
</tr>
<tr>
<td>Real server IPs</td>
<td> 20/instance</td>
<td>Total number of IP addresses for both Layer-4 and Layer-7 real servers</td>
</tr>
<tr>
<td>New connections per second</td>
<td>50,000/Anti-DDoS Advanced instance</td>
<td>The number of new connections per second for each Anti-DDoS Advanced instance</td>
</tr>
<tr>
<td>Concurrent connections</td>
<td>200,000/Anti-DDoS Advanced instance</td>
<td>The number of concurrent connections per second for each Anti-DDoS Advanced instance</td>
</tr>
</table>

The metrics above are only applicable to instances purchased on Tencent Cloud official website. If you find these limits restrictive, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.


## Billing Examples
The following example describes how an Anti-DDoS Advanced instance is billed using the combo billing mode.
Suppose a user purchases an Anti-DDoS Advanced instance in the Singapore region for 20 Gbps base protection bandwidth and 50 Gbps elastic protection bandwidth.
Suppose DDoS attacks occur with a peak attack bandwidth of 40 Gbps, which exceeds the base protection bandwidth and triggers elastic protection. The peak attack bandwidth falls into the billing tier between 40 Gbps and 50 Gbps. The elastic protection fee generated that day will be 800 USD.
The user will need to pay a total of 6,350 USD, of which 4,800 USD will be the monthly base protection fee, 750 USD will be the monthly fee for 50 Mbps application bandwidth, and 800 USD will be the elastic protection fee generated that day.
