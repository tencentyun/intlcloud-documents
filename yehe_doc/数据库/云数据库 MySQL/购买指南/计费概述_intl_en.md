>?This product now supports dynamic pricing query and cost estimation. You can use the [Price Calculator](https://intl.cloud.tencent.com/pricing/cdb) to estimate fees.

## Billing Modes

TencentDB for MySQL now offers the monthly subscription billing mode. Pay-as-you-go pricing remains unchanged.



TencentDB for MySQL supports separate billing for memory and disks to provide users with more flexible options.

Instance price formula: Instance price = Memory fee + Storage fee






## Advanced Features

### Backup capacity

Backup capacity does not support monthly subscription. Please see pay-as-you-go pricing.

**Instance renewal management**

Batch renewal, auto-renewal, collective expiry date, do-not-renew flag can be found in the **Renewal Management** page.



**Instance upgrade cost formula**

Suppose an instance expires in T days, and the monthly prepaid fee difference between the target configuration and the current configuration is C, then the total upgrade cost will be: T/30 x C.

Assume that you have an instance with 1 core, 1000 MB memory, and 100 GB disk (prepaid fee: 24.511 USD/month) and it will expire in 15 days. If you need to upgrade it to 1 core, 1000 MB memory, and 200 GB disk (prepaid fee: 34.653 USD/month), then the total upgrade cost will be: 15/30 x (34.653 - 24.511)=5.071 USD.



**Exceeding instance disk capacity limit**

To ensure business continuity, upgrade your instance specifications or purchase additional disk capacity in time before disk capacity is used up.

When the size of the data stored on an instance exceeds its capacity limit, the instance will be locked and become read-only. You will not be able to write data to it. You will need to expand its capacity or delete some database tables in the console to unlock it.

To avoid a database from triggering the lock status repeatedly, a locked instance will be unlocked and allowed for reads and writes only when its remaining available capacity accounts for more than 20% of its total capacity or is over 50 GB.



**Traffic synchronization fee for disaster recovery instances**

Data synchronization for disaster recovery instances in TencentDB for MySQL is currently free of charge.

We will notify users when this feature is commercialized.

## Pay-as-You-Go

The pay-as-you-go tiered pricing model is based on usage duration.

| Usage Duration | Tiered Pricing |
|---------|---------|
| 0 hours < duration ≤ 96 hours   | Tier 1 rate applies |
| 96 hours < duration ≤ 360 hours | Tier 2 rate applies |
| Duration > 360 hours          | Tier 3 rate applies |

### Instance price

#### Billing formula
**Total fees = memory fees + storage capacity fees + backup capacity fees + traffic fees (currently free)**

#### Billable items
<table>
<thead>
<tr>
<th width="15%">Billable Item</th>
<th>Notes</th>
</tr>
</thead>
<tbody><tr>
<td>Memory fees<br></td>
<td>The instance specification selected on the purchase page is pay-as-you-go and supports tiered pricing. For detailed prices, please see <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">Product Pricing</a>.</td>
</tr>
<tr>
<td>Storage capacity fees</td>
<td>The disk capacity selected on the purchase page is pay-as-you-go. For detailed prices, please see <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">Product Pricing</a>.<br>The storage capacity stores data files, shared tablespaces, error logs, redo logs, undo logs, data dictionaries, and binlogs that are necessary for TencentDB for MySQL.</tr>
<tr>
<td>Backup capacity fees</td>
<td>TencentDB for MySQL offers a certain amount of backup capacity free of charge based on the region, which is equivalent to the sum of storage capacity of all two-node and three-node instances (including source instances) in your region. <br>For more information on the fees for excessive backup capacity, please see <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">Backup Space Billing</a>.</td>
</tr>
<tr>
<td>Traffic fees</td>
<td>Public network traffic fees (currently free of charge).</td>
</tr>
</tbody></table>


#### Pay-as-you-go price

##### High-availability edition
<table>
  <td rowspan=2>Region</td>
  <td colspan=3 >Memory (USD/GB/Hour)</td>
  <td rowspan=2 >Disk (USD/GB/Hour)</td>
 </tr>
 <tr  >
  <td >Tier 1</td>
  <td>Tier 2</td>
  <td>Tier 3</td>
 </tr>
 <tr  >
  <td>Guangzhou</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Qingyuan</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Shanghai</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Beijing</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Chengdu</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Chongqing</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Hong Kong (China)</td>
  <td class=xl66 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Taipei (China)</td>
  <td class=xl65 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Singapore</td>
  <td class=xl65 align=right>0.0705</td>
  <td class=xl65 align=right>0.0528</td>
  <td class=xl65 align=right>0.0352</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Bangkok</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Mumbai</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Seoul</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Tokyo</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Silicon Valley</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Virginia</td>
  <td class=xl65 align=right>0.0444</td>
  <td class=xl65 align=right>0.0333</td>
  <td class=xl65 align=right>0.0222</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Toronto</td>
  <td class=xl65 align=right>0.0265</td>
  <td class=xl65 align=right>0.0199</td>
  <td class=xl65 align=right>0.0133</td>
  <td class=xl65 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Frankfurt</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Moscow</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 </tr>
</table>

##### Read-only instances

<table>
  <td rowspan=2>Region</td>
  <td colspan=3 >Memory (USD/GB/Hour)</td>
  <td rowspan=2 >Disk (USD/GB/Hour)</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Tier 1</td>
  <td class=xl1529815>Tier 2</td>
  <td class=xl1529815>Tier 3</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Guangzhou</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Qingyuan</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Shanghai</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Beijing</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Chengdu</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Chongqing</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Hong Kong (China)</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Taipei (China)</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Singapore</td>
  <td class=xl6529815 align=right>0.0352</td>
  <td class=xl6529815 align=right>0.0264</td>
  <td class=xl6529815 align=right>0.0176</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Bangkok</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Mumbai</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Seoul</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Tokyo</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Silicon Valley</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Virginia</td>
  <td class=xl6529815 align=right>0.0222</td>
  <td class=xl6529815 align=right>0.0167</td>
  <td class=xl6529815 align=right>0.0111</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Toronto</td>
  <td class=xl6529815 align=right>0.0133</td>
  <td class=xl6529815 align=right>0.0099</td>
  <td class=xl6529815 align=right>0.0066</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Frankfurt</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Moscow</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
</table>


## Billing Examples
>?The prices used in the following examples are for demonstration purposes only, which may vary depending on regions, campaigns, or policies. Please see the pricing page for actual prices.
>

### Monthly subscription
Suppose that:
- You purchase a monthly-subscribed high-availability TencentDB for MySQL instance with 4 cores, 8,000 MB memory, and 500 GB disk space in the Guangzhou Zone 3 for 1 month.
- You purchase a monthly-subscribed high-availability TencentDB for MySQL instance with 4 cores, 8,000 MB memory, and 200 GB disk space in the Guangzhou Zone 4 for 1 month.

Total fees = memory fees + storage capacity fees + backup capacity fees

##### Memory fees and storage capacity fees
Calculation formula:
Memory fees + storage capacity fees = 2 x 114.93 USD/month + (500 GB + 200 GB) x 0.1014 USD/GB/month x 1 month = 300.84 USD

##### Backup capacity fees
The high-availability TencentDB for MySQL instance in Guangzhou Zone 3 has 500 GB storage capacity per month, and the one in Guangzhou Zone 4 has 200 GB storage capacity per month, so you can have 700 GB backup capacity free of charge in the Guangzhou region every month.

Usage of backup capacity that exceeds the free tier are calculated on an hourly basis according to the following rule. For example, if your data backups reach 800 GB and log backups reach 100 GB, your total backup capacity usage in Guangzhou will exceed 700 GB, and your hourly billable backup capacity will be 200 GB (800 + 100 - 700 = 200).

Backup capacity fees (hourly) = 200 GB (usage of backup capacity that exceeds the free tier may change over time) x 0.000127 USD/GB/hour

### Pay-as-you-go
Suppose you purchase a pay-as-you-go TencentDB for MySQL instance with 4 cores, 8,000 MB memory, and 500 GB disk space in the Guangzhou region for 400 hours.
Tier 1 fees: (0.0250 USD/GB/hour * 8 GB + 500 GB * 0.0003) * 96 hours = 33.6 USD
Tier 2 fees: (0.0200 USD/GB/hour * 8 GB + 500 GB * 0.0003) * 264 hours = 81.84 USD
Tier 3 fees: (0.0150 USD/GB/hour * 8 GB + 500 GB * 0.0003) * 40 hours = 10.8 USD
Instance fees = Tier 1 fees + Tier 2 fees + Tier 3 fees = 126.24 USD

## FAQs
#### Why are additional fees incurred for my monthly-subscribed instance?
Usage of backup capacity that exceeds the free tier will be charged. Please check whether your usage of backup capacity exceeds the free tier.
You can check the usage of backup capacity on the **Database Backup** page in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/backup). For more information about backup capacity pricing, please see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).

#### Will Tencent Cloud charge for pay-as-you-go instances if they are idle?
Yes. If you stop using pay-as-you-go resources, please terminate them as soon as possible to avoid further fees.

#### What files are stored in the storage capacity?

- Data files: the space which your data takes up, including created tables and indexes
- System files (necessary for the database): shared tablespaces, error logs, redo logs, undo logs, and data dictionaries
- Binlogs: binlogs record all DDL and DML statements (except SELECT and SHOW statements) and are used to replicate and restore database data. The more data changes, the more binlogs. To reduce the space binlogs take up, they can be uploaded to COS.

## Documentation
- You can purchase TencentDB for MySQL instances through the console or API. For more information, please see [Purchase Methods](https://intl.cloud.tencent.com/document/product/236/5160).
- TencentDB for MySQL sends alert messages to you before it expires and its resources are repossessed. For more information, please see [Overdue Payment](https://intl.cloud.tencent.com/document/product/236/5159).
- You can return TencentDB for MySQL instances and request a refund. For more information, please see [Refund](https://intl.cloud.tencent.com/document/product/236/14618).
- You can adjust TencentDB for MySQL instances to a higher or lower specification. For more information, please see [Instance Adjustment Fee](https://intl.cloud.tencent.com/document/product/236/32345).
