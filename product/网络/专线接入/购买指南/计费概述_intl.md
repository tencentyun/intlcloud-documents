**Tencent Cloud Direct Connect access charges include charges for both the connection and dedicated tunnel.**
### Connection
This is the connection from your local IDC to the Tencent Cloud Direct Connect access point. Costs include Tencent Cloud charges and non-Tencent Cloud charges.
- **Tencent Cloud charges**
- The charges for a dedicated access port include initial installation fee and monthly resource occupation fee for dedicated access port.
- For access via a shared access port by partners, you only need to pay for the outbound traffic. You don't have to worry about initial installation charge and resource occupation fee for dedicated access Port.
- **Non-Tencent Cloud charges**
- Leased-line fee: You should pay your ISP for the leased line from your local IDC to the Tencent Cloud Direct Connect access point.
- In-house wiring (IHW) rental fee: Direct Connect access points in non-Tencent properties are generally deployed in neutral IDCs, and IHW rental fees may apply. For more information, consult your property operator or wiring provider.

### Dedicated Tunnel
A dedicated tunnel is the private connection from the Tencent Cloud Direct Connect access point to the Tencent Cloud Direct Connect gateway.
- If the Direct Connect access point and Direct Connect gateway are deployed in the same region, dedicated tunnels are free of charge before May 1, 2020.
- If the Direct Connect access point and Direct Connect gateway are deployed in different regions, cross-region communication over private network is charged for dedicated tunnels.

## Pricing
### Resource Occupation Fee for Dedicated Access Port
- **Initial installation fee:** One-time access fee of $2,500 US dollars.
- **Resource occupation fee for dedicated access port: Pay-as-you-go.**
<table>
<tr><th>Charged item</th><th>Access port specifications</th></th><th>Tencent Cloud International (USD/month)</th></tr>
<tr><td rowspan=3>Resource usage fee (Mainland China)</td><td>1 GE or below </td><td>90</td></tr>
<tr><td>10 GE<td>746</td></tr>
<tr><td>100 GE</td><td>5,224 </td></tr>
<tr><td rowspan=3>Resource usage fee (global)</td><td>1 GE or below</td><td>224</td></tr>
<tr><td>10 GE<td>1,642 </td></tr>
<tr><td>100 GE</td><td>11,940</td></tr>
</table>

 >Resource occupation for dedicated access port will start charging fees from July 1, 2019.

### Resource Traffic Fee for Shared Access Port by Partners
For resource of shared access port by partners, only outbound traffic is charged at the price as shown in the table below:

| Charged item | Price |
|--------| ----|
| Outbound traffic | 0.015 USD/GB |

>Outbound traffic is free of charge before May 1, 2020.

### Dedicated Tunnel Bandwidth Resource Fee
- **Monthly 95th percentile billing:**
Monthly dedicated tunnel fee = valid day proportion \* monthly 95th percentile bandwidth value \* tiered unit price.
- **Definitions:**
- 5-minute bandwidth value
 The system counts the inbound and outbound bandwidth values on the devices every minute, takes the higher value, and calculates the average in the past five minutes once every five minutes, which is recorded as the 5-minute bandwidth value.
- Valid day
 A day when there is one 5-minute bandwidth value greater than 3 Kbps is considered a valid day.
- Valid day proportion
 Valid day proportion = valid days in the month / calendar days in the month.
- Monthly 95th percentile bandwidth value
 In a calendar month, the 5-minute bandwidth values on all valid days are counted and sorted in ascending order, the highest 5% values are removed, and the remaining highest value is used as the monthly 95th percentile bandwidth value.
- Tiered unit price
 Non-accumulative tiered pricing.
- **Billing example for a dedicated tunnel:**
There are 14 valid days of dedicated tunnel usage in January. As there are 24 \* 60 / 5 = 288 sample points per day, the total number of sample points in the 14 days are 14 \* 288 = 4,032. The bandwidth values of the 4,032 points are sorted in ascending order, the first 5% values are removed, and the bandwidth value of the 3,830th point (4032 \* 0.95 = 3830.4) is used as the billable bandwidth value for the month, which is recorded as Max95. The fee for January is Max95 \* 14/31 \* tiered unit price.
- **Tiered unit price:**
 **Pay-as-you-go** billing method is used in Mainland China at the prices as shown in the table below:

| Tier (Mbps) | Monthly fee (USD/Mbps) |
| --------------- | ---------------------- |
| [0, 10)         | 85                    |
| [10, 20)        | 63                    |
| [20, 50)        | 45                    |
| [50, 100)       | 34                    |
| [100, 200)      | 25                    |
| [200, 500)      | 18                    |
| [500, 1000)     | 14                     |
| [1000, 2000)    | 11                     |
| [2000, 1000000) | 10                     |

>- For more information about tiered pricing, contact your Tencent Cloud sales representative.
>- Beijing-to-Tianjin and Guangzhou-to-Shenzhen dedicated tunnels are free of charge before December 31, 2019.
