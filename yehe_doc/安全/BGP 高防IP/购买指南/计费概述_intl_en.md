## Billing Modes
Anti-DDoS Advanced uses mixed billing modes, which include monthly subscription and pay-as-you-go. Specifically, base protection bandwidth, business bandwidth, and forwarding rules are prepaid on a monthly basis, while elastic protection bandwidth is pay-as-you-go on a daily basis.

<table>
<tr>
<th width = "15%">Billable Item</th>
<th width = "15%">Billing Mode</th>
<th width = "9%">Payment Mode</th>
<th>Billing Description</th>
</tr>
<tr>
<td >Base protection bandwidth</td>
<td>Monthly subscription</td>
<td>Prepaid</td>
<td>This provides basic protection bandwidth at a prepaid price determined by the base protection bandwidth and the purchase duration. After the purchase is made, the prepayment will be frozen and settled on the 1st day of the following month.</td>
</tr>
<tr>
<td >Elastic protection bandwidth</td>
<td>Daily</td>
<td>Pay-as-you-go</td>
<td>After the elastic protection is triggered, it will be billed based on the bandwidth range corresponding to the attack bandwidth peak on that day, and the bill will be generated the following day. If elastic protection is not triggered, no fees will be charged. You can increase or decrease the elastic protection bandwidth as needed.</td>
</tr>
<tr>
<td >Forwarding rule</td>
<td>Monthly subscription</br>Bill-by-rule</td>
<td>Pay-as-you-go</td>
<td>60 forwarding rules are provided for each Anti-DDoS Advanced instance free of charge by default. Every 10 extra rules are charged at 100 USD/month, and each Anti-DDoS Advanced instance can support up to 500 forwarding rules.</td>
</tr>
<tr>
<td >Business bandwidth</td>
<td>Monthly subscription</br>Bill-by-bandwidth</td>
<td>Prepaid</td>
<td>It refers to the bandwidth used by the business traffic forwarded to the real server after cleansing and is free of charge within 100 Mbps. If the free tier is exceeded, please increase your business bandwidth in time.</td>
</tr>
</table>

### Base protection
Base protection is prepaid on a monthly basis. The specific prices are as detailed below:

| DDoS Protection Capability | Non-BGP | BGP | Outside Mainland China |
|---------|---------|---------|---------|
| 20 Gbps | - | 1,000 USD/month | 4,800 USD/month |
| 30 Gbps | - | - | 7,000 USD/month |
| 40 Gbps | - |- | 8,200 USD/month |
| 50 Gbps | 4,000 USD/month</br>25,000 USD/year | 4,500 USD/month</br>35,000 USD/year | 10,500 USD/month |
| 100 Gbps | 40,000 USD/year | 50,000 USD/year | 198,000 USD/year|
| 300 Gbps | 60,000 USD/year | 65,000 USD/year | - |

>
- The non-BGP service covers China Telecom, China Unicom, and China Mobile. After you purchase non-BGP, 3 protected IPs (each for China Telecom, China Unicom, and China Mobile, respectively) will be provided.
- Outside Mainland China: Hong Kong (China), Taiwan (China), Singapore, Seoul, Tokyo, and Virginia.


<span id="txfh"></span>
### Elastic protection
You can enable elastic protection based on your actual business protection needs.
- If elastic protection is not enabled, the highest protection capability will be the base protection bandwidth and no postpaid fees will be incurred.
- If elastic protection is enabled, the instance's highest protection capability will be the elastic protection bandwidth.
 - If elastic protection is not triggered, no fees will be incurred.
 - If elastic protection is triggered (i.e., the attack bandwidth exceeds the base protection bandwidth but is within the elastic protection bandwidth), fees will be charged based on the billing tier corresponding to the actual attack traffic peak on the day and a bill will be generated the next day.

The specific prices of elastic protection are as detailed below:

| Elastic Protection Billing Tier | Non-BGP (USD/Day) | BGP (USD/Day) | Outside Mainland China (USD/Day) |
| -------------------- | ------------------- | ------------------- |------------------- |
| 20 Gbps ≤ Attack bandwidth peak < 30 Gbps   | -               | 260               | 400               |
| 30 Gbps ≤ Attack bandwidth peak < 40 Gbps   | -               | 450               | 700               |
| 40 Gbps ≤ Attack bandwidth peak < 50 Gbps   | -               | 600               | 800               |
| 50 Gbps ≤ Attack bandwidth peak < 60 Gbps   | 800               | 800               | 1,200               |
| 60 Gbps ≤ Attack bandwidth peak < 70 Gbps   | 1,200               | 1,200               | 1,800              |
| 70 Gbps ≤ Attack bandwidth peak < 80 Gbps   | 1,500               | 1,500               | 2,200              |
| 80 Gbps ≤ Attack bandwidth peak < 90 Gbps   | 1,700               | 1,700               | 2,500              |
| 90 Gbps ≤ Attack bandwidth peak < 100 Gbps  | 1,900              | 1,900              | 2,700              |
| 100 Gbps ≤ Attack bandwidth peak < 120 Gbps | 2,100              | 2,100              | 2,900              |
| 120 Gbps ≤ Attack bandwidth peak < 150 Gbps | 2,300               | 2,300              | 3,200              |
| 150 Gbps ≤ Attack bandwidth peak < 200 Gbps | 2,700               | 2,700              | 4,000              |
| 200 Gbps ≤ Attack bandwidth peak < 250 Gbps | 4,800              | 4,800              | 4,800              |
| 250 Gbps ≤ Attack bandwidth peak < 300 Gbps | 5,600              | 5,600              | 5,600              |
| 300 Gbps ≤ Attack bandwidth peak < 400 Gbps | -             | -                   | 6,600              |
| 400 Gbps ≤ Attack bandwidth peak < 600 Gbps | -           | -                   | -            |
| 600 Gbps ≤ Attack bandwidth peak < 900 Gbps |  -              | -                   | -            |
| 900 Gbps ≤ Attack bandwidth peak < 1.2 Tbps | -                 | -                   | -            |

### Forwarding rule
| Number of Rules | Price (USD/Month/10 Rules) |
| --------------------------- | ------------------ |
| Number of ports (or protected domain name) ≤ 60 | Free of charge |
| Number of ports (or protected domain name) > 60 | 100 |

>Number of forwarding rules refers to the number of TCP/UDP ports that can be added in non-website access configuration or HTTP/HTTPS domain names that can be added in website access configuration for an Anti-DDoS Advanced instance. The number of forwarding rules of an Anti-DDoS Advanced instance is the total number of forwarding rules in the two aforementioned access methods.

### Business bandwidth
Business bandwidth refers to the bandwidth used by normal business traffic forwarded to the real server's data center after being cleansed in the Tencent Cloud Anti-DDoS data center.
Currently, the prepaid monthly subscription billing mode is supported. The specific prices are as detailed below:

| Bandwidth	| Unit Price (USD/Month) |
|-|-|
|50 Mbps|750 |
|100 Mbps	|1,500 |
|150 Mbps	|2,250 |
|200 Mbps|	3,000	|
|500 Mbps	|7,500	|
|1 Gbps|	15,000	|
|2 Gbps	|30,000 |

The relationship between the bandwidth and number of layer-7 requests is as shown below:

| Business Bandwidth | HTTP | HTTPS |
| -------- | -------- | -------- |
| 50 Mbps | 1,500 QPS | 1,500 QPS |
| 100 Mbps | 3,000 QPS | 3,000 QPS |
| 150 Mbps | 5,000 QPS | 3,500 QPS |
| 200 Mbps | 7,000 QPS | 4,000 QPS |
| 500 Mbps | 20,000 QPS | 7,000 QPS |
| 1 Gbps | 40,000 QPS | 10,000 QPS |
| 2 Gbps | 70,000 QPS | 17,000 QPS |

>
>- Limit on the business traffic takes account of both the inbound direction (Anti-DDoS forwarding traffic) and outbound direction (Anti-DDoS outbound traffic). The business bandwidth needs to be higher than the bandwidth peak of the business inbound or outbound traffic, whichever is greater. If the actual business bandwidth is continuously above the **business bandwidth** set when you purchase the Anti-DDoS Advanced instance, packet loss may occur, which will affect the business. Therefore, you are recommended to adjust the business bandwidth promptly.
>- Here, QPS means the number of normal business requests per second when there are no attacks. If your normal business request quantity exceeds the purchased Anti-DDoS Advanced instance specification, please adjust the specification promptly so as to avoid impact on your business due to packet loss. You can adjust the business bandwidth reasonably and increase the normal HTTP/HTTPS QPS based on the relationship between the bandwidth and the number of layer-7 requests as shown in the table above.

## Other Specifications
Other specifications are as detailed below:
<table>
<tr>
<th width = "20%">Specification Name</th>
<th width = "30%">Specification Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Number of forwarding ports</td>
<td rowspan="2">60–500 ports/protected IP</td>
<td rowspan="2">Total number of forwarding rules for TCP/UDP and HTTP/HTTPS protocols. For TCP and UDP protocols, if the same forwarding port number is used, you need to configure two forwarding rules.</td>
</tr>
<tr>
<td>Number of supported domain names</td>
</tr>
<tr>
<td>Number of real server IPs</td>
<td> 20 IPs/instance</td>
<td>Total number of layer-4 and layer-7 real server IP addresses</td>
</tr>
<tr>
<td>Number of new connections per second</td>
<td>50,000 connections/protected IP</td>
<td>Number of newly established connections per second for one protected IP</td>
</tr>
<tr>
<td>Number of concurrent connections</td>
<td>200,000 connections/protected IP</td>
<td>Number of concurrent connections for one protected IP</td>
</tr>
</table>

>The specifications above are only applicable to instances purchased on Tencent Cloud official website. If they cannot meet your business needs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
