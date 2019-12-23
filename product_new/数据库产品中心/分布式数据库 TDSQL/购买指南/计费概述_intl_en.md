## Billing Modes
TencentDB for  TDSQL offers the following billing modes:

| Billing Mode | Payment Mode | Application Scenario |
|---------|---------|---------|
| Pay as you go | In this postpaid billing mode, you can apply for resources for on-demand use and will be charged based on the actual usage at the billing time. | It is suitable for instantaneously fluctuating businesses. In this mode, instances can be released immediately after the use so as to reduce the costs. |

Depending on the usage duration, the prices in pay-as-you-go mode are divided into three tiers:

| Usage Duration | Tiered Pricing |
|---------|---------|
| 0 hours < duration ≤ 96 hours | Tier 1 pay-as-you-go price applies |
| 96 hours < duration ≤ 360 hours | Tier 2 pay-as-you-go price applies |
| Duration > 360 hours | Tier 3 pay-as-you-go price applies |

## Instance Price

### Billing formula
**Total fees = instance fees + backup capacity fees + traffic fees**
**Instance fees = shard price * number of nodes = (shard memory * memory price + shard disk * disk price) * number of nodes**
>The number of nodes is the sum of master and slave instances. For example, one master and one slave are 2 nodes, while one master and two slaves are 3 nodes.
### Billable items
<table>
<thead>
<tr>
<th width="15%">Billable Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Memory specification fees<br></td>
<td>Fees of the instance specification selected on the purchase page. Tiered pay-as-you-go billing mode is supported.</td>
</tr>
<tr>
<td>Storage capacity fees</td>
<td>Fees of the disk capacity selected on the purchase page. Pay-as-you-go billing mode is supported.</td>
</tr>
<tr>
<td>Backup capacity fees</td>
<td>Fees of backup capacity and log capacity. The backup capacity mainly stores key logs and backup files during TDSQL operation, while the log capacity stores transaction logs (binlogs), error logs, and slow logs. 50% of the instance capacity is gifted as the backup capacity, and excessive capacity is free of charge too for now. </td>
</tr>
<tr>
<td>Traffic fees</td>
<td>This refers to the fees of public network traffic (free of charge for now).</td>
</tr>
</tbody></table>

### Pay-as-you-go

<table>
    <tr>
        <td>Region</td>
        <td>Tier 1 (USD/GB/hour)</td>
        <td>Tier 2 (USD/GB/hour)</td>
        <td>Tier 3 (USD/GB/hour)</td>
        <td>Disk price (USD/GB/hour)</td>
    </tr>
    <tr>
        <td>Guangzhou, Shanghai, Beijing</td>
        <td>0.026194</td>
        <td>0.013097</td>
        <td>0.019646</td>
        <td>0.000250</td>
    </tr>
    <tr>
        <td>Chengdu, Chongqing</td>
        <td>0.026194</td>
        <td>0.019646</td>
        <td>0.013097</td>
        <td>0.000250</td>
    </tr>
    <tr>
        <td>Hong Kong (China)</td>
        <td>0.034420</td>
        <td>0.025815</td>
        <td>0.017210</td>
        <td>0.000118</td>
    </tr>
    <tr>
        <td>Singapore</td>
        <td>0.035225</td>
        <td>0.026419</td>
        <td>0.017613</td>
        <td>0.000118</td>
    </tr>
    <tr>
        <td>Japan</td>
        <td>0.027778</td>
        <td>0.020833</td>
        <td>0.013889</td>
        <td>0.000153</td>
    </tr>
    <tr>
        <td>Virginia</td>
        <td>0.022222</td>
        <td>0.016667</td>
        <td>0.011111</td>
        <td>0.000097</td>
    </tr>
    <tr>
        <td>Silicon Valley (US)</td>
        <td>0.027500</td>
        <td>0.020625</td>
        <td>0.013750</td>
        <td>0.000094</td>
    </tr>
    <tr>
        <td>Toronto</td>
        <td>0.036836</td>
        <td>0.027627</td>
        <td>0.018418</td>
        <td>0.000139</td>
    </tr>
</table>

## Billing Example


- For example, if you purchase 2 TDSQL instances (one-master-one-slave edition) in Beijing with 2 GB of shard memory and 500 GB of shard disk for 400 hours,
then the fees to be paid are calculated as follows:
 - Tier 1: (2 GB * 0.026194 USD/GB/hour + 500 GB * 0.000250 USD/GB/hour) * 2 nodes * 96 hours = 17.029248 USD
 - Tier 2: (2 GB * 0.013097 USD/GB/hour + 500 GB * 0.000250 USD/GB/hour) * 2 nodes * 264 hours = 48.830432 USD
 - Tier 3: (2 GB * 0.019646 USD/GB/hour + 500 GB * 0.000250 USD/GB/hour) * 2 nodes * 40 hours = 7.09552 USD
 - Total instance fees = tier 1 + tier 2 + tier 3 = 72.9552 USD



