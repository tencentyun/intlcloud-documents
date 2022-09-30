Tencent Cloud Anti-DDoS Advanced has adopted new billing rules from **March 24, 2022**.
## Billing Mode
Anti-DDoS Advanced adopts a combo billing mode of monthly subscription and pay-as-you-go. Specifically, base protection bandwidth, application bandwidth and forwarding rules are billed monthly, while elastic protection bandwidth and application bandwidth in excess of the plan are billed daily.

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
<td>Pay-as-you-go on a daily basis</td>
<td>Pay-as-you-go</td>
<td>Charges will be incurred only when elastic protection is triggered. Once it is triggered, you will be billed at the tier corresponding to the amount of usage for the current day (Peak attack bandwidth – Base protection bandwidth) and settled on the following day. You can customize the configuration to meet your protection needs.</td>
</tr>
<tr>
<td >Forwarding rules</td>
<td> <ul><li/>Monthly subscription<li/>Billed by forwarding rules</ul></td>
<td>Pay-as-you-go</td>
<td>60 forwarding rules are provided for free for each Anti-DDoS Advanced instance by default. Every additional 10 rules costs USD 100 per month. Each instance can have up to 500 forwarding rules.</td>
</tr>
<tr>
<td >Application bandwidth</td>
<td><ul><li/>Monthly subscription<li/>Billed by bandwidth<li/>Pay-as-you-go on a daily basis</ul></td>
<td>Pay-as-you-go</td>
<td><ul style="margin:0"><li/>The application bandwidth limit applies to both the inbound Anti-DDoS forwarding traffic and the outbound Anti-DDoS traffic. The application bandwidth needs to be higher than the peak bandwidth of the two, whichever is greater.<li/>When the application bandwidth is insufficient or a higher QPS is needed, you can upgrade or enable elastic application bandwidth; otherwise, packet loss or business impact may occur.<li/>After elastic application bandwidth is enabled, bandwidth in excess of the preset specification will be charged at 1 USD/Mbps/day. Please select the specification after reasonably assessing your application bandwidth scale.</ul></td>
</tr>
</table>


### Base protection
The basic protection service is billed based on your monthly plan. See the following table for detailed prices.

#### Regions in the Chinese mainland

| Base Protection Capacity | Non-BGP        | BGP                      |
| ------------- | ----------- | ------------------------ |
| 30 Gbps        | -           | 3,300 USD/month              |
| 60 Gbps        | 7,200 USD/month | 7,200 USD/month              |
| 100 Gbps       | 7,800 USD/month | 7,800 USD/month              |
| 300 Gbps       | 8,470 USD/month | 8,470 USD/month              |
| 500 Gbps       | -           | 614,000 USD/year            |
| 800 Gbps       | -           | 831,000 USD/year            |
| 1,000 Gbps      | -           | 997,000 USD/year            |

#### Regions outside the Chinese mainland

| Base Protection Capacity | Anti-CC Protection Cap | Price           |
| ------------- | ----------- | -------------- |
| 20 Gbps        | 40,000 QPS   | 4,800 USD/month    |
| 50 Gbps        | 150,000 QPS  | 10,500 USD/month  |
| 100 Gbps       | 300,000 QPS  | 198,000 USD/year |

>?
>- "Non-BGP" refers to China Mobile/China Union/China Telecom network services. A non-BGP plan includes three Anti-DDoS Advanced instances, one for each of the network services.
>- "Outside the Chinese mainland" refers to Tencent Cloud regions outside the Chinese mainland, namely, Hong Kong (China), Taiwan (China), Singapore, Seoul, Tokyo, Virginia, Silicon Valley and Frankfurt.


<span id="txfh"></span>
### Elastic protection
You can enable elastic protection as needed.
#### Regions in the Chinese mainland
- If elastic protection is not enabled for an instance, its maximum protection will be the base protection bandwidth, and no extra fees will be incurred.
- If elastic protection is enabled for an instance, its maximum protection will be the selected elastic protection bandwidth.
  - If elastic protection is not triggered, no charges will be incurred.
  - Elastic protection will be triggered when the peak attack traffic exceeds the base protection bandwidth. You will be billed at the tier corresponding to the amount of usage for the current day (Peak attack bandwidth – Base protection bandwidth) and settled on the following day.

>?
>- Elastic bandwidth cap is the overall amount of multiple ISP bandwidth limits. Note that attack traffic exceeding one of the limits may be blocked even if the overall cap is not reached.
>-  Billable elastic bandwidth = Peak attack bandwidth – Base protection bandwidth

The detailed pricing of elastic protection is as follows:

| Billing Tier                   | Non-BGP/BGP (USD/Day) |
| ------------------------------ | ------------------- |
| 0 Gbps ≤ Billable elastic bandwidth < 5 Gbps     | 130                 |
| 5 Gbps ≤ Billable elastic bandwidth < 10 Gbps    | 170                 |
| 10 Gbps ≤ Billable elastic bandwidth < 20 Gbps   | 340                 |
| 20 Gbps ≤ Billable elastic bandwidth < 30 Gbps   | 590                 |
| 30 Gbps ≤ Billable elastic bandwidth < 40 Gbps   | 800                 |
| 40 Gbps ≤ Billable elastic bandwidth < 50 Gbps   | 950                 |
| 50 Gbps ≤ Billable elastic bandwidth < 60 Gbps   | 1,100                |
| 60 Gbps ≤ Billable elastic bandwidth < 70 Gbps   | 1,250                |
| 70 Gbps ≤ Billable elastic bandwidth < 80 Gbps   | 1,400                |
| 80 Gbps ≤ Billable elastic bandwidth < 90 Gbps   | 1,540                |
| 90 Gbps ≤ Billable elastic bandwidth < 100 Gbps  | 1,675                |
| 100 Gbps ≤ Billable elastic bandwidth < 120 Gbps | 1,960                |
| 120 Gbps ≤ Billable elastic bandwidth < 150 Gbps | 2,390                |
| 150 Gbps ≤ Billable elastic bandwidth < 200 Gbps | 3,100                |
| 200 Gbps ≤ Billable elastic bandwidth < 250 Gbps | 3,800                |
| 250 Gbps ≤ Billable elastic bandwidth < 300 Gbps | 4,470                |
| 300 Gbps ≤ Billable elastic bandwidth < 400 Gbps | 6,340                |
| 400 Gbps ≤ Billable elastic bandwidth < 600 Gbps | 8,800                |
| 600 Gbps ≤ Billable elastic bandwidth< 900 Gbps  | 14,670               |
| 900 Gbps ≤ Billable elastic bandwidth < 1.2 Tbps | 20,000               |

#### Outside the Chinese mainland

- If elastic protection is not enabled for an instance, its maximum protection will be the base protection bandwidth, and no extra fees will be incurred.

- If elastic protection is enabled for an instance, its maximum protection will be the selected elastic protection bandwidth.

  - If elastic protection is not triggered, no charges will be incurred.
  - Elastic protection will be triggered when the peak attack traffic exceeds the base protection bandwidth. You will be billed at the tier within which the peak attack bandwidth for the current day falls and settled on the following day.

The detailed pricing of elastic protection is as follows:

| Billing Tier                 | Outside the Chinese mainland (USD/day) |
| ---------------------------- | --------------- |
| 20 Gbps ≤ Peak attack bandwidth < 30 Gbps   | 400             |
| 30 Gbps ≤ Peak attack bandwidth < 40 Gbps   | 700             |
| 40 Gbps ≤ Peak attack bandwidth < 50 Gbps   | 800             |
| 50 Gbps ≤ Peak attack bandwidth < 60 Gbps   | 1,200             |
| 60 Gbps ≤ Peak attack bandwidth < 70 Gbps   | 1,800             |
| 70 Gbps ≤ Peak attack bandwidth < 80 Gbps   | 2,200            |
| 80 Gbps ≤ Peak attack bandwidth < 90 Gbps   | 2,500            |
| 90 Gbps ≤ Peak attack bandwidth < 100 Gbps  | 2700            |
| 100 Gbps ≤ Peak attack bandwidth < 120 Gbps | 2900            |
| 120 Gbps ≤ Peak attack bandwidth < 150 Gbps | 3200            |
| 150 Gbps ≤ Peak attack bandwidth < 200 Gbps | 4000            |
| 200 Gbps ≤ Peak attack bandwidth < 250 Gbps | 4800            |
| 250 Gbps ≤ Peak attack bandwidth < 300 Gbps | 5600            |
| 300 Gbps ≤ Peak attack bandwidth < 400 Gbps   | 6,600            |

>? Elastic bandwidth cap is the overall amount of multiple ISP bandwidth limits. Note that attack traffic exceeding one of the limits may be blocked even if the overall cap is not reached.

### Forwarding rules

| Number of Forwarding Rules                      |  Price (USD/month/10 rules) |
| --------------------------- | ------------------ |
| Number of ports (or protected domain names) ≤ 60  | Free               |
| Number of ports (or protected domains)  > 60 | 100                |

>? "Forwarding rules" is the total number of TCP/UDP ports (for non-website applications) and HTTP/HTTPS domain names configured (for website applications) that you configure for an Anti-DDoS Advanced instance.

### Application bandwidth
Application bandwidth is the bandwidth used for forwarding the application traffic that has been cleansed by the Tencent Cloud Anti-DDoS data center back to the data center on the real server.
- After elastic application bandwidth is enabled:
  - If elastic application bandwidth is not triggered, only the preset application bandwidth fee will be charged.
  - If elastic application bandwidth is triggered (the actual application bandwidth exceeds the preset application bandwidth), the excessive bandwidth will be billed on a daily basis with bill for day T pushed on day T + 1. The billing rule is excessive bandwidth * 1 USD/Mbps, and the excessive bandwidth is the maximum outbound Anti-DDoS traffic on day T minus the preset application bandwidth specification. If the excess is < 0, no bill will be pushed on day T + 1.
- If elastic application bandwidth is not enabled, the maximum application bandwidth is the preset specification. If it is exceeded, packet loss or business impact may occur, and only the preset application bandwidth fee will be charged as follows:


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
| -------- | ---------- |
| 50 Mbps   | 5,000 QPS   |
| 100 Mbps  | 10,000 QPS  |
| 150 Mbps  | 15,000 QPS  |
| 200 Mbps  | 20,000 QPS  |
| 500 Mbps  | 50,000 QPS  |
| 1,000 Mbps | 100,000 QPS |
| 2,000 Mbps | 200,000 QPS |

>?
>- The application bandwidth is the maximum protection bandwidth for both inbound and outbound traffic. When the actual usage has exceeded the application bandwidth you set for a long period, we recommend increasing the limit before packet loss or service interruption occurs.
>- QPS measures the number of normal application requests per second when there are no attacks. If this number is larger than the application bandwidth you selected when you purchased your Anti-DDoS Advanced instance, we recommend that you increase the HTTP/HTTPS QPS limit promptly to avoid affecting your business due to packet loss. To adjust the application bandwidth, refer to the table above.

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
<td rowspan="2">60-500/Anti-DDoS Advanced instance</td>
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
<td>Concurrent connections</td>
<td>200,000/Anti-DDoS Advanced instance</td>
<td>The number of concurrent connections per second for each Anti-DDoS Advanced instance.</td>
</tr>
</table>

>? The specifications above are only applicable to instances purchased on Tencent Cloud official website. If you want to increase specifications, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Arrears Notification
For Anti-DDoS Advanced instances:
- If the account balance is sufficient, the system will automatically settle the fees for the previous month and deduct them on the 1st of the following month.
- If the account balance is insufficient, the system will remind you to top up the account via the channel you configured (email, SMS, and Message Center).

>!
>- Anti-DDoS Advanced is a pay-as-you-go service that is billed monthly. The minimum subscription term is 1 month. Upon expiry, your subscription will be auto-renewed unless canceled by [contacting us](https://intl.cloud.tencent.com/contact-us). Your instances cannot be terminated during a subscription term.
>- Make sure that you have one-month credit to be frozen when activating this service.
>- Payments for this service are not refundable.

## Service Termination
Anti-DDoS Advanced adopts a pay-as-you-go model. If you want to end the service, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to terminate your instances. Otherwise, charges are still be incurred.
- After you apply for a termination in the current month, the monthly-subscribed items will be settled as usual, while the daily billable items are settled based on the actual usage. After you terminate your instances, the service will be stopped immediately and the instances will no longer be billed for the next month.
- The entire termination takes 1-3 working days to complete and is subject to the actual operation (protection fees may be incurred during the period).
