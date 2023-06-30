To upgrade the Lighthouse instance specifications, you need to upgrade the instance bundles in the console. The upgrade takes effect immediately. 

<dx-alert infotype="explain" title="">
For directions on instance bundle upgrade, see [Upgrading Instance Bundle](https://intl.cloud.tencent.com/document/product/1103/41562).
</dx-alert>

## Billing Rule
- The upgrade fee is calculated according to the price difference between the new and original bundles and the length of upgrade period.
Upgrade fee = (New bundle monthly rate * Remaining months * Applicable discount) - (Original bundle monthly rate * Remaining validity in months * Original discount) 
 - The number of remaining months is converted from the number of remaining days.
   - **Remaining days** = Expiration date - Current date
   - **Converted remaining months** = Remaining days / (365 / 12)
 - **Discount**: It varies by the instance region and usage period. For details, see [Basic Bundle Pricing](https://intl.cloud.tencent.com/document/product/1103/41403). 
- The upgrade does not affect the resource expiration date.
- You can pay the upgrade fee by using your vouchers and free credits.
>? Note that if the original bundle was purchased with a special price, the special price is not used for the upgrade fee calculation. Instead, the official listed monthly price is used.   

## Data Transfer Plan
After you upgrade an instance bundle, the data transfer plan follows the following rule:
- The current traffic usage of the instance is not changed. Only the quota of the monthly data transfer plan is upgraded.
Assume that the data plan of the original bundle is 200 GB, and 100 GB has been used in this month. If the data plan of the new bundle is 500 GB, then the remaining quota for this month is 400 GB. 
- If the instance is upgraded from bandwidth-based billing to a data transfer plan, the all quota of the transfer plan is granted. 



## Billing Example
>? The following prices are for demonstration only. For the accurate bundle prices, see [Basic Bundle Pricing](https://intl.cloud.tencent.com/document/product/1103/41403).


<table>
<tr>
<th>Example</th>
<td>Purchased a one-year bundle in Hong Kong (China) on Dec 31, 2021. </td>
<td>On May 1, 2022, upgraded the bundle as below:</td>
</tr>
<tr>
<th>Specification</th>
<td>
Price: 5 USD/month
<ul class="params">
<li>CPU: 2 core</li>
<li>MEM: 2 GB</li>
<li>SSD system disk: 30 GB</li>
<li>Bandwidth: 30 Mbps</li>
<li>Monthly data transfer: 1024 GB</li>
</ul>
</td>
<td>
Price: 22 USD/month
<ul class="params">
<li>CPU: 2 core</li>
<li>MEM: 8 GB</li>
<li>SSD system disk: 100 GB</li>
<li>Bandwidth: 30 Mbps</li>
<li>Monthly data transfer: 4096 GB</li>
</ul>
</td>
</tr>
</table>

In this case, the upgrade fee is calculated as below:
- Remaining days = 31 * 4 + 30 × 3 + 30 = 244 days.
 Here, **4** stands for four months: July, August, October, and December, **3** stands for three months: June, September, and November, and the **30** at the end is the number of remaining days in May (31 - 1 = 30).  
- Remaining months = 244 / (365 / 12) =  
- Discount:
  - According to the validity of the new bundle, a 12% discount is offered as described in the official price list. 
  - There is no discount for the original bundle. 
- **Upgrade fees** = (22 * 244 / (365 / 12) * 0.88) - (5 * 244 / (365 / 12) * 1) = 115.17 USD.

<style>
 .params{margin-bottom:0px !important;}
</style>
