## Billing Mode
TencentDB for MySQL offers the following two billing mode:

| Billing Mode | Payment Mode | Use Case |
|---------|---------|---------|
| Monthly subscription | [Prepaid](https://intl.cloud.tencent.com/document/product/555/42701). You need to pay the fees when creating an instance. | It is more cost-effective in the long term for businesses with stable needs than pay-as-you-go billing. Moreover, the longer a service is purchased, the higher the discount. |
| Pay-as-you-go | [Postpaid](https://intl.cloud.tencent.com/document/product/555/30328). You can request for resources on-demand and will be charged based on the actual usage upon settlement. | It is suitable for businesses with fluctuating demands. Instances can be released immediately after use to save costs. |

## Instance Pricing
### Billing formula
**Total fees = memory and CPU fees + storage space fees + backup space fees + traffic fees (free of charge for now)**

### Billable items
<table>
<thead><tr><th width="15%">Billable Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Memory and CPU fees<br></td>
<td>The instance specification selected on the purchase page supports monthly subscription and pay-as-you-go billing with tiered pricing. For detailed prices, see <a href="https://intl.cloud.tencent.com/pricing/cdb/overview" target="_blank">Pricing | TencentDB for MySQL</a>.<br>Pay-as-you-go billing adopts 3-tier pricing. The longer the usage, the higher the discount.<br>Tier 1: 0 hours < tier 1 ≤ 96 hours. Tier 2: 96 hours < tier 2 ≤ 360 hours. Tier 3: tier 3 > 360 hours.</td></tr>
<tr>
<td>Storage space fees</td>
<td>The disk space selected on the purchase page supports monthly subscription and pay-as-you-go billing with tiered pricing. For detailed prices, see <a href="https://intl.cloud.tencent.com/pricing/cdb/overview" target="_blank">Pricing | TencentDB for MySQL</a>.<br>The storage space is used to store data files, shared tablespaces, error, redo, and undo log files, data dictionaries, and binlogs that are necessary for TencentDB for MySQL operations.</tr>
<tr>
<td>Backup space fees</td>
<td>TencentDB for MySQL offers a certain amount of backup space free of charge by region, which is equivalent to the total storage space of all two-node and three-node instances (including source and disaster recovery instances) in a region.<br>For more information on the fees for excessive backup space, see <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">Backup Space Billing</a>.</td></tr>
<tr>
<td>Traffic fees</td>
<td>Public network traffic fees (free of charge currently).</td></tr>
</tbody></table>


You can directly use the [Price Calculator](https://intl.cloud.tencent.com/pricing/cdb/calculator) to calculate the instance specification, storage space, and backup space fees for resource cost estimation. For accurate calculation, use the calculator after logging in to your Tencent Cloud account.

## Billing Examples
>?The following prices are for demonstration only. The actual prices at the official website shall prevail, which may vary by region, campaign, or policy.

**Pay-as-you-go billing example**
You purchase a pay-as-you-go two-node TencentDB for MySQL instance with 4 cores, 8,000 MB memory, and 500 GB disk space in Guangzhou region for 400 hours, and the used backup space is within the free tier.
Tier 1 fees: (0.4 USD/GB/hour + 500 GB * 0.00021739 USD/GB/hour) * 96 hours = 48.8 USD
Tier 2 fees: (0.32 USD/GB/hour + 500 GB * 0.00021739 USD/GB/hour) * 264 hours = 113.2 USD
Tier 3 fees: (0.24 USD/GB/hour + 500 GB * 0.00021739 USD/GB/hour) * 40 hours = 13.9 USD
Instance fees = tier 1 fees + tier 2 fees + tier 3 fees = 175.9 USD

**Monthly subscription billing example**
In Guangzhou region:
- You purchase a monthly subscribed two-node TencentDB for MySQL instance with 4 cores, 8,000 MB memory, and 500 GB disk space in Guangzhou Zone 3 for one month.
- You purchase a monthly subscribed two-node TencentDB for MySQL instance with 4 cores, 8,000 MB memory, and 200 GB disk space in Guangzhou Zone 4 for one month.

Total fees = memory and CPU fees + storage space fees + backup space fees

#### Memory and CPU fees
The monthly subscription price of a 4-core 8,000 MB MEM instance in Guangzhou region is 120 USD/month, so the total memory and CPU fees are 2 * 120 USD/month * 1 month = 240 USD.

#### Storage space fees
The monthly subscription price of instance disk in Guangzhou region is 0.10588235 USD/GB/month, so the storage space fees are (500 GB + 200 GB) * 0.10588235 USD/GB/month * 1 month = 74.12 USD.

#### Backup space fees
If you have a two-node instance with a purchased database storage space of 500 GB/month in Guangzhou Zone 3 and another such instance with 200 GB/month in Guangzhou Zone 4, you will get a free backup space of 700 GB/month in Guangzhou region.

If your data backups reach 800 GB and log backups reach 100 GB in the current hour, your total backup space used in Guangzhou region will exceed 700 GB, and you will be billed for the excess of 200 GB (800 + 100 - 700 = 200) for the current hour and so on.

Hourly backup space fees = 200 GB (the backup space that exceeds the free tier may change over time) * 0.000113 USD/GB/hour = 0.0226 USD

## FAQs
#### Why are additional fees incurred for my monthly-subscribed instance?
Check whether your used backup space exceeds the free tier. Excessive backup space will be charged.
You can view the backup space usage on the database backup page in the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/backup/index). For more information, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).

#### Will idle pay-as-you-go instances be billed?
Yes. If you stop using pay-as-you-go instances, terminate them as soon as possible to avoid further fees.

#### Which types of files are stored in the storage space?
- Data files: The space which your data takes up, including created tables and indexes.
- System files (necessary for the database): Shared tablespaces, error logs, redo logs, undo logs, and data dictionaries.
- Binlogs: Binlogs record all DDL and DML statements (except `SELECT` and `SHOW` statements) and are used to replicate and restore database data. The more data changes, the more binlogs. To reduce the space binlogs take up, they can be [uploaded to COS](https://intl.cloud.tencent.com/document/product/236/40186).

## References
- TencentDB for MySQL instances can be purchased in the console or via APIs. For more information, see [Purchase Methods](https://intl.cloud.tencent.com/document/product/236/5160).
- TencentDB for MySQL sends alert messages to you seven days before it expires and its resources are repossessed. For more information, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/236/5159).
- You can return TencentDB for MySQL instances and request a refund in the console. For more information, see [Refund](https://intl.cloud.tencent.com/document/product/236/14618).
- You can upgrade or downgrade the specifications of TencentDB for MySQL instances. For more information, see [Instance Adjustment Fee](https://intl.cloud.tencent.com/document/product/236/32345).






