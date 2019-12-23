New COS users are eligible for the following limited-time free tier: 

| User Type | Free Tier | Validity Period |
| -------- | ----------------- | ------ |
| Personal user | 50 GB of standard storage capacity | 6 calendar months |
| Corporate user | 1 TB of standard storage capacity | 6 calendar months |

## Free Tier

Billable items in COS and the corresponding free tier are as listed in the following table:

<table>
   <tr>
      <th>Fees</th>
      <th>Billable Item</th>
      <th>Available Free Tier</th>
   </tr>
   <tr>
      <td rowspan="3">Storage capacity fees</td>
      <td>Standard storage capacity</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Standard_IA storage capacity</td>
      <td rowspan="7">No<br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/16871">Billing Overview</a></td>
   </tr>
   <tr>
      <td>Archive storage capacity</td>
   </tr>
   <tr>
      <td>Request fees</td>
      <td>Number of requests</td>
   </tr>
   <tr>
      <td>Data retrieval fees</td>
      <td>Volume of retrieved data</td>
   </tr>
   <tr>
      <td rowspan="3">Traffic fees</td>
      <td>Public network downstream traffic</td>
   </tr>
   <tr>
      <td>CDN origin-pull traffic</td>
   </tr>
   <tr>
      <td>Cross-region replication traffic</td>
   </tr>
</table>

> 
>
> - The free tier is only applicable to **public cloud regions** but not finance cloud regions. For more information, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
> - If you already receives a discount, the cost is calculated based on the discount price and your account would not be eligible for the Free Tier.
> - If your service is interrupted due to violations or arrears, you will not be eligible for the Free Tier perk. Free Tier will be unavailable until the service is restarted.

## Billing Sequence

At the time of bill settlement, the system will settle in the order of **free tier > pay-as-you-go billing**.

By default, the system uses the pay-as-you-go billing method for bill settlement, i.e., the system will deduct the free tier first and then bill the excessive usage (if any) in a **pay-as-you-go** manner.


## Issuance and Query

The free tier will be delivered to your account in the form of a free storage pack after you activate COS.

## Calculation of the Validity Period

**Free tier** is valid for 6 calendar months after you activate COS, including the month of activation.

For example, if you activate COS at 17:13:14 on February 10, 2019, then the free tier will be valid for the standard storage capacity between February and July 2019 as the standard storage capacity is settled on a monthly basis.

## Example

John Smith, a personal user, activated the COS service on March 10, 2019. He uploaded files of 60 GB in standard storage class on March 16, downloaded 10 GB of data through the public network on March 20, and didn't perform any other operations at other times, so:

- He was granted free standard storage capacity of 50 GB per month for 6 months.
- On March 21, 2019, the public network downstream traffic was billed for 10 GB of data.
- At the beginning of April 2019, the standard storage capacity was billed. As the files of 60 GB was only stored for half a month in March, the monthly storage capacity was about 30 GB, which was within the free tier; therefore, no standard storage capacity fees were charged.
- At the beginning of April 2019, the data uploading and downloading requests in March were billed.

In April 2019, John didn't perform any other operations, and the 60 GB of data was retained in COS, so:
- At the beginning of May 2019, the standard storage capacity was billed. The monthly storage capacity was 60 GB, which exceeded the free tier, **so fees for the excessive 10 GB of standard storage capacity were charged**.

>
>- This example focuses on the relevant billing details for personal users during the validity period of the free tier. For detailed descriptions of billable items, monthly storage capacity calculation rules, and cost calculation formulas, see [Billable Items](https://intl.cloud.tencent.com/document/product/436/16871).
>- For more billing examples, see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).

## FAQs

For FAQs about billable usage and free tier, see [Billable Usage](https://intl.cloud.tencent.com/document/product/436/10373).
