<span id="CBS"></span>
## Cloud Block Storage (CBS) Billing Overview
### Billing
Cloud Block Storage is a pay-as-you-go cloud storage service provided by Tencent Cloud.

| Billing Plan | Pay as you go |
|---------|---------|
| Payment method | A deposit of one hour’s fee is required upon purchase. This service is billed and charged by the hour. |
| Pricing | USD/GB\*hour |
| Minimum usage duration | One hour. You can purchase or release the service at any time. |
| Use cases | This service is applicable to scenarios where the demand for resources fluctuates dramatically, such as during flash sales on e-commerce sites. |

### Pricing
Pricing varies by region and disk type. For more information, refer to [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

<span id="Snapshot"></span>

## Snapshot Billing Overview
Snapshots were **commercialized** on January 22, 2019. All snapshots are billed based on how much storage space they use.
> [Images](https://intl.cloud.tencent.com/document/product/213/4940) use the CBS snapshot service for data storage. As a result, retaining custom images occupies a certain portion of your snapshot capacity and incurs costs.

### Billing
You are charged according to the total storage capacity of your snapshots. Each region is charged separately. CBS is **pay-as-you-go** on an hourly billing cycle.
For example, assume you purchase a 100 GB cloud disk and write 10 GB of data, and there are no other snapshots in the current region. If a snapshot is created at this time, and no other snapshots are created or deleted by the end of the current billing cycle, you are charged for 10 GB of storage for this snapshot.
### Billing Standard
Pricing for snapshots varies by region. For more information, refer to [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
### Free Tier
Tencent Cloud offers 50 GB of storage space for free to users in China. The detailed policy is as follows:
- The free tier is available to users in Beijing, Shanghai, Guangzhou, Shenzhen Finance Zone, Shanghai Finance Zone, Guangzhou Open, Chengdu, Chongqing, and Hong Kong, China. Other regions do not have a free tier.
- Cloud disks in the aforementioned regions with a status other than `repossessed` or `terminated` get 50 GB of free snapshot storage.
- This free tier will be phased out in July 2020.

The following table describes how snapshot storage is billed under different circumstance:

<table>
     <tr>
         <th>Region</th>  
         <th nowrap="nowrap">Total snapshot size</th>  
				 <th nowrap="nowrap">Cloud disk quantity and status</th>
				 <th>Details</th>
     </tr>
	 <tr>
         <td nowrap="nowrap">North China (Beijing)</td>
         <td>100 GB</td>
				 <td nowrap="nowrap">1 cloud disk<br/>**To be repossessed**</td>
				 <td><li>The only cloud disk in the region is being **Repossessed**. Therefore, the free tier is not applicable. You are billed for the 100 GB snapshot storage on an hourly basis.</li><li>A single cloud disk with the status **Mounted** or **To be mounted** would re-enable the free tier, which would reduce your billable snapshot storage size from 100 GB to 50 GB. To do so, add funds for CBS, or purchase a new cloud disk. </li></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Southeast Asia (Hong Kong, China)</td>
         <td>60 GB</td>
				 <td>2 cloud disks<br/>**To be mounted** and **To be repossessed**</td>
				 <td>Eligible for the free tier. Total billable snapshot storage size is 60 GB - 50 GB = 10 GB.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Southeast Asia (Singapore)</td>
         <td>40 GB</td>
				 <td>1 cloud disk<br/>**Mounted**</td>
				 <td>Not eligible for the free tier. Total billable snapshot storage size is 40 GB.</td>
     </tr>
</table>

### Freezing Policy
Once an account becomes delinquent, all snapshot operations such as create, rollback, cross-region duplication, and scheduled policies, are suspended. Your snapshots are kept for **30 days**. If at the end of 30 days, your account is still delinquent, all snapshots are deleted. You can also [delete them](https://intl.cloud.tencent.com/document/product/362/5758) voluntarily.
>
> - You are still billed for the snapshot storage space used after your account becomes delinquent until the snapshots are terminated.
> - Once snapshots are terminated, the data cannot be restored.
> - Once the overdue payment is paid, snapshot operations are automatically resumed.
> - Delete snapshots you no longer need to avoid additional charges.
