You can quickly and easily adjust the package configuration of Lighthouse instances. If you want to increase the instance configuration as your business grows, you can directly upgrade instance packages in the console. After a successful upgrade, the instances will immediately run at the new package configuration.


## Billing Rule
- The price difference of instance package upgrade is charged by day in the following way: 
Upgrade fees = (monthly price of target package * number of upgrade months * applicable discount) - (monthly price of original package * number of upgrade months * applicable discount)
 - Upgrade fees are charged by day: 
   - **Number of upgrade days** = resource expiration time - current time
   - **Number of upgrade months** = number of upgrade days / (365 / 12)
 - **Applicable discount**: it varies by instance region, number of upgrade months, and applicable discount as listed at the Lighthouse official website. For more information, please see duration discounts in different regions in [Basic Package Pricing](https://intl.cloud.tencent.com/document/product/1103/41403).
- Upgrade does not affect the resource expiration time.
- You can use vouchers and credit gifted by the platform (gift cards) to deduct the upgrade fees.
>? The promotional upgrade policy is the same as the instance package upgrade rule, i.e., upgrade fees = (monthly price of target package * number of upgrade months * applicable discount) - (monthly price of original package * number of upgrade months * applicable discount).

## Traffic Package Description
After you upgrade an instance package, the traffic package follows the following rule:
- The amount of currently used traffic of the instance does not change, and the monthly traffic package limit will be adjusted to that after upgrade.
For example, if the traffic package of the original package is 200 GB, 100 GB has been used in this month, and the traffic package of the new package after the upgrade is 500 GB, then 400 GB public network traffic can be used in this month.
- If an instance package is upgraded from fixed bandwidth to traffic package, then after the successful upgrade, the instance can use the entire amount of traffic up to the traffic package limit, and traffic usage will be calculated immediately.



## Billing Example
>? The following prices are for demonstration only but not the actual prices at the official website. For package unit prices, please see [Basic Package Pricing](https://intl.cloud.tencent.com/document/product/1103/41403).


<table>
<tr>
<th>Background</th>
<td>You purchased the following Lighthouse package in Hong Kong (China) for one year on December 31, 2020:</td>
<td>On May 1, 2021, you upgraded the package to the following configuration:</td>
</tr>
<tr>
<th>Configuration</th>
<td>
Price: 24 CNY/month
<ul class="params">
<li>CPU: 1 core</li>
<li>Memory: 1 GB</li>
<li>SSD system disk: 25 GB</li>
<li>Peak bandwidth: 30 Mbps</li>
<li>Monthly traffic package: 1,024 GB</li>
</ul>
</td>
<td>
Price: 133 CNY/month
<ul class="params">
<li>CPU: 2 cores</li>
<li>Memory: 8 GB</li>
<li>SSD system disk: 100 GB</li>
<li>Peak bandwidth: 30 Mbps</li>
<li>Monthly traffic package: 4,096 GB</li>
</ul>
</td>
</tr>
</table>

Against the above package upgrade background, the fees are calculated as follows: 
- Number of upgrade days = 31 * 4 + 30 × 3 + 30 = 244 days. 
Here, "4" stands for four months: July, August, October, and December, "3" stands for three months: June, September, and November, and "30" is the 31 days in May minus 1 day. 
- Number of upgrade months = 244 / (365 / 12). 
- Applicable discount: 
  - The target package is eligible for a discount at the official website. For a monthly subscription duration of 6–11 months, a 12% discount is offered. 
  - The original package isn't eligible for any discount. 
- **Upgrade fees** = (133 * 244 / (365 / 12) * 0.88) - (24 * 244 / (365 / 12) * 1)  = 746.36 CNY.

<style>
 .params{margin-bottom:0px !important;}
</style>
