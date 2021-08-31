Tencent Cloud plans to **upgrade the specifications of all CLB instances staring from 00:00:00, November 2, 2021 (UTC +8)**, and the prices will be adjusted accordingly.


## Upgrade Description
After the upgrade, the guaranteed performance of each individual CLB instance is 50,000 max concurrent connections, 5000 new connections per second and 5000 QPS. Each shared CLB instance can leverage its performance within the specification.
>?
>- Before the upgrade, shared CLB instances share resources of one cluster, which may affect the performance in case of resource contention.
>- After the upgrade, the basic performance for every individual shared CLB instance is guaranteed. When the required performance exceeds the guaranteed value, rate limiting and packet loss may occur.


## Price Adjustment
The price adjustment covers all CLB instances (former "Application Load Balancer instances") and Classic CLB instances. 
- **Public network CLB instance price will be increased**.
- **Tencent Cloud will begin charging for private network CLB instances at the same price of public network CLB instances**.


See below for the new instance prices:
<dx-alert infotype="explain" title="">
Prices provided in this notice take effect from November 2, 2021 (UTC +8) until next price adjustment. This document describes only the price adjustments. For specific prices, see the pricing on purchase page or in your actual order.
</dx-alert>
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
To prevent business interruption caused by overdue payment, please delete unnecessary CLB instances.
</dx-alert>


## References
- [Bill-by-IP Account Billing Description](https://intl.cloud.tencent.com/document/product/214/36998)
- [Bill-by-CVM Account Billing Description](https://intl.cloud.tencent.com/document/product/214/8848)
- [LCU Billing](https://cloud.tencent.com/document/product/214/58387)

