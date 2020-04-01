## Billing Mode
TencentDB for MySQL offers the pay-as-you-go billing mode: 

Depending on the usage duration, the prices in pay-as-you-go mode divides into three tiers:

| Usage Duration | Tiered Pricing | 
|---------|---------|
| 0 hours < duration ≤ 96 hours | Tier 1 pay-as-you-go price applies | 
| 96 hours < duration ≤ 360 hours | Tier 2 pay-as-you-go price applies | 
| Duration > 360 hours | Tier 3 pay-as-you-go price applies | 

## Instance Pricing

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
<td>The instance specification selected on the purchase page is pay-as-you-go and supports tiered pricing. For detailed prices, please see <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">Product Pricing</a>.</td>
</tr>
<tr>
<td>Storage capacity fees</td>
<td>The disk capacity selected on the purchase page is pay-as-you-go and supports tiered pricing. For detailed prices, please see <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">Product Pricing</a>.</td>
</tr>
<tr>
<td>Backup capacity fees</td>
<td>TencentDB for MySQL offers a certain amount of backup capacity free of charge based on the region, which is equivalent to the sum of storage capacity of all high-availability instances (including master and disaster recovery instances) in your region. <br>For more information on the fees for excessive back capacity, please see <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">Backup Capacity Billing Description</a>.</td>
</tr>
<tr>
<td>Traffic fees</td>
<td>This refers to the fees of public network traffic (free of charge for now).</td>
</tr>
</tbody></table>
