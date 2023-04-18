
## Billing Formula
**Total fees = instance fees + backup space fees (currently free) + traffic fees (currently free) + audit fees (currently free)**
**Instance fees = node price * number of nodes * number of shards = (node memory size * memory price + node disk size * disk price) * number of nodes * number of shards**

>?The number of nodes is the sum of source and replica nodes specified in the instance specification. For example, 1-source-1-replica specification means 2 nodes and 1-source-2-node specification 3 nodes.

#### Billable items
<table>
<thead><tr><th width="28%" colspan = "2">Billable Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td rowspan=3>Instance fees</td></tr>
<td>Memory specification fees<br></td>
<td>Fees for the instance specification selected on the purchase page, which can be monthly subscribed or pay-as-you-go and supports tiered pricing.</td></tr>
<tr>
<td >Storage space fees</td>
<td>Fees for the disk size selected on the purchase page, which can be monthly subscribed or pay-as-you-go.</td></tr>
<tr>
<td colspan = "2">Backup space fees</td>
<td>Fees for the backup space. The backup space mainly stores key logs (binlogs, error logs, slow logs, etc.) and backup files of TDSQL for MySQL.
<br>You will receive 100% of the instance capacity for free to use as the backup space. Any usage exceeding this complimentary capacity is billed as detailed in <a href="https://www.tencentcloud.com/document/product/1042/53797">Backup Space Billing</a>.</td></tr>
<tr>
<td colspan = "2">Traffic fees</td><td >Fees for public network traffic, which is currently free of charge.</td></tr>
<tr>
<td colspan = "2">Audit fees</td><td >Fees for the database audit feature, which is currently in beta test free of charge.</td></tr>
</tbody></table>

## Monthly Subscription Pricing
<table>
<thead><tr><th>Region</th><th>Memory Price (USD/GB/Month)</th><th>Disk Price (USD/GB/Month)</th></tr></thead>
<tbody><tr>
<td>Guangzhou, Beijing, Shanghai, Shenzhen, Nanjing</td><td>9.43</td><td>0.06</td></tr>
<tr>
<td>Chengdu, Chongqing</td><td>9.43</td><td>0.06</td></tr>
<tr>
<td>Hong Kong (China)</td><td>12.3913</td><td>0.085</td></tr>
<tr>
<td>Virginia, Frankfurt, Silicon Valley</td><td>8</td><td>0.07</td></tr>
<tr>
<td>Toronto</td><td>13.2609</td><td>0.1</td></tr>
<tr>
<td>Mumbai, Singapore</td><td>12.6812</td><td>0.085</td></tr>
<tr>
<td>Seoul, Tokyo</td><td>10</td><td>0.11</td></tr>
</tbody></table>

## Pay-as-You-Go Pricing
<table>
<thead><tbody>
<tr><th rowspan=2>Region</th><th  colspan = "3">Memory Price (USD/GB/Hour)</th><th rowspan=2>Disk Price (USD/GB/Hour)</th></tr>
<tr><th>Tier 1</th><th>Tier 2</th><th>Tier 3</th></tr></thead>
<tr>
<td>Guangzhou, Beijing, Shanghai, Shenzhen, Nanjing</td>
<td>0.02619</td><td>0.01965</td><td>0.01310</td><td>0.00025</td></tr>
<tr>
<td>Chengdu, Chongqing</td>
<td>0.02619</td><td>0.01965</td><td>0.01310</td><td>0.00025</td></tr>
<tr>
<td>Hong Kong (China)</td>
<td>0.03442</td><td>0.02582</td><td>0.01721</td><td>0.00012</td></tr>
<tr>
<td>Virginia, Frankfurt, Silicon Valley</td>
<td>0.02222</td><td>0.01667</td><td>0.01111</td><td>0.00010</td></tr>
<tr>
<td>Toronto</td>
<td>0.03684</td><td>0.02763</td><td>0.01842</td><td>0.00014</td></tr>
<tr>
<td>Seoul, Tokyo</td>
<td>0.02778</td><td>0.02083</td><td>0.01389</td><td>0.00015</td></tr>
<tr>
<td>Mumbai, Singapore</td>
<td>0.03523</td><td>0.02642</td><td>0.01761</td><td>0.00012</td></tr>
</tbody></table>
## Billing Example
**Monthly subscription**: Suppose a user purchases 1 monthly subscribed TDSQL for MySQL instance with 2 shards in Guangzhou region for 1 month. Each shard has 2 nodes (1 source and 1 replica), and each node has 2 GB memory and 500 GB disk capacity.
The fees are calculated as follows:
Instance fees = (node memory size * memory price + node disk size * disk price) * number of nodes * number of shards = (2 GB * 9.43 USD/GB/month + 500 GB * 0.06 USD/GB/month) * 2 nodes * 2 shards * 1 month = 195.44 USD
	
**Pay-as-you-go**: Suppose a user purchases 1 pay-as-you-go TDSQL for MySQL instance with 2 shards in Beijing region for 400 hours. Each shard has 2 nodes (1 source and 1 replica), and each node has 2 GB memory and 500 GB disk capacity.
The fees are calculated as follows:

 - Tier 1 fees: (2 GB * 0.026194 USD/GB/hour + 500 GB * 0.000250 USD/GB/hour) * 2 nodes * 2 shards * 96 hours = 68.116992 USD
 - Tier 2 fees: (2 GB * 0.013097 USD/GB/hour + 500 GB * 0.000250 USD/GB/hour) * 2 nodes * 2 shards * 264 hours = 159.660864 USD
 - Tier 3 fees: (2 GB * 0.019646 USD/GB/hour + 500 GB * 0.000250 USD/GB/hour) * 2 nodes * 2 shards * 40 hours = 26.28672 USD
Instance fees = tier 1 fees + tier 2 fees + tier 3 fees = 254.064576 USD
