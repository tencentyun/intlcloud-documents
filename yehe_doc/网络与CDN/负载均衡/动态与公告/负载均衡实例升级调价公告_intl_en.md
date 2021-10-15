Tencent Cloud plans to upgrade the architecture of all CLB instances staring from 00:00:00, November 2, 2021 (UTC +8). After the upgrade, the guaranteed performance of each individual CLB instance will be increased to 50,000 concurrent connections, 5,000 new connections per second and 5,000 QPS.


The performance is guaranteed for each CLB instance.
>?
>- Before the upgrade, shared CLB instances share resources of one cluster, which may affect the performance in case of resource contention.
>- After the upgrade, the basic performance for every individual shared CLB instance is guaranteed. When the required performance exceeds the guaranteed value, resource contention may occur.


## Price Adjustment
The price adjustment covers all CLB instances (former "Application Load Balancer instances") and Classic CLB instances.
- **A private network CLB instance is priced as 0.686 USD per day (1.029 USD per day for some regions)**.
- **A public network CLB instance is priced as 0.686 USD per day (1.029 USD per day for some regions)**.

See below for the new instance prices:
<dx-tabs>
::: Pay-as-you-go instance billing
Prices provided in this notice take effect from 00:00:00, November 2, 2021 (UTC +8) until next price adjustment. This document describes only the price adjustments. For specific prices, see the pricing on purchase page or in your actual order.

<table>
  <tbody>
          <tr>
			<th width="14%">Billing Item</th>
			<th width="12%">Billing Mode</th>
			<th width="12%">Billing Cycle</th>
      <th width="40%">Region</th>
      <th width="22%">Price (Unit: USD/Day)</th>
  </tr>
   <tr>
		  <td rowspan="2">Instance fees</td>
			<td rowspan="2">Pay-as-you-go</td>
			<td rowspan="2">Day</td>
      <td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, Silicon Valley, Virginia, Toronto, Moscow, Jakarta</td>
       <td>0.686</td>
		</tr>
		   <tr>
      <td>Bangkok, Mumbai, Seoul, Tokyo, Frankfurt</td>
       <td>1.029</td>
		</tr>
</tbody></table>

<dx-alert infotype="notice" title="">
The price adjustment may cause overdue payments, leading to account suspension and business interruption. Please delete unnecessary CLB instances based on your usage and monthly cost.
</dx-alert>

## FAQs
How do I optimize my bill?
- Terminate idle CLB instances such as those without listeners or unbound to real servers.
- Each CLB can have up to 50 listeners. You can create multiple protocol ports for a single CLB instance. For more details, see [Restrictions](https://intl.cloud.tencent.com/document/product/214/6187).


## References
- [Bill-by-IP Account Billing Description](https://intl.cloud.tencent.com/document/product/214/36998)
- [Bill-by-CVM Account Billing Description](https://intl.cloud.tencent.com/document/product/214/8848)
- [LCU Billing](https://intl.cloud.tencent.com/document/product/214/41563)
