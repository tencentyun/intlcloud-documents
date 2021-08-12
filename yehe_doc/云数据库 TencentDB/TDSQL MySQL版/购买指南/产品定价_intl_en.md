
## Billing Formula
**Total fees = Instance fees + Backup capacity fees (free of charge for now) + Traffic fees (free of charge for now)**
**Instance fees = Node price x Number of nodes x Number of shards = (Node memory size x Memory price + Node disk size x Disk price) x Number of nodes x Number of shards**

>?The number of nodes is the sum of primary and secondary nodes specified in the instance specification. For example, 1-primary-1-secondary specification means 2 nodes and 1-primary-2-secondary specification 3 nodes.

#### Billable items
<table>
<thead>
<tr>
<th width="28%" colspan = "2">Billable Items</th>
<th>Notes</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=3>Instance fees</td>
</tr>
<td>Memory fees<br></td>
<td>Fees for the instance specification selected on the purchase page. Monthly subscription and pay-as-you-go billing modes are supported.</td>
</tr>
<tr>
<td >Storage capacity fees</td>
<td>Fees for the disk capacity selected on the purchase page. Monthly subscription and pay-as-you-go billing modes are supported.</td>
</tr>
<tr>
<td colspan = "2">Backup capacity fees</td>
<td>Fees for the backup capacity. The backup capacity mainly stores key logs (binlogs, error logs, slow logs, etc.) and backup files. 50% of the instance capacity is gifted as the backup capacity, and usage exceeding this complimentary capacity is free of charge for now.</td>
</tr>
<tr>
<td colspan = "2">Traffic fees</td>
<td >Fees for public network traffic (free of charge at present).</td>
</tr>
</tbody></table>

## Node Monthly Subscription Price (USD)
>? The monthly subscription mode is currently in beta. Prices published here are for reference only. Refer to your bills for final prices. To use this billing option, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
>

<table>
<thead>
<tr>
<th>Region</th>
<th>Memory Price (USD/GB/Month)</th>
<th>Disk Price (USD/GB/Month)</th>
</tr>
</thead>
<tbody><tr>
<td>Guangzhou, Shanghai, and Beijing</td>
<td>9.43</td>
<td>0.06</td>
</tr>
<tr>
<td>Chengdu, Chongqing</td>
<td>9.43</td>
<td>0.06</td>
</tr>
<tr>
</tr>
<tr>
<td>Hong Kong (China)</td>
<td>12.3913</td>
<td>0.085</td>
</tr>
<tr>
<td>Virginia, Frankfurt</td>
<td>8</td>
<td>0.07</td>
</tr>
<tr>
<td>Toronto</td>
<td>13.2609</td>
<td>0.1</td>
</tr>
</tbody></table>




## Node Pay-As-You-Go Price (USD)

<table>
<thead>
<tbody><tr>
        <th rowspan=2>Region</th>
        <th  colspan = "3">Memory Price (USD/GB/Hr)</th>
        <th rowspan=2>Disk Price (USD/GB/Hr)</th>
    </tr>
		<tr>
        <th>Tier 1</th>
        <th>Tier 2</th>
        <th>Tier 3</th>
    </tr>
</thead>
    <tr>
        <td>Guangzhou, Shanghai, and Beijing</td>
        <td>0.02619</td>
        <td>0.01965</td>
        <td>0.01310</td>
        <td>0.00025</td>
    </tr>
		    <tr>
        <td>Chengdu, Chongqing</td>
        <td>0.02619</td>
        <td>0.01965</td>
        <td>0.01309</td>
        <td>0.00025</td>
    </tr>
    <tr>
        <td>Hong Kong (China)</td>
        <td>0.03442</td>
        <td>0.02582</td>
        <td>0.01721</td>
        <td>0.00012</td>
    </tr>
    <tr>
        <td>Virginia, Frankfurt</td>
        <td>0.02222</td>
        <td>0.01667</td>
        <td>0.01111</td>
        <td>0.00010</td>
    </tr>
    <tr>
        <td>Toronto</td>
        <td>0.03684</td>
        <td>0.02763</td>
        <td>0.01842</td>
        <td>0.00014</td>
    </tr>
</tbody></table>


## Billing Examples

**Monthly subscription**: suppose a user purchases 1 monthly-subscribed TDSQL for MySQL instance with 2 shards in the Guangzhou region for 1 month. Each shard has 2 nodes (1 primary and 1 secondary), and each node has 2 GB memory and 500 GB disk capacity.
The fees are calculated as follows:
Instance fees = (Node memory size x Memory price + Node disk size x Disk price) x Number of nodes x Number of shards = (2 GB x 9.43 USD/GB/month + 500 GB x 0.06 USD/GB/month) x 2 nodes x 2 shards x 1 month = 195.44 USD
	
**Pay-as-you-go**: suppose a user purchases 1 pay-as-you-go TDSQL for MySQL instance with 2 shards in the Beijing region for 400 hours. Each shard has 2 nodes (1 primary and 1 secondary), and each node has 2 GB memory and 500 GB disk capacity.
The fees are calculated as follows:
 - Tier 1 fees: (2 GB x 0.026194 USD/GB/hr + 500 GB x 0.000250 USD/GB/hr) x 2 nodes x 2 shards x 96 hours = 68.116992 USD
 - Tier 2 fees: (2 GB x 0.013097 USD/GB/hr + 500 GB x 0.000250 USD/GB/hr) x 2 nodes x 2 shards x 264 hours = 159.660864 USD
 - Tier 3 fees: (2 GB x 0.019646 USD/GB/hr + 500 GB x 0.000250 USD/GB/hr) x 2 nodes x 2 shards x 40 hours = 26.28672 USD
Instance fees = Tier 1 fees + Tier 2 fees + Tier 3 fees = 254.064576 USD
