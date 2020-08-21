## Billing Description
**Tencent Cloud Direct Connect is billed on the basis of connection, dedicated tunnel, and direct connect gateway.**
The figure below specifies the fees:
![](https://main.qcloudimg.com/raw/810dbbd6163c5f19a2d98eac91e0556b.png)

### Connections
A connection is the connection between your local IDC and the Tencent Cloud Direct Connect access point. You need to pay Tencent Cloud billable items and non-Tencent Cloud billable items.
- **Tencent Cloud billable items**
 - The charges for a dedicated access port include initial installation fee and monthly resource occupation fee for the dedicated access port.
 - You do not need to pay the initial installation fee or resource occupation fee for access through a shared access port. 
- **Non-Tencent Cloud billable items**
 - Leased-line fee: you should pay your ISP for the leased line between your local IDC and the Tencent Cloud Direct Connect access point.
 - In-house wiring (IHW) rental fee: Direct Connect access points in non-Tencent properties are generally deployed in neutral IDCs. Therefore, fiber-to-the-building (FTTB) and IHW rental fees may incur. For more information, consult your property operator or wiring provider.

### Dedicated tunnels
A dedicated tunnel is the Tencent Cloud private network connection between the Direct Connect access point and the Tencent Cloud direct connect gateway.
- If the Direct Connect access point and direct connect gateway are deployed in the same region, dedicated tunnels will be free of charge before May 1, 2020. After then, a free tier of 10 Gbps will be provided. If you require a higher bandwidth, contact your Tencent Cloud rep.
- If the Direct Connect access point and direct connect gateway are deployed in different regions, cross-region communication over the private network will be charged for dedicated tunnels, and no free tier will be provided.

## Direct connect gateways
A Direct Connect gateway is your gateway object in Tencent Cloud, and a fee will be incurred by the traffic passing through it.
- Inbound traffic fee: traffic from your local IDC to a Tencent Cloud IDC over Direct Connect is free of charge.
- Outbound traffic fee: traffic from a Tencent Cloud IDC to your local IDC over Direct Connect is charged based on actual traffic usage at a rate of 0.015 USD/GB.


## Pricing Description
Direct Connect is billed as follows.
![](https://main.qcloudimg.com/raw/4c62cd77dd8aef1097bba22958055f47.png)

### Dedicated access port fee
- **Initial installation fee:** one-time access fee of USD 2,500.
- **Resource occupation fee for dedicated access port:** monthly pay-as-you-go. The fee incurred in the current month will be charged from your account between 8 and 10 AM on the first day of the next month.
- **Billing time**: the billing starts on the day when the connection is in "operating" status, and stops when the connection is deleted on the [Direct Connect Console](https://console.cloud.tencent.com/dc/dc). The connection used within one month will be billed on the basis of valid days (number of billable days in the current month / number of calendar days in the current month).

<table>
<tr><th>Billable Item</th><th>Access Port Specification</th><th>Tencent Cloud International (USD/month)</th></tr>
<tr><td rowspan=3>Resource occupation fee (Chinese mainland)</td><td>1 GbE or below </td><td>90</td></tr>
<tr><td>10 GbE<td>746 </td></tr>
<tr><td>100 GbE</td><td>5,224 </td></tr>
<tr><td rowspan=3>Resource occupation fee (outside Chinese mainland)</td><td>1 GbE or below</td><td>224 </td></tr>
<tr><td>10 GbE<td>1,642</td></tr>
<tr><td>100 GbE</td><td>11,940</td></tr>
</table>

 >?Resource occupation fee for dedicated access port was charged starting July 1, 2019.

### Direct connect gateway traffic fee
For a direct connect gateway, outbound traffic is charged at the price as shown below.

| Billable Item | Price |
| ------------ | -------- |
| Inbound traffic | Free of charge |
| Outbound traffic | 0.015 USD/GB |

>?Outbound traffic fee will be charged starting November 1, 2020.

### Cross-region dedicated tunnel bandwidth resource fee
#### Monthly 95th percentile billing
Monthly dedicated tunnel fee = number of valid days in the month / number of calendar days in the month * 95th percentile of the monthly peak bandwidth * tiered unit price.
- **5-minute bandwidth value**
 The system collects the higher value of the inbound and outbound bandwidth on the devices every minute, and calculates the average in the last five minutes once every five minutes. The average is recorded as the 5-minute bandwidth value.
- **Valid day**
 A valid day is a day in which at least one 5-minute bandwidth value is greater than 3 Kbps.
- **Proportion of valid days**
Proportion of valid days = number of valid days in the month / number of calendar days in the month
- **95th percentile of the monthly peak bandwidth**
 In a calendar month, the 5-minute bandwidth values on all valid days are sorted in ascending order, and the top 5% are removed. The highest value of the remaining sample points is used as the 95th percentile of the monthly peak bandwidth.
- **Tiered unit price**
 Non-accumulative tiered pricing.

#### Tiered unit prices for 95th percentile of the monthly peak bandwidth
In Chinese mainland, the **pay-as-you-go** billing mode applies at the price as shown below.

| Specification (Mbps)    | Monthly Fee (USD/Mbps) |
| --------------- | --------------- |
| [0, 10)         | 85             |
| [10, 20)        | 63             |
| [20, 50)        | 45             |
| [50, 100)       | 34             |
| [100, 200)      | 25             |
| [200, 500)      | 18             |
| [500, 1000)     | 14             |
| [1000, 2000)    | 11             |
| [2000, 1000000) | 10             |

>?
>- For more information on tiered pricing, contact your Tencent Cloud rep.
>- Communication over the Beijing-Tianjin and Guangzhou-Shenzhen dedicated tunnels is free of charge before December 31, 2020.
