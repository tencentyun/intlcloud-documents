
## Billing Mode
The billing mode of Anti-DDoS Pro (Enterprise) varies by the region of your application.
- Chinese mainland: Base protection + elastic protection
- Outside the Chinese mainland: Tencent Cloud Anti-DDoS cleansing center provides an all-out protection

>?
>- Chinese mainland regions: Beijing, Shanghai, Guangzhou
>- Outside the Chinese mainland: Hong Kong (China), Singapore, Tokyo, Jakarta, Silicon Valley, Frankfurt, Virginia, São Paulo
>- All-out protection: Integrating the local cleansing capability, the all-out protection aims to spare no effort to successfully defend against each DDoS attack. Tbps-level protection capability is provided in and outside the Chinese mainland.

Anti-DDoS Pro (Enterprise) takes effect only after binding it with an Anti DDoS EIP. You need to change the cloud IP to Anti DDoS EIP. Anti-DDoS Pro (Enterprise) must be located in the same region with the bound cloud resource, and the Anti DDoS EIP is billed when it is created.

The billing details are as below:
<table>
<thead>
<tr>
<th>Region</th>
<th>Parameter</th>
<th>Billing mode</th>
<th>Payment mode</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=2 >Chinese mainland</td>
<td>Base protection bandwidth</td>
<td>Monthly subscription</td>
<td>Prepaid</td>
<td>The fee is calculated based on the base protection bandwidth and how long the service plan you purchased. If you increase the bandwidth, extra fees will occur. Please note that you can only upgrade or keep your current service plan. Downgrade is not supported.</td>
</tr>
<tr>
<td>Elastic protection bandwidth</td>
<td>Pay-as-you-go</td>
<td>Postpaid</td>
<td>Charges will be incurred only when elastic protection is triggered. Once it is triggered, you will be billed at the tier corresponding to the amount of usage for the current day (Peak attack bandwidth – Base protection bandwidth) and settled on the following day. You can customize the configuration to meet your protection needs.</td>
</tr>
<tr>
<td rowspan=2 >In and outside the Chinese mainland</td>
<td rowspan=2 >Application bandwidth</td>
<td>Monthly subscription</td>
<td>Prepaid</td>
<td>The application bandwidth refers to the normal bandwidth of the protected application and is billed by 95th percentile. Anti-DDoS Pro (Enterprise) allows you to exceed your plan’s limit, but the all-out protection capability will become not available and only the basic protection capability remains when the limit has been exceeded for 36 hours accumulatively in a month. The application bandwidth can be increased or decreased, which takes effect in the next month.</td>
</tr>
<tr>
<td>Pay-as-you-go</td>
<td>Postpaid</td>
<td>When elastic application bandwidth is enabled, the amount of bandwidth exceeding the specified amount will be billed. For the price, see <a href="https://www.tencentcloud.com/document/product/1029/55301#yw">Pricing of application bandwidth</a>.</td>
</tr>
</tbody></table>

>?
>- 95th percentile bandwidth: In each calendar month, the inbound/outbound bandwidth is sampled every 5 minutes and the maximum is taken as the peak bandwidth on each day. At the end of the month, the sampled values are sorted from highest to lowest, and the top 5% are removed. The 95th largest value is the billable bandwidth of the month.
>- For a 10-IP plan, 50 Mbps of application bandwidth is offered for free by default.
>- For a 50-IP plan, 300 Mbps of application bandwidth is offered for free by default.
>- For a 100-IP plan, 1,000 Mbps of application bandwidth is offered for free by default.

## Chinese Mainland
### Base protection
Base protection is a postpaid monthly subscription service. See the following table for detailed prices.
<table>
<thead>
<tr>
<th width="10%" and rowspan=2>Base protection bandwidth</th>
<th colspan=3>Monthly list price (USD)</th>
</tr>
<tr>
<th>10-IP plan</th>
<th>50 IPplan</th>
<th>100-IP plan</th>
</tr>
</thead>
<tbody>
<tr>
<td>300G</td>
<td>13333.33 </td>
<td>26666.66 </td>
<td>44444.44 </td>
</tr>
<tr>
<td>400G</td>
<td>22222.22 </td>
<td>44444.44 </td>
<td>84444.44 </td>
</tr>
<tr>
<td>500G</td>
<td>66666.66 </td>
<td>88888.88 </td>
<td>111111.11 </td>
</tr>
<tr>
<td>600G</td>
<td>80000 </td>
<td>111111.11</td>
<td>133333.33 </td>
</tr>
<tr>
<td>800G</td>
<td>88888.88 </td>
<td>133333.33 </td>
<td>177777.77 </td>
</tr>
<tr>
<td>1T</td>
<td>111111.11 </td>
<td>177777.77 </td>
<td>222222.22 </td>
</tr>
</tbody></table>


### Elastic protection
You can enable elastic protection as needed.
- If elastic protection is not enabled for an instance, its maximum protection will be the base protection bandwidth, and no extra fees will be incurred.
- If elastic protection is enabled for an instance, its maximum protection will be the selected elastic protection bandwidth.
  - If elastic protection is not triggered, no charges will be incurred.
  - Elastic protection will be triggered when the peak attack traffic exceeds the base protection bandwidth. You will be billed at the tier corresponding to the amount of usage for the current day (Peak attack bandwidth – Base protection bandwidth) and settled on the following day.

Elastic bandwidth cap is the overall amount of multiple ISP bandwidth limits. Note that blocking may occur when attack traffic exceeds one of the limits even if the overall cap is not reached.
- Billing for postpaid elastic protection of Anti-DDoS Pro (Enterprise): Settled on a calendar day.
- Billable elastic bandwidth = Peak attack bandwidth – Base protection bandwidth

The detailed pricing of elastic protection is as follows:

| Elastic protection bandwidth (Gbps)     | Below 5 IPs (USD) | 5-10 IPs (USD) | 10-20 IPs (USD) | 20-50 IPs (USD) | 50 IPs above (USD) |
| -------------------- | ------------- | ------------ | ------------- | ------------- | -------------- |
| 0＜ Billable elastic bandwidth ≤5     | 130           | 260          | 390          | 520          | 650           |
| 5＜ Billable elastic bandwidth ≤10     | 166.66           | 333.33          | 500          | 666.66          | 833.33           |
| 10＜ Billable elastic bandwidth ≤20     | 333.33           | 666.66          | 1000          | 1333.33          | 1666.66           |
| 20＜ Billable elastic bandwidth ≤30     | 583.33           | 1166.66          | 1750          | 2333.33          | 2916.66           |
| 30＜ Billable elastic bandwidth ≤40     | 800           | 1600          | 2400          | 3200          | 4000           |
| 40＜ Billable elastic bandwidth ≤50     | 950           | 1900          | 2850          | 3800          | 4750           |
| 50＜ Billable elastic bandwidth ≤60     | 1100           | 2200          | 3300          | 4400          | 5500           |
| 60＜ Billable elastic bandwidth ≤70     | 1250           | 2500          | 3750          | 5000          | 6250           |
| 70＜ Billable elastic bandwidth ≤80     | 1391.66           | 2783.33          | 4175          | 5566.66          | 6958.33           |
| 80＜ Billable elastic bandwidth ≤90     | 1533.33           | 3066.66          | 4600          | 6133.33          | 7666.66           |
| 90＜ Billable elastic bandwidth ≤100     | 1675           | 3350          | 5025          | 6700          | 8375           |
| 100＜ Billable elastic bandwidth ≤120     | 1958.33           | 3916.66          | 5875          | 7833.33          | 9791.66           |
| 120＜ Billable elastic bandwidth ≤150     | 2383.33           | 4766.66          | 7150          | 9533.33          | 11916.66           |
| 150＜ Billable elastic bandwidth ≤200     | 3091.66           | 6183.33          | 9275          | 12366.66          | 15458.33           |
| 200＜ Billable elastic bandwidth ≤250     | 3800           | 7600          | 11400          | 15200          | 19000           |
| 250＜ Billable elastic bandwidth ≤300     | 4466.66           | 8933.33          | 13400          | 17866.66          | 22333.33           |
| 300＜ Billable elastic bandwidth ≤400     | 6333.33           | 12666.66          | 19000          | 25333.33          | 31666.66           |
| 400＜ Billable elastic bandwidth ≤600     | 8800           | 17600          | 26400          | 35200          | 44000           |
| 600＜ Billable elastic bandwidth ≤900     | 14666.66           | 29333.33          | 44000          | 58666.66          | 73333.33           |
| 900＜ Billable elastic bandwidth ≤1200     | 20000           | 40000          | 60000          | 80000          | 100000           |

>? When elastic application bandwidth is enabled, and if you want to **disable** it, this will take effect in the next month.

### Pricing of application bandwidth[](id:yw)
The application bandwidth refers to the normal bandwidth of the protected application. It is billed based on monthly 95th percentile by either the outgoing or incoming traffic (whichever is higher).
<table>
<thead>
<tr>
<th  width="20%" rowspan=2>Application bandwidth</th>
<th colspan=3>Unit price (prepaid and postpaid)</th>
</tr>
<tr>
<th>Monthly list price</td>
<th>Yearly list price</td>
<th>37.5% off for yearly subscription</td>
</tr>
</thead>
<tbody>
<tr>
<td>0-1 Gbps (inclusive)</td>
<td>14 USD/Mbps/month</td>
<td>160 USD/Mbps/year</td>
<td>100 USD/Mbps/year</td>
</tr>
<tr>
<td>1-3 Gbps (inclusive)</td>
<td>10 USD/Mbps/month</td>
<td>120 USD/Mbps/year</td>
<td>75 USD/Mbps/year</td>
</tr>
<tr>
<td>3-10 Gbps (inclusive)</td>
<td>7 USD/Mbps/month</td>
<td>80 USD/Mbps/year</td>
<td>50 USD/Mbps/year</td>
</tr>
<tr>
<td>10 Gbps above</td>
<td>4 USD/Mbps/month</td>
<td>40 USD/Mbps/year</td>
<td>25 USD/Mbps/year</td>
</tr>
</tbody></table>

### Calculation formula for elastic application bandwidth
Fee on elastic application bandwidth = (95th percentile of the monthly peak bandwidth - Prepaid application bandwidth) x Unit price

## Outside the Chinese Mainland
### Pricing of protected IPs
<table>
<thead>
<tr>
<th width="50%" rowspan=2>Number of protected IPs</th>
<th colspan=1>Monthly subscription price (USD)</th>
</tr>
<tr>
<th>List price</th>
</tr>
</thead>
<tbody>
<tr>
<td>10 IPs</td>
<td>8890</td>
</tr>
<tr>
<td>50 IPs</td>
<td>17780</td>
</tr>
<tr>
<td>100 IPs</td>
<td>33333.33</td>
</tr>
</tbody></table>
