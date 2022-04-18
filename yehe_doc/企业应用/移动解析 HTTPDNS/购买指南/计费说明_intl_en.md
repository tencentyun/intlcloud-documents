HTTPDNS is daily pay-as-you-go by the number of DNS queries. DNS queries performed from 00:00:00 to 23:59:59 on a day will be billed at 8:00:00 the next day.

## Free Tier
Users with HTTPDNS activated and enabled are provided with a free tier every month (30 natural days). The free tier varies by user type:

| User Type | Number of Free DNS Queries |
|---------|---------|
| DNSPod-resolved domain | 6 million/month |
| Non-DNSPod-resolved domain | 3 million/month |


## Traffic Package
You can [purchase a traffic package](https://buy.qcloud.com/httpdns) for fees deduction. The traffic package will be deducted first during billing, and any excess will be billed at the unit price of **0.04 CNY/10,000 queries**.

Traffic packages are priced as follows:

| Traffic Package Size | Price (CNY) | Validity Period |
|--------|--------| --------|
| 10 million | 32 | 3 months |
| 30 million | 84 | 3 months	|
| 300 million | 780 | 3 months |
| 1.5 billion | 3,600 | 3 months |
>?A traffic package is valid for 3 months from the date of purchase, and any unused DNS queries will expire upon the expiration of the traffic package.

Purchase a traffic package according to the number of DNS queries based on your industry and use case and monthly active users (N) to ensure that your traffic package will be sufficient:
<table>
<thead>
  <tr>
    <th>Industries and Use Cases</th>
    <th>Monthly Active Users (N)</th>
    <th>Monthly DNS Query Volume</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="4"><li>Audio/Video</li><li>Ecommerce</li><li>Social networking and community</li><li>Underlying mobile applications</li></td>
    <td>N ≥ 100 million</td>
    <td>1 trillion</td>
  </tr>
  <tr>
    <td>100 million > N ≥ 50 million</td>
    <td>100 billion</td>
  </tr>
  <tr>
    <td>50 million > N ≥ 10 million</td>
    <td>10 billion</td>
  </tr>
	  <tr>
    <td>10 million > N ≥ 5 million</td>
    <td>1 billion</td>
  </tr>
  <tr>
	<td rowspan="4"><li>Gaming</li><li>News and finance</li><li>Download tool</li><li>Express delivery and logistics</li><li>Real estate</li></td>
    <td>N ≥ 80 million</td>
    <td>100 billion</td>
  </tr>
  <tr>
    <td> 80 million > N ≥ 30 million</td>
    <td>10 billion</td>
  </tr>
  <tr>
    <td>30 million > N ≥ 10 million</td>
    <td>1 billion</td>
  </tr>
	  <tr>
    <td>10 million > N ≥ 5 million</td>
    <td>100 million</td>
  </tr>
</tbody>
</table>


## Auto-Renewal
If you enable auto-renewal, the traffic package will be automatically renewed as described below:
- The validity period of the renewed traffic package will be the same as the initial validity period.
- After auto-renewal is set, a traffic package of the same specification will be automatically purchased at the price indicated above on the day following the expiration of the traffic package. Make sure that your account balance is sufficient, because a payment failure will cancel auto-renewal.
- If a traffic package is used up before expiration, it will not be automatically renewed immediately but on the day following its expiration as described above. If no new traffic package is available at that time, HTTPDNS will be billed by the number of DNS queries according to the billing rules, so your DNS service will not be affected.
- If you want to cancel auto-renewal, you need to do so **before 23:59:59 on the expiration date**, and this operation will not incur any extra fees. If auto-renewal is not canceled before that time, your traffic package will be renewed.


## Pay-As-You-Go

### Calculation method
The number of HTTP DNS queries encrypted with DES under the current account for each natural day is calculated as follows:
- **1 HTTPS DNS query = 5 HTTP DNS queries encrypted with DES**
- **1 HTTP DNS query encrypted with AES = 3 HTTP DNS queries encrypted with DES**

<table class="t">
<tr>
<th> Billing Mode </th>
<th> Cycle </th>
<th>  Price </th>
</tr>
<tr>
<td> Pay-As-You-Go (postpaid) </td>
<td> Daily </td>
<td> 0.04 CNY/10,000 queries</td>
</tr>
</table>

>?If the number of DNS queries for a month is greater than 50 billion, HTTPDNS will be billed daily at 200 CNY/100 million queries in pay-as-you-go (postpaid) mode.

### Billing examples
If HTTPDNS was used to perform 1 million HTTP DNS queries encrypted with DES on the 1st day of the month and perform 800,000 HTTP DNS queries encrypted with DES and 200,000 HTTPS DNS queries on the 2nd day, the number of HTTP DNS queries encrypted with DES for the 1st day would be 1 million, and the number of HTTP DNS queries encrypted with DES for the 2nd day would be 800,000 + 5 \* 200,000 = 1.8 million.

The total pay-as-you-go fees would be 0.04 CNY/10,000 queries \* (1 million + 1.8 million) = 11.2 CNY.

## Deduction Order
### Usage deduction order
![](https://qcloudimg.tencent-cloud.cn/raw/e40def7c45fdd68c5475a9a9d5d98753.png)

### Deduction order example
If you host your domain in DNSPod and purchase an HTTPDNS traffic package of 10 million DNS queries, you will have a free tier of 6 million queries/month and 10 million queries in the traffic package. When you use HTTPDNS, the free tier will be deducted first; after the free tier is used up, the traffic package will be deducted; after the traffic package is used up, HTTPDNS will automatically switch to the pay-as-you-go billing mode.

>?If you encounter problems when using the product, contact [online customer service](https://intl.cloud.tencent.com/contact-sales) for assistance.
