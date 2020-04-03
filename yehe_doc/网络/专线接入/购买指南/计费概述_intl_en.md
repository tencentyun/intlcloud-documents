## Billing Description
**Tencent Cloud Direct Connect is billed on the basis of connection, dedicated tunnel, and Direct Connect gateway.**

### Connection
A connection is the connection between your local IDC and the Tencent Cloud Direct Connect access point. You need to pay Tencent Cloud billable items and non-Tencent Cloud billable items.
- **Tencent Cloud billable items**
 - The charges for application for a dedicated access port include initial installation fee and monthly resource occupation fee for the dedicated access port.
 - For access through a shared access port by partners, you don't need to pay the initial installation fee and resource occupation fee for the dedicated access port.
- **Non-Tencent Cloud billable items**
 - Leased-line fee: you should pay your ISP for the leased line from your local IDC to the Tencent Cloud Direct Connect access point.
 - In-house wiring (IHW) rental fee: Direct Connect access points in non-Tencent properties are generally deployed in neutral IDCs, and fiber-to-the-building (FTTB) and IHW rental fees may be incurred. For more information, please consult your property operator or wiring provider.

### Dedicated tunnel
A dedicated tunnel is the Tencent Cloud private network connection between the Direct Connect access point and the Tencent Cloud Direct Connect gateway.
- If the Direct Connect access point and Direct Connect gateway are deployed in the same region, dedicated tunnels will be free of charge before May 1, 2020. After then, a free tier of 10 Gbps will be provided, and if you require higher bandwidth, please contact your Tencent Cloud rep.
- If the Direct Connect access point and Direct Connect gateway are deployed in different regions, cross-region communication over the private network will be charged for dedicated tunnels, and no free tier will be provided.

### Direct Connect gateway
A Direct Connect gateway is your gateway object in Tencent Cloud, and a fee will be incurred by the traffic passing through it.
- Inbound traffic: traffic from your local IDC to a Tencent Cloud IDC over Direct Connect is free of charge.
- Outbound traffic: traffic from a Tencent Cloud IDC to your local IDC over Direct Connect is charged based on the actual traffic usage at 0.015USD/GB.


## Pricing Description
Direct Connect is billed as follows:

### Dedicated access port fee
- **Initial installation fee:** one-time access fee of USD 2,500.
- **Resource occupation fee for dedicated access port:** monthly pay-as-you-go. The fee incurred in the current month will be charged from your account between 8 and 10 AM on the first day next month.
<table>
<tr><th>Billable Item</th><th>Access Port Specification</th><th>Tencent Cloud International (USD/month)</th></tr>
<tr><td rowspan=3>Resource occupation fee (Mainland China)</td><td>1 GbE or below </td><td>90</td></tr>
<tr><td>10 GbE<td>746 </td></tr>
<tr><td>100 GbE</td><td>5,224 </td></tr>
<tr><td rowspan=3>Resource occupation fee (outside Mainland China)</td><td>1 GbE or below</td><td>224 </td></tr>
<tr><td>10 GbE<td>1,642</td></tr>
<tr><td>100 GbE</td><td>11,940</td></tr>
</table>

 >Resource occupation fee for dedicated access port was charged starting July 1, 2019.

### Direct Connect gateway traffic fee
For a Direct Connect gateway, outbound traffic is charged at the price as shown below:

| Billable Item | Price |
| ------------ | -------- |
| Inbound traffic | Free |
| Outbound traffic | 0.015 USD/GB |

>Outbound traffic fee will be charged starting November 1, 2020.

### Cross-region dedicated tunnel bandwidth resource fee
#### Monthly 95th percentile billing
Monthly dedicated tunnel fee = valid days in the month / calendar days in the month * monthly 95th percentile of peak bandwidth * tiered unit price.
- **5-minute bandwidth value**
 The system collects the inbound and outbound bandwidth values on the devices once every minute, takes the higher one of them, and calculates the average in the last five minutes once every five minutes. The average is recorded as the 5-minute bandwidth value.
- **Valid day**
 A day when there is a 5-minute bandwidth value greater than 3 Kbps is considered a valid day.
- **Valid day proportion**
Valid day proportion = valid days in the month / calendar days in the month.
- **Monthly 95th percentile of peak bandwidth**
 In a calendar month, the 5-minute bandwidth values on all valid days are counted and sorted in ascending order, the highest 5% ones are discarded, and the remaining highest one is used as the monthly 95th percentile of peak bandwidth.
- **Tiered unit price**
 Non-accumulative tiered pricing.

#### Tiered unit prices for monthly 95th percentile of peak bandwidth
**Pay-as-you-go** billing mode is used in regions outside Mainland China at the prices as shown below:

| Specification (Mbps)    | 	Monthly Fee (USD/Mbps) |
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

>
>- For more information on tiered pricing, please contact your Tencent Cloud rep.
>- Communication over the Beijing-Tianjin and Guangzhou-Shenzhen dedicated tunnels is free of charge before December 31, 2020.

