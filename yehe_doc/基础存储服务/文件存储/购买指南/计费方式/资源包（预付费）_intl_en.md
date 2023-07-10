CFS can be billed using the pay-as-you-go mode (postpaid) or a resource pack (prepaid). This document introduces billing via a resource pack, which has a fixed storage capacity and duration.

## Billing Description

<table>
   <tr>
      <th>Billable Item</th>
      <th>Billing Method</th>
      <th>Billing Cycle</th>
      <th>Description</th>
   </tr>
     <tr>
      <td>Storage usage</td>
      <td>Resource pack (prepaid)</td>
      <td>Monthly subscription</td>
      <td>A valid resource pack can be used to offset the corresponding pay-as-you-go fees.</td>
   </tr>
</table>



## Purchase Notes

- Currently, only the Standard and High-Performance storage classes support resource packs, and only CNY accounts can purchase them. For more information, please see [Available Regions](https://intl.cloud.tencent.com/document/product/582/35772).
- **A resource pack takes effect once it’s bound to a file system and can only offset fees incurred by this single file system, which cannot be unbound while the resource pack is valid. In addition, using resource packs across availability zones (AZs) is not supported yet**. Therefore, before you purchase a resource pack, double check the file system you want to bind to as well as the AZ of the resource pack.
- Once bound to a file system, a resource pack will take effect (no refunds allowed) and its effective period will be calculated by month. If needed, you can delete the file system bound, changing the status of the resource pack to “Unused” and suspending its effective period. After you bind the resource pack to another file system, it will take effect again using its remaining effective period.
- You can purchase multiple CFS resource packs, although each file system can only be bound to one resource pack of the same type at a time. If needed, you can upgrade or renew the resource pack.
- A file system redeemed with a storage pack will have the corresponding throughput performance. If you have a low data volume but require high throughput, you can purchase a resource pack to increase the upper threshold of the throughput for your file system. For more information, please see [Storage Class and Performance Specification](https://intl.cloud.tencent.com/document/product/582/33745).
- While the resource pack is effective, bills will be settled in the following sequence: free tier > resource pack > pay-as-you-go. Usage beyond the free tier and the resource pack’s capacity will be billed using the pay-as-you-go mode.
- If an account has overdue payments (the account’s balance is below 0), the CFS service will be suspended after 24 hours, regardless of whether the resource pack is effective or not.


## Resource Pack Pricing 

>? The unit prices for the NFS and the CIFS/SMB file systems are the same.
>

<table>
   <tr>
      <th rowspan="2">Storage Class</th>
      <th rowspan="2">Region</th>
      <th rowspan="2">Specification</th>
      <th nowrap="nowrap">1-Month</th>
      <th nowrap="nowrap">6-Month</th>
      <th nowrap="nowrap">12-Month</th>
   </tr>
      <tr>
      <th nowrap="nowrap">Price (USD)</th>
      <th nowrap="nowrap">Price (USD)</th>
      <th nowrap="nowrap">Price (USD)</th>
   </tr>
    <tr>
      <td rowspan="8">High-Performance</td>
      <td rowspan="8">The Chinese mainland</td>
   <tr>
      <td>50 GB</td>
      <td>12</td>
      <td>62.4</td>
      <td>117</td>
   </tr>
   <tr>
      <td>200 GB</td>
      <td>48</td>
      <td>249.6</td>
      <td>468</td>
   </tr>
  <tr>
      <td>500 GB</td>
      <td>118</td>
      <td>624</td>
      <td>1,170</td>
   </tr>
     <tr>
      <td>2 TB</td>
      <td>485</td>
      <td>2,396.2</td>
      <td>4,153</td>
   </tr>
   <tr>
      <td>5 TB</td>
      <td>1,185</td>
      <td>5,990.4</td>
      <td>10,383</td>
   </tr>
   <tr>
      <td>20 TB</td>
      <td>4,739</td>
      <td>23,961.6</td>
      <td>41,533</td>
   </tr>
      <tr>
      <td>50 TB</td>
      <td>11,182</td>
      <td>55,910.4</td>
      <td>95,846</td>
   </tr>
      <tr>
      <td rowspan="8">Standard</td>
      <td rowspan="8">The Chinese mainland</td>
      <td>50 GB</td>
      <td>3</td>
      <td>15</td>
      <td>26</td>
   </tr>
   <tr>
      <td>200 GB</td>
      <td>10</td>
      <td>52</td>
      <td>90</td>
   </tr>
   <tr>
      <td>500 GB</td>
      <td>23</td>
      <td>115</td>
      <td>205</td>
   </tr>
  <tr>
      <td>2 TB</td>
      <td>93</td>
      <td>470</td>
      <td>848</td>
   </tr>
     <tr>
      <td>5 TB</td>
      <td>232</td>
      <td>1,167</td>
      <td>2,110</td>
   </tr>
   <tr>
      <td>20 TB</td>
      <td>862</td>
      <td>4,347</td>
      <td>7,868</td>
   </tr>
   <tr>
      <td>50 TB</td>
      <td>2,156</td>
      <td>10,869</td>
      <td>19,635</td>
   </tr>
      <tr>
      <td>100 TB</td>
      <td>4,205</td>
      <td>20,953</td>
      <td>37,916</td>
   </tr>
</table>

>?
> - Currently, High-Performance file systems are still in beta testing and are not available to the general public.
> - Currently, the Turbo series cannot be billed using a resource pack (prepaid).
> 


## Examples

#### The effective period and the file system performance of resource packs

Suppose that you purchased two High-Performance storage packs (Guangzhou Zone 3, 200 GB, **3-month effective period**) at 14:30 on July 15, 2020 and bound them to file system A and file system B, respectively.
- The two storage packs will be used to offset 200 GB of usage for file systems A and B, respectively, with the effective period of 14:30 on July 15, 2020 to 13:29 on October 15, 2020.
- If file system A has used 500 GB of storage and file system B has used 100 GB, the throughput upper threshold of A will be 500 × 0.2 + 200 = 300 MB/s and the throughput upper threshold of B will be 200 × 0.2 + 200 = 240 MB/s.

#### Resource pack effective period

Suppose that you purchased a **High-Performance storage pack** (**Guangzhou Zone 3, 200 GB**, 3-month effective period) at 14:30 on July 15, 2020 and bound it to a 300 GB High-Performance file system. From 14:00 to 15:00 on July 15, 2020, a total of **800 GB of High-Performance storage usage** and **3,000 GB of Standard storage usage** was used.
- The **200 GB of High-Performance storage usage** will be offset by your resource pack.
- The remaining **600 GB of High-Performance storage usage and 3,000 GB of Standard storage usage** will be billed using the pay-as-you-go billing mode.

  

