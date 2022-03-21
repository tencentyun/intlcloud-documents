## Overview
Tencent Cloud COS offers a limited Free Tier to all new customers, that is, all the first time users of COS. This Free Tier applies to STANDARD storage usage charges for data stored in the **STANDARD** storage class. See more details in the table below: 

| User Type | Free Tier          | Term |
| -------- | ----------------- | ------ |
| All new customers | 50 GB of STANDARD storage usage | 6 months |

>?The storage capacity is calculated in binary, for example, 1 TB = 1024 GB.

## Free Tier

The Free Tier is only applicable to **Public Cloud regions**. For more information, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

The table below shows COS [billable items](https://intl.cloud.tencent.com/document/product/436/33776) and whether the Free Tier is available to them.

> !
>
>- The free tier is not applicable to any STANDARD_IA or ARCHIVE billable items including storage usage, requests, and traffic, and any other STANDARD billable items than **STANDARD storage usage**.
>- If your service is suspended due to violations or overdue payment, you will not be eligible for the Free Tier perk. Free Tier will be unavailable until the service is restarted.

<table>
   <tr>
      <th>Fees</th>
      <th>Billable Item</th>
      <th>Available Free Tier</th>
   </tr>
   <tr>
      <td rowspan="5">Storage Usage Fees</td>
      <td>INTELLIGENT TIERING storage usage</td>
      <td>No</td>
   </tr>
   <tr>   
      <td>STANDARD storage usage</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>STANDARD_IA storage usage</td>
      <td rowspan="7">No<br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/33776">Billable Items</a></td>
   </tr>
   <tr>
      <td>Archive storage usage</td>
   </tr>
   </tr>
   <tr>
      <td>DEEP ARCHIVE storage usage</td>	
   <tr>
      <td>Request Fees</td>
      <td>Number of requests</td>
   </tr>
   <tr>
      <td>Data Retrieval Fees</td>
      <td>Amount of data retrieved </td>
   </tr>
   <tr>
      <td rowspan="1">Traffic Fees</td>
      <td>Public network downstream traffic, CDN origin-pull traffic, Cross-region replication traffic, Global acceleration traffic
   </tr>
   <tr>
	     <td rowspan="1">Management Feature Fees</td>
       <td>Inventory feature fees, Select feature fees, Batch operation fees, Object tagging fees</td>
   </tr>
</table>




## Access and Query
You receive the benefits of COS free tier in the format of storage pack automatically after you sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and activate COS service in the [console](https://console.cloud.tencent.com/cos5). 


## Validity Period

The **Free Tier** is valid for 6 months after the activation of your COS service.

For example, if you activated COS at 17:13:14 on March 10, 2019, and assume that 6 months is equal to 180 days, then the free tier would cover your STANDARD storage usage between March 10 and September 5, 2019.


## Billing Sequence

During the free tier term, you may be charged other fees you incur, such as request, traffic and other basic fees. Therefore, the billing sequence varies for your billing settlement depending on the scenario.

- By default, COS bills are settled in a pay-as-you-go manner.
- If you are eligible for the free tier for STANDARD storage usage, and have no storage pack available, you are charged in a pay-as-you-go manner only for the usage exceeding the free tier.


## Example

John Smith, a new user, activated the COS service on March 10, 2019. He uploaded files of 60 GB in standard storage class on March 16, downloaded 10 GB of data through the public network on March 20, and didn't perform any other operations at other times, so:

- He was granted free STANDARD storage usage of 50 GB per month for 6 months.
- On March 21, 2019, the public network downstream traffic was billed for 10 GB of data.
- On April 1, 2019, the STANDARD storage usage was billed, and 10 GB of storage usage in excess of the free tier was used every day from March 16 to March 31 (160 GB in total for 16 days). This value was divided by 31, and the result of 5.16 GB was billed as the STANDARD storage usage.
- At the beginning of April 2019, the data uploading and downloading requests in March were billed.

In April 2019, John didn't perform any other operations, and the 60 GB of data was retained in COS, so:

- At the beginning of May 2019, the standard storage capacity was billed. The monthly storage capacity was 60 GB, which exceeded the free tier, **so fees for the excessive 10 GB of standard storage capacity were charged**.


> ?The above example applies to scenarios where a new user has activated the COS service for the first time, and is eligible for the free tier. For billing after the free tier term ends, see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).
## Troubleshooting

Should you have any questions about the free tier or your bills, see [Billing](https://intl.cloud.tencent.com/document/product/436/10373).
