
## Billing Mode
TencentDB for SQL Server offers the following billing mode:

| Billing Mode | Payment Mode | Use Case |
|---------|---------|---------|
| Pay-as-you-go | In this [postpaid](https://intl.cloud.tencent.com/document/product/555/30328) billing mode, you can apply for resources for on-demand use and will be charged based on the actual usage at the billing time. | It is suitable for instantaneously fluctuating businesses. In this mode, instances can be released immediately after the use to save costs. |

## Instance Pricing
### Billing formula
**Total fees = instance specification fees + storage space fees + backup space fees**

### Billable items
<table>
<thead><tr><th width="15%">Billable Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Instance specification fees<br></td>
<td>The instance specification selected on the purchase page is pay-as-you-go. <li>For primary instance specification pricing, see <a href="https://intl.cloud.tencent.com/document/product/238/8294" target="_blank">Product Pricing</a>. <li>For read-only instance specification pricing, see <a href="https://www.tencentcloud.com/document/product/238/53999" target="_blank">Read-Only Instance Specification Pricing</a>.</td>
</tr>
<tr>
<td>Storage space fees</td>
<td>The disk capacity selected on the purchase page is pay-as-you-go. <li>For primary instance storage pricing, see <a href="https://intl.cloud.tencent.com/document/product/238/8294#ZSLCCJG" target="_blank">Product Pricing</a>. <li>For read-only instance storage pricing, see <a href="https://www.tencentcloud.com/document/product/238/53999#ZDSLCCJG" target="_blank">Read-Only Instance Storage Pricing</a>.</td>
</tr>
<td>Backup space fees</td>
<td>The backup space is used to store the backup files of all TencentDB for SQL Server instances in a region, including automatic data backups, manual data backups, and log backups. <li>For local backup pricing, see <a href="https://intl.cloud.tencent.com/document/product/238/45849" target="_blank">Backup Space Billing</a>. <li>For the storage and traffic fees incurred by cross-region backup, see <a href="https://intl.cloud.tencent.com/document/product/238/50229" target="_blank">Cross-Region Backup Billing</a>.</td>
</tr>
</tbody></table>



>?TencentDB for SQL Server provides you with a free tier of backup space for each region, which equals to the sum of the storage space of all your primary single-node (formerly Basic Edition) and two-node (formerly High Availability/Cluster Edition) instances in the region. This free tier is not applicable to cross-region backup files, which all incur fees. Billing for excess backup space beyond the free tier started at 00:00 on July 10, 2022.
