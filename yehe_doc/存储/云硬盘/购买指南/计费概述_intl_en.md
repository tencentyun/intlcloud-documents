
## CBS Billing Overview[](id:CBS)
### Billing modes
Cloud Block Storage is a pay-as-you-go cloud storage service provided by Tencent Cloud.
See the table below for details.

| Billing plan | Pay as you go |
|---------|---------|
| Payment method | A deposit of one hour’s fee is required upon purchase. This service is billed by the hour. |
| Pricing | USD/GB\*hour |
| Minimum usage duration | Charged by the second and billed by the hour. You can purchase or release the service at any time. |
| Use cases | This service is applicable to scenarios where the business demand fluctuates greatly, such as ecommerce flash sales. |

### Pricing
Pricing varies by region and disk type. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).


## Snapshot Billing Overview[](id:Snapshot)
Snapshot service was **commercialized** on January 22, 2019 at 00:00:00. All snapshots are billed based on the storage usage.
>! [Images](https://intl.cloud.tencent.com/document/product/213/4940) use the CBS snapshot service for data storage. As a result, retaining custom images occupies a certain portion of your snapshot capacity and incurs costs.

### Billing modes
You are charged according to the total storage size of your snapshots. Each region is charged separately. CBS is **pay-as-you-go** on an hourly billing cycle.
>?To view the size of your snapshots in each region, go to the [Snapshot console](https://console.cloud.tencent.com/cvm/snapshot/overview).
>





### Pricing
Pricing for snapshots varies by region. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

### Free tier
Tencent Cloud offers 50 GB of storage space for free to users in the Chinese mainland. The detailed policy is as follows:
- The free tier is available to users in regions as listed in the [Snapshot console](https://console.cloud.tencent.com/cvm/snapshot/overview).
- This free tier will be phased out in October 2021.

The following table describes how snapshot storage is billed under different circumstance:

<table>
     <tr>
         <th>Region</th>  
         <th nowrap="nowrap">Total snapshot size</th>  
				 <th nowrap="nowrap">Number of cloud disks</th>
				 <th>Details</th>
     </tr>
	 <tr>
         <td nowrap="nowrap">North China (Beijing)</td>
         <td>100 GB</td>
				 <td nowrap="nowrap">1 cloud disk</td>
				 <td>Eligible for the 50 GB free tier. Total billable snapshot storage size is 100 GB - 50 GB = 50 GB.</td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Hong Kong, Macao and Taiwan, China (Hong Kong)</td>
         <td>60 GB</td>
				 <td>2 cloud disks</td>
				 <td>Eligible for the 50 GB free tier. Total billable snapshot storage size is 60 GB - 50 GB = 10 GB.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Southeast Asia (Singapore)</td>
         <td>40 GB</td>
				 <td>1 cloud disk</td>
				 <td>Not eligible for the free tier. Total billable snapshot storage size is 40 GB.</td>
     </tr>
</table>

### Overdue payment
Once your account becomes overdue, snapshots will go into the **Isolated** status, and service will be suspended. For more information, see [Overdue Policy](https://intl.cloud.tencent.com/document/product/362/31625).

