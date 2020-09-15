
## Billing Formula
**Total fees = Instance fees + Backup capacity fees + Traffic fees**.
**Instance fees = Node price x Number of nodes x Number of shards=(Node memory size x Memory price + Node disk size x Disk price) x Number of nodes x Number of shards**

>?The number of nodes is the sum of primary and secondary instances. For example, 1 primary and 1 secondary are 2 nodes, and 1 primary and 2 secondaries are 3 nodes.

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
<td >Storage capacity fees</td>
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




## Node Monthly Subscription Price (USD)
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
<td>Beijing, Shanghai, Guangzhou, Tianjin, Nanjing, Shenzhen, Qingyuan</td>
<td>0.06</td>
<td>9.43</td>
</tr>
<tr>
<td>Chengdu, Chongqing</td>
<td>0.06</td>
<td>9.43</td>
</tr>
<tr>
<td>Hong Kong (China)</td>
<td>0.085</td>
<td>12.3913</td>
</tr>
<tr>
<td>Virginia</td>
<td>0.07</td>
<td>8</td>
</tr>
<tr>
<td>Silicon Valley</td>
<td>0.068</td>
<td>9.9</td>
</tr>
<tr>
<td>Toronto</td>
<td>0.1</td>
<td>13.2609</td>
</tr>
<tr>
<td>Frankfurt</td>
<td>0.1</td>
<td>9.9</td>
</tr>
<tr>
<td>Singapore</td>
<td>0.085</td>
<td>12.6812</td>
</tr>
    <tr>
  <td>Japan</td>
<td>0.11</td>
<td>10</td>
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
        <td>Beijing, Shanghai, Guangzhou, Tianjin, Nanjing, Shenzhen, Qingyuan</td>
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
    </tr>
    <tr>
        <td>Hong Kong (China)</td>
        <td>0.03442</td>
        <td>0.02582</td>
        <td>0.01721</td>
        <td>0.00012</td>
    </tr>
    <tr>
        <td>Virginia</td>
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
<tr>
        <td>Silicon Valley (US)</td>
        <td>0.02750</td>
        <td>0.02063</td>
        <td>0.01375</td>
        <td>0.00009</td>
    </tr>
    <tr>
        <td>Singapore</td>
        <td>0.03522</td>
        <td>0.02642</td>
        <td>0.01761</td>
        <td>0.00012</td>
    </tr>
    <tr>
        <td>Japan</td>
        <td>0.02778</td>
        <td>0.02083</td>
        <td>0.01389</td>
        <td>0.00015</td>
    </tr>
    <tr>
        <td>Frankfurt</td>
        <td>0.02222</td>
        <td>0.01667</td>
        <td>0.01111</td>
        <td>0.00010</td>
    </tr>
</tbody></table>

## 

## Billing Examples

**Monthly subscription**: suppose a user purchases 1 monthly subscription TDSQL instance with 2 nodes (1 primary and 1 secondary) in the Guangzhou region for 1 month, and each node has 2 GB memory, 500 GB disk capacity, and 2 shards.
The fees to be paid are calculated as follows:
Instance fees = (Node memory size x Memory price + Node disk size x Disk price) x Number of nodes x Number of shards=(2 GB x 9.43 USD/GB/month + 500 GB x 0.06 USD/GB/month) x 2 nodes x 2 shards x 1 month = 195.44 USD
	
**Pay-as-you-go**: suppose a user purchases 1 pay-as-you-go TDSQL instance with 2 nodes (1 primary and 1 secondary) in the Beijing region for 400 hours, and each node has 2 GB of memory, 500 GB disk capacity, and 2 shards.
The fees to be paid are calculated as follows:
 - Tier 1 fee: (2 GB x 0.026194 USD/GB/hr + 500 GB x 0.000250 USD/GB/hr) x 2 nodes x 2 shards x 96 hours = 68.116992 USD
 - Tier 2 fee: (2 GB x 0.013097 USD/GB/hr + 500 GB x 0.000250 USD/GB/hr) x 2 nodes x 2 shards x 264 hours = 159.660864 USD
 - Tier 3 fee: (2 GB x 0.019646 USD/GB/hr + 500 GB x 0.000250 USD/GB/hr) x 2 nodes x 2 shards x 40 hours = 26.28672 USD
Total instance fees=Tier 1 fee + Tier 2 fee + Tier 3 fee = 254.064576 USD
