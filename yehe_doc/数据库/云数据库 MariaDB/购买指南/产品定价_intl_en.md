
## Billing Formula
**Total fees = Instance fees + Backup capacity fees + Traffic fees**.
**Instance fees = Node price x Number of nodes = (Node memory x Memory price + Node disk capacity x Disk price) x Number of nodes**

>? The number of nodes is the sum of primary and replica instances. For example, 1 primary and 1 replica are 2 nodes, and 1 primary and 2 replicas are 3 nodes.

#### Billable Items
<table>
<thead>
<tr>
<th width="28%" colspan = "2">Billable Items</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=3>Instance fees</td>
</tr>
<td>Memory fees<br></td>
<td>Fees for the instance specification selected on the purchase page. Billing options include monthly subscription and pay-as-you-go.</td>
</tr>
<tr>
<td >Storage usage fees</td>
<td>Fees for the disk capacity selected on the purchase page. Billing options include monthly subscription and pay-as-you-go.</td>
</tr>
<tr>
<td colspan = "2">Backup capacity fees</td>
<td>Backup and log capacity fees. Backup capacity mainly stores key logs and backup files. Log capacity stores transaction logs (binlogs), error logs, and slow logs. Users will receive 50% of the instance capacity for free to use as backup capacity. Any usage exceeding this complimentary capacity will not be charged for now.</td>
</tr>
<tr>
<td colspan = "2">Traffic fees</td>
<td >Public network traffic fees (currently free of charge).</td>
</tr>
</tbody></table>

## Pricing for Monthly Subscription Single Node
>? Monthly subscription is currently in beta. This pricing document is for reference only, please see your bill for the actual price. If you wish to use this billing option, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
>
<table>
<thead>
<tr>
<th>Region</th>
<th>Disk Price (USD/GB/Month)</th>
<th>Memory Price (USD/GB/Month)</th>
</tr>
</thead>
<tbody><tr>
<td>Guangzhou, Beijing, Shanghai, Shenzhen, Nanjing, Chengdu, Chongqing, Qingyuan</td>
<td>0.18</td>
<td>9.43</td>
</tr>
<tr>
<td>Hong Kong (China)</td>
<td>0.085</td>
<td>12.39</td>
</tr>
<tr>
<td>Japan</td>
<td>0.11</td>
<td>10.00</td>
</tr>
<tr>
<td>Virginia, Frankfurt</td>
<td>0.07</td>
<td>8.00</td>
</tr>
<tr>
<td>Toronto</td>
<td>0.1
</td>
<td>13.26</td>
</tr>
<tr>
<td>Singapore</td>
<td>0.085</td>
<td>12.68</td>
</tr>
</tbody></table>



## Pricing for Pay-As-You-Go Single Node

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
        <td>Guangzhou, Beijing, Shanghai, Shenzhen, Nanjing, Chengdu, Chongqing,Qingyuan</td>
        <td>0.0262</td>
        <td>0.0196</td>
        <td>0.0131</td>
        <td>0.00025</td>
    </tr>
    <tr>
        <td>Hong Kong (China)</td>
        <td>0.0344</td>
        <td>0.0258</td>
        <td>0.0172</td>
        <td>0.00011806</td>
    </tr>
    <tr>
        <td>Virginia,Frankfurt</td>
        <td>0.0222</td>
        <td>0.0167</td>
        <td>0.0111</td>
        <td>0.00009722</td>
    </tr>
    <tr>
        <td>Toronto</td>
        <td>0.0368</td>
        <td>0.0276</td>
        <td>0.0184</td>
        <td>0.00013889</td>
    </tr>
	    <tr>
        <td>Japan</td>
        <td>0.0278</td>
        <td>0.0208</td>
        <td>0.0139</td>
        <td>0.00015278</td>
    </tr>
	    <tr>
        <td>Singapore</td>
        <td>0.0352</td>
        <td>0.0264</td>
        <td>0.0176</td>
        <td>0.00011806</td>
    </tr>
</tbody></table>

## Billing Examples 
**Monthly subscription**: suppose a user purchases 1 monthly subscription TencentDB for MariaDB with 2 nodes (1 primary and 1 replica) in the Guangzhou region for 1 month, and each node has 2 GB memory and 500 GB disk capacity.
The fees to be paid are calculated as follows:
Instance fees = (Node memory x Memory price + Node disk capacity x Disk price) x Number of nodes=(2 GB × 9.43 USD/GB/month + 500 GB x 0.18 USD/GB/month) x 2 nodes x 1 month = 217.72 USD
	
**Pay-as-you-go**: suppose a user purchases 1 pay-as-you-go TencentDB for MariaDB with 2 nodes (1 primary and 1 replica) in the Beijing region for 400 hours, and each node has 2 GB memory and 500 GB disk capacity.
The fees to be paid are calculated as follows:
 - Tier 1 fee: (2 GB x 0.0262 USD/GB/hr + 500 GB x 0.00025 USD/GB/hr) x 2 nodes x 96 hours = 34.061 USD
 - Tier 2 fee: (2 GB x 0.0196 USD/GB/hr + 500 GB x 0.00025 USD/GB/hr) x 2 nodes x 264 hours = 86.698 USD
 - Tier 3 fee: (2 GB x 0.0131 USD/GB/hr + 500 GB x 0.00025 USD/GB/hr) x 2 nodes x 40 hours = 12.096 USD
Instance fees = Tier 1 fee + Tier 2 fee + Tier 3 fee = 132.855 USD
