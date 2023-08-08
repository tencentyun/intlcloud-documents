This document describes IPSec VPN and SSL VPN billing items and pricing.
>?
>- The price information presented in the tables of this document is for reference only. When it is inconsistent with the price information on the purchase page, the later shall prevail.
>- The adjustment of VPN gateway bandwidth is limited to [20,100] Mbps and [200,1000] Mbps. 
>

## Billable Items
![](https://qcloudimg.tencent-cloud.cn/raw/5446aa22b46d4f04476d96aa93222129.jpg)
<table>
<thead>
<tr>
<th>Type</th>
<th>Billable Item</th>
<th>Billing Plan</th>
</tr>
<tr>
<td>IPSec VPN </td>
<td>VPN gateway</td>
<td>Pay-as-you-go. For details, see <a href="#IPSecdingjia">IPSec VPN Pricing</a>.</td>
</tr>
<tr>
<td>SSL VPN </td>
<td>VPN gateway and SSL connections </td>
<td>Pay-as-you-go. For details, see <a href="#dingjia">SSL VPN Pricing</a>.</td>
</tr>
<tr>
<td colspan="2">Public network traffic fee</td>
<td>For details of the traffic fee, see <a href="https://www.tencentcloud.com/document/product/213/10578">Public Network Billing</a>.</td>
</tr>
</tbody></table>
<dx-alert infotype="explain" title="">
For IPSec VPN, the customer gateways are free of charge. For SSL VPN, the VPN servers and clients are free of charge.
</dx-alert>


## IPSec VPN Pricing[](id:IPSecdingjia)
IPSec VPN supports the traffic-based billing.

### Traffic-based billing
Traffic-based billing contains two parts, **traffic fee** (traffic going to the public network) and **gateway fee** (hourly billing, with a minimum usage of one hour).
- For traffic fee details, see [Public Network Billing](https://www.tencentcloud.com/document/product/213/10578).
- For gateway fee details, see the following table:
>?VPN gateway is your target gateway on Tencent Cloud side. The traffic flowing through the VPN gateway incurs fees. The gateway fee is billed by traffic.
The traffic here refers to the outbound traffic of the VPN gateway, which is also called the downstream traffic.

<table>
<thead>
<tr>
<td width="12%">Gateway specification</td>
<td width="18%">Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing</td>
<td width="18%"> Silicon Valley, Frankfurt, Seoul, Mumbai, Virginia, Tokyo, Taipei (China), Hong Kong (China), Sao paulo, Jakarta</td>
<td width="18%"> Toronto, Singapore, Bangkok </td>
</tr>
<tr>
<td>5 Mbps/10 Mbps/20 Mbps/</br>50 Mbps/100 Mbps</td>
<td>0.074 USD/hour</td>
<td>0.089 USD/hour</td>
<td>0.12 USD/hour</td>
</tr>
<tr>
<td>200 Mbps/500 Mbps/1,000 Mbps</td>
<td>0.44 USD/hour</td>
<td>0.6 USD/hour</td>
<td>0.75 USD/hour</td>
</tr>
<tr>
<td>3000 Mbps</td>
<td>0.6 USD/hour</td>
<td>0.9 USD/hour</td>
<td>0.9 USD/hour</td>
</tr>
</tbody></table>

#### Billing Example - Usage period less than one hour
Assume a user purchases 50 Mbps VPN gateway in Beijing with the bill-by-traffic option and uses a total of 5 GB traffic between 07:00:00-07:59:59, then at 08:00:00, the user will be required to pay the following fees:
+ Traffic fee: Traffic unit price (0.12 USD/GB for Beijing) × Traffic Usage (in GB) = 0.12 × 5 = 0.6 USD
+ Gateway fee: Gateway unit price (0.074 USD/hour for Beijing) × Gateway usage period (hourly billing, at least one hour is charged) = 0.074 × 1 = 0.074 USD

Total price = Traffic fee + Gateway fee = 0.6 USD + 0.074 USD = 0.67 USD

## SSL VPN Connection Pricing[](id:dingjia)
SSL VPN is a pay-as-you-go service. It contains three parts of fee: **traffic fee** (going to the  public network), **gateway fee** (hourly billing, with a minimum usage of one hour), and **SSL connection fee** (hourly billing, with a minimum usage of one hour).
- For traffic fee details, see [Public Network Billing](https://www.tencentcloud.com/document/product/213/10578).
- For gateway fee details, see the following table:
<table>
<thead>
<tr>
<th width="12%">Gateway specification</th>
<th width="18%">Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing</th>
<th width="18%">Silicon Valley, Frankfurt, Seoul, Mumbai, Virginia, Toronto, Bangkok, Singapore, Tokyo, Taipei (China), Hong Kong (China)</th>
</tr>
<tr>
<td>5 Mbps/10 Mbps/20 Mbps/</br>50 Mbps/100 Mbps</td>
<td>0.074 USD/hour</td>
<td>0.12 USD/hour</td>
</tr>
<tr>
<td>200 Mbps/500 Mbps/1,000 Mbps</td>
<td>0.44 USD/hour</td>
<td>0.6 USD/hour</td>
</tr>
</tbody></table>
- For the SSL connection fee, see the following table:
<table>
<tr>
<th>Number of connections </th>
<th>Price (USD/hour)</th>
</tr>
<tr>
<td>(0,10]</td>
<td>0.003</td>
</tr>
<tr>
<td> (10,1000]</td>
<td>0.002</td>
</tr>
</tbody></table>

>? For 200 Mbps and 500 Mbps, up to 500 connections are supported. For 1000 Mbps, up to 1,000 connections are supported.
>

## Billing Example - Usage period less than one hour
Assume a user purchases a 50 Mbps pay-as-you-go VPN gateway with 5 SSL connections in Beijing. During 07:00:00 to 07:29:59, the traffic usage is 5 GB. The bill for the next hour (08:00:00 to 08:59:59) is calculated as below:
+ Traffic fee: Traffic unit price (0.12 USD/GB for Beijing) × Traffic Usage (in GB) = 0.12 × 5 = 0.6 USD
+ Gateway fee: Gateway unit price (0.074 USD/hour for Beijing) × Gateway usage period (in hour) = 0.074 × 1 = 0.074 USD
+ SSL connection fee: Connection unit price (0.003 USD/connection/hour for Beijing) × Number of SSL connections × Usage period (in hour) = 0.003 × 5 × 1 (Usage less than one hour is rounded up to one hour) = 0.015 USD

Total price = Traffic fee + Gateway fee + SSL connection fee = 0.6 USD + 0.074 USD + 0.015 USD = 0.69 USD
