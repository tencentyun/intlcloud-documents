## Billing Mode
TencentDB for PostgreSQL offers the following two billing modes:

| Billing Mode | Payment Mode | Application Scenario | 
|---------|---------|---------|
| Pay as you go | In this [postpaid](https://cloud.tencent.com/document/product/555/9617) billing mode, you can apply for resources for on-demand use and will be charged based on the actual usage at the billing time. | It is suitable for instantaneously fluctuating businesses. In this mode, instances can be released immediately after the use so as to reduce the costs. | 

A linear pricing schedule is used for pay-as-you-go disks. The unit prices for different regions are as follows:

| Region | Unit Price (USD/GB/Hour) |
|---------|---------|
| Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Tianjin, Shenzhen | 0.0005 |
| Hong Kong (China), Singapore, Seoul, Mumbai | 0.00024 |
| Toronto, Frankfurt | 0.00028 |
| Silicon Valley, Virginia | 0.00019 |
| Moscow, Tokyo | 0.00031 |

Depending on the usage duration, the prices for pay-as-you-go memory are divided into three tiers:

| Usage Duration | Tiered Pricing | 
|---------|---------|
| 0 hours < duration ≤ 96 hours | Tier 1 pay-as-you-go price applies | 
| 96 hours < duration ≤ 360 hours | Tier 2 pay-as-you-go price applies | 
| Duration > 360 hours | Tier 3 pay-as-you-go price applies | 

The unit prices per tier for different regions are as follows:

| Region | Tier 1 (USD/GB/Hour) | Tier 2 (USD/GB/Hour) | Tier 3 (USD/GB/Hour) | 
|---------|---------|---------|---------|
| Frankfurt, Silicon Valley | 0.055 | 0.041 | 0.028 |
| Russia, Japan, Mumbai, Seoul | 0.056 | 0.042 | 0.028 |
| Singapore | 0.07 | 0.053 | 0.035 |
| Hong Kong (China) | 0.069 | 0.052 | 0.034 |
| Virginia | 0.044 | 0.033 | 0.022 |
| Toronto | 0.074 | 0.055 | 0.037 |
| Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Tianjin, Shenzhen | 0.052 | 0.039 | 0.026 |


## Instance Price

### Billing formula
**Total fees = memory specification fees + storage capacity fees + backup capacity fees + traffic fees**

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
<td>Fees of the instance specification selected on the purchase page.</td>
</tr>
<tr>
<td>Storage capacity fees</td>
<td>Fees of the disk capacity selected on the purchase page.</td>
</tr>
<tr>
<td>Backup capacity fees</td>
<td>TencentDB for PostgreSQL offers a free tier of backup capacity based on the region, which is equivalent to 50% of the total storage capacity of all the instances in your region.<br>Excessive backup capacity is free of charge currently.</td>
</tr>
<tr>
<td>Traffic fees</td>
<td>Fees of public network traffic (free of charge for now).</td>
</tr>
</tbody></table>


## Billing Example
Assume that you purchase a pay-as-you-go TencentDB for PostgreSQL instance with a memory size of 8 GB and disk capacity of 500 GB in the Guangzhou region and use it for 24 hours.
The fees for the current month are calculated as follows:
Instance price = memory specification fees + storage capacity fees = 0.0005 USD/GB/hour * 500 GB * 24 hours + 0.052 USD/GB/hour * 8 GB * 24 hours = 15.984 USD
