<span id="CBS"></span>
## CBS billing overview
### Billing Mode
| Billing mode | Pay as you go |
|---------|---------|
| Payment method | Freezes an hour’s fees during purchase, payment settled once an hour |
| Billing unit | USD/GB\*hour |
| Minimum use duration | Hourly settlement, can be purchased or released at any time |
| Use cases | Applicable where the demand for devices fluctuates dramatically, such as during flash sales on e-commerce sites |

### Billing Standard
Billing standard varies by regions and disk types. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

<span id="Snapshot"></span>
## Snapshot billing overview
Snapshots was **commercialized** on January 22, 2019. After commercialization, all stored snapshots and newly generated snapshots will be billed based on their use of the storage capacity.
> **Note**：
> [Images](https://intl.cloud.tencent.com/document/product/213/4940) uses the CBS snapshot service for data storage. As a result, retaining custom images will occupy a certain portion of your snapshot capacity, and will incur associated costs.

### Billing Mode
Fees are charged according to the total storage capacity of your snapshots. Each region is charged separately. CBS is **pay-as-you-go** on an hourly billing cycle.
For example, you purchase a 100GB cloud disk and write 10GB of data, and there are no other snapshots in the current region. If a snapshot is created at this time, and no other snapshots are created or deleted in the unit of an hour, the snapshot of this hour in this region will be charged as 10GB of storage.

### Billing Standard
Billing standard for snapshots varies by regions. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
### Complimentary Quota
After snapshot commercialization, Tencent Cloud will still provide users with a certain amount of free tier in major regions in China. The free tier policy is as follows:
- The free tier covers mainland China and Hong Kong, China. Overseas regions do not currently have free tier for snapshots.
- When users in one of the regions mentioned above have cloud disks in normal operating status (not in to be repossessed or terminated status), Tencent Cloud provides a 50GB snapshot free tier in this region.
- Time limit of the free tier is 1 year, and we plan to cancel this free tier policy by February 2020.

The following table describes snapshot billing circumstances under different use scenarios of snapshots and cloud disks:

<table>
     <tr>
         <th>Region</th>  
         <th nowrap="nowrap">Total snapshot capacity</th>  
				 <th nowrap="nowrap">Cloud disk quantity and status</th>
				 <th>Snapshot billing circumstances</th>
     </tr>
	 <tr>
         <td nowrap="nowrap">North China (Beijing)</td>
         <td>100GB</td>
				 <td nowrap="nowrap">1 cloud disk<br/>**To be repossessed** status</td>
				 <td><li>Complimentary snapshot quota is not available currently. Total snapshot capacity of 100GB is pay-as-you-go on an hourly billing cycle.</li><li>After the cloud disk is renewed or a new cloud disk is purchased, complimentary quota can be obtained again, and snapshot capacity is pay-as-you-go on an hourly billing cycle as (100GB - 50GB = 50GB).</li></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Southeast Asia (Hong Kong, China)</td>
         <td>60GB</td>
				 <td>1 cloud disk<br/>**Mounted** status</td>
				 <td>Currently has the complimentary snapshot quota, total snapshot capacity is pay-as-you-go on an hourly billing cycle as (60GB - 50GB = 10GB).</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Southeast Asia (Singapore)</td>
         <td>40GB</td>
				 <td>1 cloud disk<br/>**Mounted** status</td>
				 <td>Does not have a complimentary snapshot quota, total snapshot capacity is pay-as-you-go on an hourly billing cycle as 40GB.</td>
     </tr>
</table>

### Freezing Policy
Once your Tencent Cloud account goes into arrears, snapshot-related operations are immediately suspended, including creation, rollback, cross-region replication, and scheduled snapshot policies. After the account has been in arrears for 30 days, all snapshots will be deleted.
