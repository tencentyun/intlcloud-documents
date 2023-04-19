This document explains the billing of bill-by-IP accounts and provides related billing examples.

## Billable Items
For bill-by-IP accounts, the CLB cost involves the following four parts: instance fee, public network fee, cross-region binding fee and LCU fee.
>? 
>+ Only LCU-supported CLB instances incur LCU usage fees. LCU-supported CLB instances are only available to beta users now. To use it, please [submit an application](https://intl.cloud.tencent.com/apply/p/fj5bwo9e6rj).
>+ Shared CLB instances are free of LCU charges.
<table>
<tr>
<th>Account Type</th>
<th>Network Type </th>
<th>Instance Type</th>
<th>Instance Fee</th>
<th>Public Network Fee</th>
<th>Cross-region Binding Fee </th>
<th>LCU Fee</th>
</tr>
<tr>
<td rowspan="4" width="15%">Bill-by-IP</td>
<td rowspan="2">Public network </td>
<td >Shared</td>
<td rowspan="2">&#10003; </td>
<td rowspan="2">&#10003; </td>
<td rowspan="2">&#10003; </td>
<td>-</td>
</tr>
<tr>
<td >LCU-supported</td>
<td >&#10003; </td>
</tr>
<tr>
<td rowspan="2">Private network </td>
<td >Shared</td>
<td rowspan="2">&#10003; </td>
<td rowspan="2">- </td>
<td rowspan="2">-</td>
<td >-</td>
</tr>
<tr>
<td >LCU-supported</td>
<td >&#10003; </td>
</tr>
</table>

+ Private network CLB is free of public network fee but generates instance fee. For more details, see [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/document/product/214/41565).
+ Public network CLB generates instance fee and public network fee.
+ If <a href="https://intl.cloud.tencent.com/document/product/214/38441"> cross-region binding 2.0</a> is configured and enabled for public network CLB instances, the cross-region binding fee is included in the CNN bill.

>! Tencent Cloud plans to upgrade the architecture of all CLB instances staring from 00:00:00, November 2, 2021 (UTC +8). After the upgrade, the guaranteed performance of each individual CLB instance will be increased to 50,000 concurrent connections, 5,000 new connections per second and 5,000 QPS. The new unit price for CLB instances (both private and public network) is 0.686 USD/day for most regions, and 1.029 USD/day for the rest regions. See [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/document/product/214/41565) for more details.


## Pay-As-You-Go[](id:pay-as-you-go)
The CLB cost is calculated on the actual amount of usage.

### Pricing
CLB cost = [Instance fee](#traffic-instance) + [Public network fee](#traffic-width) + [LCU fee](#traffic-lcu)
#### [Instance fee](id:traffic-instance)
The instance fee is billed by day and settled once every day. Each partial hour is billed as a full hour

<table>
<thead>
<tr>
<th >Region</th>
<th >Instance Fee (Unit: USD/Day)</th>
</tr>
</thead>
<tbody><tr>
<td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, Jakarta, Silicon Valley, Virginia, Toronto, Moscow</td>
<td>0.686</td>
</tr>
<tr>
<td>Bangkok, Mumbai, Seoul, Tokyo, Frankfurt, Sao Paulo</td>
<td>1.029</td>
</tr>

</tbody></table>

>!
> - Fee for one hour will be deducted in advance when you create a pay-as-you-go CLB instance. Make sure that your account balance is sufficient.
> - The CLB instance will incur daily instance fees even when it is idle (i.e., there is no access requests and no real server is bound).
#### [Public network fee](id:traffic-width)
<dx-accordion>

::: Bill\sby\straffic[](id:traffic)
This billing mode is based on the total volume of data (in GB) transferred over the public network and settled once every hour, which is applicable to scenarios where the business traffic fluctuates greatly. If your bandwidth utilization is below 10%, we recommend using bill-by-traffic.
<dx-alert infotype="explain" title="">
- Currently, the outbound traffic is billable, i.e., traffic from CLB to the public network.
- To avoid unexpected costs due to traffic surges, you can set a bandwidth cap. Any traffic over the cap is dropped and does not incur charges.
- The traffic units are 1024-based. For example, 1 TB = 1,024 GB, and 1 GB = 1,024 MB.
</dx-alert>

<table>
<thead>
<tr>
<th width="70%">Region</th>
<th>Public Network Fee (Unit: USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>Chinese mainland, Seoul, Hong Kong (China), Jakarta</td>
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
</tr><tr>
<td>São Paulo</td>
<td>0.15</td>
</tr>
</tbody></table>
:::
::: Bill\sby\sBWP[](id:bag)
This billing mode bills multiple IPs in an aggregated manner and is applicable to large-scale businesses where public network instances have traffic peaks at different times. For more details about the pricing, see [BGP Bandwidth Package](https://intl.cloud.tencent.com/document/product/684/15254#bgp).
:::
</dx-accordion>

#### [LCU fee](id:traffic-lcu)
For more details on how LCU is billed in the pay-as-you-go modal, see [LCU Billing](https://intl.cloud.tencent.com/document/product/214/41563).

### Billing samples
<dx-accordion>
::: Shared CLB instance
#### Sample 1 (public network is billed by traffic)
Suppose you use a pay-as-you-go CLB instance with bill-by-traffic public network and the total traffic from CLB to the public network is 2 GB between June 1st 10:00:00 and June 2nd 09:59:59 in Guangzhou.
- Total instance fee = Unit price × Usage duration, that is 0.686 USD/day × 1 day = 0.686 USD.
- Total public network fee = Unit price × Total traffic, that is 0.12 USD/GB × 2 GB = 0.24 USD.
Total fee = Instance fee + Public network fee, that is 0.686 USD + 0.24 USD = 0.926 USD.

#### Sample 2 (public network is billed by bandwidth package)
Suppose you use a pay-as-you-go CLB instance with bill-by-BWP public network between June 1st 10:00:00 and June 2nd 09:59:59 in Guangzhou.
- Total instance fee = Unit price × Usage duration, that is 0.686 USD/day × 1 day = 0.686 USD.
- Total public network fee for this period cannot be settled because <a href="https://intl.cloud.tencent.com/document/product/684/15254">BWP fees</a> are settled monthly.
Total fee = Instance fee, that is 0.686 USD.
:::
::: LCU-supported CLB instance
#### Sample 1 (public network is billed by traffic)
Suppose you use a pay-as-you-go CLB instance with bill-by-traffic public network, the total traffic from CLB to the public network is 2 GB between June 1st 10:00:00 and June 2nd 09:59:59 in Guangzhou and the average LCUs used per hour is 2 LCUs.
- Total instance fee = Unit price × Usage duration, that is 0.686 USD/day × 1 day = 0.686 USD.
- Total public network fee = Unit price × Total traffic, that is 0.12 USD/GB × 2 GB = 0.24 USD.
- Total LCU fee = 2 LCUs × 0.0072 USD/LCU/hour × 24 hour = 0.3456 USD.
Total fee = Instance fee (0.686 USD) + Public network fee (0.24 USD) + LCU fee (0.3456 USD) = 1.2716 USD.

#### Sample 2 (public network is billed by bandwidth package)
Suppose you use a pay-as-you-go CLB instance with bill-by-BWP public network between June 1st 10:00:00 and June 2nd 09:59:59 in Guangzhou and the average LCUs used per hour is 2 LCUs.
- Total instance fee = Unit price × Usage duration = 0.686 USD/day × 1 day = 0.686 USD.
- Total public network fee for this period cannot be settled because <a href="https://intl.cloud.tencent.com/document/product/684/15254">BWP fees</a> are settled monthly.
- Total LCU fee = 2 LCUs × 0.0072 USD/LCU/hour × 24 hour = 0.3456 USD.
Total fee = Instance fee (0.686 USD) + LCU fee (0.0144 USD) = 1.0316 USD.

:::
</dx-accordion>
