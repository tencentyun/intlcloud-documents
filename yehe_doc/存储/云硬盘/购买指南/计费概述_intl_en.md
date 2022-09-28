
## CBS Billing Overview[](id:CBS)
### Billing Mode
Tencent Cloud provides two cloud disk billing modes to meet different customer needs: monthly subscription and pay-as-you-go.
The differences between these two billing modes are as follows:

| Billing Mode | Monthly Subscription | Pay-as-you-go |
|---------|---------|---------|
| Payment mode | Prepaid | Fees for one billing cycle will be frozen upon purchase, settled every hour |
| Price unit | USD/GB/month | USD/GB/hour|
| Minimum usage duration | Used for at least one month | Charged by the second and billed by the hour. You can purchase or release the service at any time. |
| Use cases | Suitable for businesses with stable and long-term device demands | Suitable for scenarios where the demand for devices fluctuates significantly, such as flash sale campaigns on an e-commerce site |

### Billing Standards
Pricing varies by region and disk type. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).


## Snapshot Billing Overview[](id:Snapshot)
Snapshot service was **commercialized** on January 22, 2019 at 00:00:00. All snapshots are billed based on the storage usage.

<dx-alert infotype="notice" title="">
[Images](https://intl.cloud.tencent.com/document/product/213/4940) use the CBS snapshot service for data storage. As a result, retaining custom images occupies a certain portion of your snapshot capacity and incurs costs.
</dx-alert>


### Billing Mode
You are charged according to the total storage size of your snapshots. Each region is charged separately. CBS is **pay-as-you-go** on an hourly billing cycle.

<dx-alert infotype="explain" title="">
To view the size of your snapshots in each region, go to the [Snapshot console](https://console.cloud.tencent.com/cvm/snapshot/overview).
</dx-alert>




### Billing Standards
Pricing for snapshots varies by region. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

### Free Tier

After the commercialization of snapshots, Tencent Cloud still provides users with a free tier of 80 GB in regions in China. The part beyond the free tier is postpaid on an hourly basis. For billing standards, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413#Snapshot). Note the following:
- The free tier is available to users in regions as listed in the [Snapshot console](https://console.cloud.tencent.com/cvm/snapshot/overview).
- The free snapshot tier will be canceled in the future. For more information, check the [CBS](https://www.tencentcloud.com/document/product/362) product page regularly.

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
				 <td>Eligible for the 80 GB free tier. Total billable snapshot storage size is 100 GB - 80 GB = 20 GB.</li></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Hong Kong, Macao and Taiwan, China (Hong Kong)</td>
         <td>90 GB</td>
				 <td>2 cloud disks</td>
				 <td>Eligible for the 80 GB free tier. Total billable snapshot storage size is 90 GB - 80 GB = 10 GB.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Southeast Asia (Singapore)</td>
         <td>40 GB</td>
				 <td>1 cloud disk</td>
				 <td>Not eligible for the free tier. Total billable snapshot storage size is 40 GB.</td>
     </tr>
</table>

### Overdue Payment
Once your account becomes overdue, snapshots will go into the **Isolated** status, and service will be suspended. For more information, see [Overdue Policy](https://intl.cloud.tencent.com/document/product/362/31625).

