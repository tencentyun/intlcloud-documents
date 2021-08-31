Private network CLB is free of charge, while public network CLB is charged for instance fees and public network fees. If you purchase a CLB instance under a bill-by-IP account, two billing modes are supported: monthly subscription and pay-as-you-go.

## Monthly Subscription
>? The monthly subscription mode is currently in beta. Prices published here are for reference only. Refer to your bills for final prices. To use this billing option, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
>
Monthly subscription is prepaid. You need to pay for one or multiple months or even years in advance. This billing mode is applicable to long-term businesses with stable peak traffic. The public network fees of a monthly subscription CLB instance only support bill-by-bandwidth, and the monthly bandwidth is cheaper than the hourly bandwidth. If you need to use CLB in the long run, we recommend purchasing a monthly subscription CLB instance.


### Billing cycle
You need to pay for the total purchased duration (in months) in advance.

### Billing formula
The billable items include instance fees and public network fees.
Total fees = Instance fees + Public network fees = (Monthly instance fees × Purchased duration) + (Monthly bandwidth fees × Purchased duration)

### Pricing
>?
>- The network billing mode of a monthly subscription CLB instance only supports billing at a fixed bandwidth.
>- You need to configure the bandwidth upper limit when purchasing a CLB instance with fixed bandwidth. This limit applies to both the outbound and inbound bandwidth. If exceeded, packets are lost by default and no fees will be incurred.
>- Regardless of the actual bandwidth, the CLB instance is always billed by the configured bandwidth upper limit.
>
<table>
  <tbody>
     <tr>
      <th rowspan="2" width="35%">Region</th>
      <th rowspan="2" width="15%">Instance Fees<br>(USD/Month)</th>
      <th colspan="6" width="50%" style="text-align:center;">Bandwidth Fees (USD/Month)</th>
  </tr>
  <tr>
       <th>1 Mbps</th>
       <th>2 Mbps</th>
       <th>3 Mbps</th>
       <th>4 Mbps</th>
       <th>5 Mbps</th>
       <th>6 Mbps and above<br>("n" is the configured bandwidth upper limit)</th>
  </tr>
   <tr>
      <td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing</td>
      <td rowspan="4">2.06</td>
       <td>3.29</td>
       <td>6.75</td>
       <td>10.14</td>
       <td>13.71</td>
       <td>17.85</td>
       <td>17.85 + 11.43 × (n-5)</td>   
    </tr>
   <tr>
      <td>Hong Kong (China), Silicon Valley, Virginia, Toronto</td>
        <td>4.29</td>
       <td>8.58</td>
       <td>12.87</td>
       <td>17.16</td>
       <td>21.45</td>
       <td>21.45 + 14.29 × (n - 5) </td>    
    </tr>
    <tr>
      <td>Singapore, Frankfurt, Moscow</td>
      <td>3.29</td>
       <td>6.58</td>
       <td>9.87</td>
       <td>13.16</td>
       <td>16.45</td>
       <td>16.45 + 11.43 × (n - 5) </td>    
    </tr>
    <tr>
      <td>Bangkok, Mumbai, Seoul, Tokyo</td>
      <td>3.57</td>
       <td>7.14</td>
       <td>7.72</td>
       <td>14.28</td>
       <td>17.85</td>
       <td>17.85 + 12 × (n - 5) </td>   
    </tr>
</tbody></table>

### Billing sample
Suppose you purchase a monthly subscription CLB instance in the Guangzhou region for 6 months and configure the bandwidth upper limit to 2 Mbps, which falls into the price tier of 6.75 USD/month:
- Instance fees = Monthly instance fees × Purchased duration = 2.06 USD/month × 6 months = 12.35 USD
- Public network fees = Monthly bandwidth fees × Purchased duration = 6.75 USD/month × 6 months = 40.5 USD
Total fees to be paid in advance = Instance fees + Public network fees = 12.35 USD + 40.5 USD = 52.85 USD

## Pay-as-You-Go
Pay-as-you-go is an elastic billing mode, where you can create/terminate instances at any time and pay for what you use.

### Billing cycle
Instance fees and public network fees (dedicated bandwidth package):
 - Fees are settled once every hour.
 - Fees are calculated based on the actual hours of usage.
 - Billing starts at the point in time when the CLB instance is created successfully and ends at the point in time when you initiate to terminate the instance.
 - Usage duration shorter than 1 hour will be calculated as 1 hour.

If public network fees are billed by bandwidth package, the billing cycle will be monthly. For more information, please see [Billing Modes](https://intl.cloud.tencent.com/document/product/684/15255).

### Billing formula
The billable items include instance fees and public network fees.
The public network fees support both bill-by-traffic and bandwidth package.
The calculation formula of total public network fees varies by billing modes, as detailed below:
<table ><thead><tr><th>Billing Mode</th><th>Total Fees</th></tr></thead>
<tbody>
<tr><td><a href="#traffic">Bill-by-traffic</a></td><td>Total fees = Instance fees (hourly instance fees × usage duration) + Public network fees (traffic fees per unit × total traffic)</td></tr>
<tr><td><a href="#bag">Bandwidth package</a> </td><td> Total fees = Instance fees (hourly instance fees × usage duration) + Public network fees (<a href="https://intl.cloud.tencent.com/document/product/684/15255">bandwidth package fees</a>) </td></tr></tbody></table>

### Pricing
#### Instance fees
<table>
<thead>
<tr>
<th >Region</th>
<th >Instance Fees<br>(USD/Day)</th>
</tr>
</thead>
<tbody><tr>
<td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing</td>
<td>0.07</td>
</tr>
<tr>
<td>Silicon Valley, Virginia</td>
<td>0.12</td>
</tr>
<tr>
<td>Singapore, Toronto, Frankfurt, Moscow</td>
<td>0.14</td>
</tr>
<tr>
<td>Hong Kong (China), Seoul, Tokyo, Mumbai, Bangkok</td>
<td>0.22</td>
</tr>
</tbody></table>

>!
> - Fees for one billing cycle will be deducted in advance when you create a pay-as-you-go CLB instance. Make sure that your account balance is sufficient.
> - You will be billed for hourly instance fees even when the CLB instance you purchased is in idle status (i.e., no access requests and no real server is bound).

#### Public network fees

- <span id="traffic">**Bill-by-traffic**
This billing mode is based on the total volume (in GB) of data transferred over the public network and is applicable to scenarios where the business traffic fluctuates greatly. If your bandwidth utilization is below 10%, we recommend using bill-by-traffic.
>?
>- Currently, the outbound traffic is billable, i.e., traffic from CLB to the public network.
>- To avoid fees incurred by sudden traffic surges, you can specify the bandwidth upper limit. If exceeded, packets are lost by default and no fees will be incurred.
<table>
<thead>
<tr>
<th width="80%">Region</th>
<th width="20%">Public Network Fees (USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>Chinese Mainland, Seoul, Hong Kong (China)</td>
<td>0.12</td>
</tr>
<tr>
<td>Singapore</td>
<td>0.081</td>
</tr>
<tr>
<td>Frankfurt, Toronto, Silicon Valley</td>
<td>0.077</td>
</tr>
<tr>
<td>Moscow, Tokyo</td>
<td>0.13</td>
</tr><tr>
<td>Virginia</td>
<td>0.075</td>
</tr><tr>
<td>Bangkok, Mumbai</td>
<td>0.1</td>
</tr>
</tbody></table>

- <span id="bag"> **Bandwidth package**
This billing mode bills multiple IPs in an aggregated manner and is applicable to large-scale businesses where public network instances have traffic peaks at different times.
For detailed pricing, please see [Billing Modes](https://intl.cloud.tencent.com/document/product/684/15255).

### Billing samples

#### Sample 1 (public network is billed by traffic)
Suppose you use a pay-as-you-go CLB instance whose public network billing mode is bill-by-traffic and the total traffic from CLB to the public network is 2 GB between 09:00:00, June 1, 2020 and 08:59:59, June 2, 2020 in the Guangzhou region, then:
- Instance fees = Hourly instance fees × Usage duration = 0.07 USD/day × 1 day = 0.07 USD
- Public network fees: Traffic fees per unit × Total traffic = 0.12 USD/GB × 2 GB = 0.24 USD
Total fees = Instance fees + Public network fees = 0.07 USD + 0.24 USD = 0.31 USD

#### Sample 2 (public network is billed by bandwidth package)
Suppose you use a pay-as-you-go CLB instance whose public network billing mode is bandwidth package between 09:00:00, June 1, 2020 and 08:59:59, June 2, 2020 in the Guangzhou region, then:
- Instance fees = Hourly instance fees × Usage duration = 0.07 USD/day × 1 day = 0.07 USD
- Public network fees: because <a href="https://intl.cloud.tencent.com/document/product/684/15255">bandwidth package fees</a> are settled monthly, only instance fees will be settled during usage.
Total fees = Instance fees = 0.07 USD, which will be settled and deducted at the next hour (10:00:00–10:59:59).
