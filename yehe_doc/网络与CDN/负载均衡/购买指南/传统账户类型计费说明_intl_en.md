This document explains the billing of bill-by-CVM accounts and provides billing samples for reference.

## Billable Items
For bill-by-CVM accounts, the CLB cost involves the following three parts: instance fee, public network fee and LCU fee.
<table>
<tr>
<th>Account Type</th>
<th>Network Type</th>
<th>Instance Type</th>
<th>Instance Fee</th>
<th>Public Network Fee</th>
<th>LCU Fee</th>
</tr>
<tr>
<td rowspan="4" width="15%">Bill-by-CVM</td>
<td rowspan="2">Public network </td>
<td >Shared</td>
<td rowspan="2">&#10003; </td>
<td rowspan="2">× </td>
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
<td >-</td>
</tr>
<tr>
<td >LCU-supported</td>
<td >&#10003; </td>
</tr>
</table>

>?
>+ Only LCU-supported CLB instances will incur LCU usage fees. LCU-supported CLB instances are only available to beta users. To use it, please [submit an application](https://intl.cloud.tencent.com/apply/p/fj5bwo9e6rj). Shared CLB instances are free of LCU charges.
>+ Private network CLBs are free of public network fee but incur instance fee.
>+ Public network CLBs only incur instance fee. You can purchase public network on CVM. For more details, see [Public Network Fee](https://intl.cloud.tencent.com/zh/document/product/213/39743).

### Instance fee
>! Tencent Cloud upgraded the architecture of all CLB instances at 00:00:00, November 2, 2021 (UTC +8). After the upgrade, the guaranteed performance of each individual CLB instance is increased to 50,000 concurrent connections, 5,000 new connections per second and 5,000 QPS. The new unit price for CLB instances (both private and public network) is 0.686 USD/day for most regions, and 1.029 USD/day for the rest regions. See [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/zh/document/product/214/41565) for more details.
>
- A private network CLB is free of public network fee but incurs instance fee. For more details, see [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/zh/document/product/214/41565).
- **The public network CLB instance adopts pay-per-use model.**
 - It is settled once every hour.
 - It is calculated based on the actual hours of usage.
 - Billing starts at the point in time when the CLB instance is created successfully and ends at the point in time when you initiate to terminate the instance.
 - Usage duration shorter than 1 hour will be calculated as 1 hour.
- **The public network CLB instance fee varies between regions:**
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


- **Billing sample**:
  If you use a public network CLB instance between 09:00:00 and 09:59:59 in Guangzhou, the instance fee is 0.686 USD and will be settled and deducted at the next hour (10:00:00–10:59:59).
>!
>- Fee for one settlement cycle will be deducted in advance when you create a pay-as-you-go CLB instance. Make sure that your account balance is sufficient.
>- The CLB instance will incur hourly instance fees even when it is idle (i.e., there is no access requests and no real server is bound).

### Public network fee
Tencent Cloud provides high-quality public VIPs for ISPs to ensure optimal network experience.
>!The public network fee for the client accessing CLB will be included in the CVM bill. If you do not purchase public network, you cannot access the CVM instance via the public network CLB instance.
>
<table>
<tr>
<th width="18%">CLB IP Version</th>
<th width="82%">Public Network Fee</th>
</tr>
<tr>
<td>IPv4 and IPv6 NAT64 CLB instance</td>
<td>When a client accesses a CLB, the public network fee incurred is included in the CVM bill. When creating a CVM instance, you need to specify the public network capability (maximum bandwidth) and billing method as bill-by-traffic. A CLB only serves as a public network egress. If you do not purchase public network, you cannot access the CVM instance via the public network CLB instance.</td>
</tr>
<tr>
<td>IPv6 CLB instance</td>
<td>IPv6 CLB is a paid service. For bill-by-CVM accounts, the bandwidth fee for an IPv6 CLB instance using the IPv6 dual-stack public network is settled in BWP. When creating an IPv6 CLB instance, you need to specify the public network capability (maximum bandwidth) and billing method as bill-by-BWP. For more details, see <a href="https://intl.cloud.tencent.com/zh/document/product/684/15254" target="_blank">Billing Overview</a>.</td>
</tr>
</table>

### LCU fee
For more details on the LCU fee, see [LCU Pricing](https://intl.cloud.tencent.com/zh/document/product/214/41563).
## References
[Billing Overview](https://intl.cloud.tencent.com/zh/document/product/214/36999)