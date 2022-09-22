
ECM has two billable items: **[computing storage](#ComputingStorage)** and **[network bandwidth](#NetworkBandwidth)**.

## Computing Storage[](id:ComputingStorage)
The computing storage service is billed and settled daily by the daily peak usage.

### Calculation cycle
Daily billing: fees for a day are billed and charged in the morning the next day.

### Calculation formula
Daily fees = daily peak resource usage * resource unit prices

- **Daily peak resource usage:** maximum usage of resources such as CPU, memory, and storage from 00:00 to 24:00 on a day. Resources you add before midnight every day will be included in the calculation of the daily peak resource usage and increase the total daily fees.
For example, if you create a resource or create and immediately terminate a resource at 23:59:58, both operations will increase the daily fees.
**You should pay attention to the time point when you create a resource to avoid losses caused by creating resources too late on a day or maloperations.**
- **Resource unit prices:** unit prices of resources such as CPU, memory, and storage of instances on the edge node.



### Pricing

|   Resource Type   | Price   |
| -------- | --------- |
| CPU (cores)  |      2 CNY/core/day   |
| Memory (GB) |   0.63333 CNY/GB/day   |
| Storage (GB) |   0.01167 CNY/GB/day   |


### Pricing examples
At 10:00 on August 1, 2020, a user created two Standard S4 instances with the same configuration on an edge node in Beijing Zone 1 (China Mobile). The instance configuration was as follows:

- Number of CPU cores: 8
- Memory: 16 GB
- System disk storage: 50 GB
- Data disk storage: 300 GB

At 14:00 on August 1, 2020, the user created three Standard SN3ne instances with the same configuration on an edge node in Shanghai Zone 2 (China Unicom). The instance configuration was as follows:

- Number of CPU cores: 4
- Memory: 8 GB
- System disk storage: 50 GB
- Data disk storage: 200 GB

At 22:00 on August 1, 2020, the user terminated an instance in Shanghai Zone 2 (China Unicom).

Therefore, the computing resource usage of the user reached the daily maximum value at 14:00 on that day as detailed below:

- CPU: 8 * 2 + 4 * 3 = 28 cores
- Memory: 16* 2 + 8 * 3 = 56 GB
- Storage: 350 * 2 + 250 * 3 = 1450 GB

Resource unit prices: 2 CNY/core/day (CPU), 0.63333 CNY/GB/day (memory), and 0.01167 CNY/GB/day (storage). The daily fees were calculated by the peak usage value of each resource.

The fees incurred by the user on August 1, 2020 were 28 * 2 + 56 * 0.63333 + 1450 * 0.01167 = 108.39 CNY/day and were charged in the morning the next day.

## Network Bandwidth[](id:NetworkBandwidth)

The network bandwidth service is billed monthly by the 95th percentile of the monthly peak bandwidth counted by the ISP on each edge node.

### Calculation cycle
Monthly billing: the fees are charged in the morning the first day of the calendar month immediately after the current billing cycle. For example, the network bandwidth bill in May (between 2020-05-01 00:00:00 and 2020-05-31 23:59:59) is generated on June 1.

### Calculation formula
Monthly fees = 95th percentile of monthly peak bandwidth * proportion of valid days * bandwidth unit price of node ISP

- **95th percentile of monthly peak bandwidth:** the average 10-second outbound bandwidth value and inbound bandwidth value of a node are calculated once every 5 minutes, the peak inbound bandwidth value and peak outbound bandwidth value in 5 minutes are taken, and the greater of the two is used as a sample point. During monthly settlement, all sample points collected once every 5 minutes in that month are sorted in descending order, the top 5% of the sample points are removed, and the highest one among the remaining sample points is used as the 95th percentile of monthly peak bandwidth of the node.
For example, you use the network bandwidth service on an edge node for 14 valid days in June. As one sample point is generated every 5 minutes, 288 (60 min * 24 / 5 min) sample points are generated every day, and 4,032 (14 days * 288 sample points/day) sample points are generated in 14 days. The bandwidth values of the 4,032 sample points are sorted in descending order, the top 5% of the sample points (4032 * 0.05 = 201.6 sample points) are removed, and the bandwidth value of the 202nd sample point is taken as the 95th percentile of monthly peak bandwidth.
- **Proportion of valid days:** a valid day is a day on which the bandwidth value of at least one sample point is higher than 1 Kbps.
    Proportion of valid days: number of valid days / number of days in the billed month.
- **Node ISP bandwidth unit price:** it is the bandwidth unit price of the ISP in the node region. The following ISPs are supported: China Telecom, China Unicom, and China Mobile.

### Pricing

<table>
	<tr><th>Region</th><th>China Telecom Bandwidth Price</th><th>China Unicom Bandwidth Price</th><th>China Mobile Bandwidth Price</th></tr>
	<tr><td><ul  style="margin: 0;"><li>Beijing</li><li>Shanghai</li><li>Guangzhou</li></ul></td><td>40 CNY/Mbps/month</td><td>35 CNY/Mbps/month</td><td>20 CNY/Mbps/month</td></tr>
	<tr><td>Hangzhou</td><td>40 CNY/Mbps/month</td><td>19 CNY/Mbps/month</td><td>14 CNY/Mbps/month</td></tr>
	<tr><td>Other regions</td><td>21 CNY/Mbps/month</td><td>19 CNY/Mbps/month</td><td>14 CNY/Mbps/month</td></tr>
</table>

### Pricing examples

In June 2020 (30 days), a user generated network bandwidth above 1 Kbps for 14 days on a China Telecom node in Beijing, and the 95th percentile of monthly peak bandwidth was 60 Mbps, then in that month:
- Proportion of valid days: 14 / 30 = 0.4667
- Node ISP bandwidth unit price: 40 CNY/Mbps/month
- China Telecom bandwidth fees in June: 60 * (14/ 30) * 40 = 1120 CNY

The system charged the user in the morning on July 1, 2020.

## Other Services

When creating an ECM instance, you can choose to activate CWPP and CM free of charge.
- CWPP: you can install the agent to activate CWPP Basic.
- CM: CM supports monitoring, analysis, and alarming for Tencent Cloud services. You can install the agent to get server monitoring metrics.
