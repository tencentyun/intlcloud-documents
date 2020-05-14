New COS users are eligible for the following time-limited free tier: 

| User Type | Free Tier | Validity Period |
| -------- | ----------------- | ------ |
| Personal user | 50 GB of standard storage capacity | 6 months |
| Enterprise user | 1 TB of standard storage capacity | 6 months |


## Free Tier

Billable items in COS and the corresponding free tier are as listed in the following table:

<table>
   <tr>
      <th>Fees</th>
      <th>Billable Item</th>
      <th>Available Free Tier</th>
   </tr>
   <tr>
      <td rowspan="4">Storage capacity fees</td>
      <td>MAZ_STANDARD storage capacity</td>
      <td>No</td>
   <tr>
      <td>STANDARD storage capacity</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>STANDARD_IA storage capacity</td>
      <td rowspan="6">No<br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/33776">Billable Items</a></td>
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
      <td rowspan="1">Traffic fees</td>
      <td>Public network downstream traffic, CDN origin-pull traffic, cross-region replication traffic
   </tr>
   <tr>
	     <td rowspan="1">Administrative feature fees</td>
       <td>Inventory fees, extraction fees, batch operation fees, object tagging fees</td>
   </tr>
</table>

>
> - The Free Tier is only applicable to **Public Cloud regions**, but not Finance Cloud regions. For more information, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224).
> - If your service is interrupted due to violations or arrears, you will not be eligible for the Free Tier perk. Free Tier will be unavailable until the service is restarted.

## Billing Sequence

The bill is settled in the order of **free tier > storage pack > pay-as-you-go**.

- By default, COS settles bills in the pay-as-you-go method, i.e., it deducts from the Free Tier first, and then bill the excessive usage (if any) in a **pay-as-you-go** manner.
- If you have purchased a paid storage pack, during the pack’s validity period, COS will deduct from the Free Tier and your paid storage pack first, and then bill the excessive usage (if any) in a **pay-as-you-go** manner.



## Issuance and Query

The free tier will be delivered to your account in the form of a free storage pack after you activate COS. You can view when your Free tier storage pack will take effect and expire in the [Storage Package Management](https://console.cloud.tencent.com/cos5/package) page in the console.

## Calculation of the Validity Period

The **Free Tier Validity Period** is 6 months after you activate COS service.

For example, if you activated COS at 17:13:14 on March 10, 2019, and assume that 6 months is equal to 180 days, then the free tier would be valid for the STANDARD storage capacity between March 10 and September 5, 2019.

## Example

John Smith, a personal user, activated the COS service on March 10, 2019. He uploaded files of 60 GB in standard storage class on March 16, downloaded 10 GB of data through the public network on March 20, and didn't perform any other operations at other times, so:

- He was granted free standard storage capacity of 50 GB per month for 6 months.
- On March 21, 2019, the public network downstream traffic was billed for 10 GB of data.
- On April 1, 2019, the STANDARD storage capacity was billed, and 10 GB of storage capacity in excess of the free tier was used every day from March 16 to March 31 (160 GB in total for 16 days). This value was divided by 31, and the result of 5.16 GB was billed as the STANDARD storage capacity.
- At the beginning of April 2019, the data uploading and downloading requests in March were billed.

In April 2019, John didn't perform any other operations, and the 60 GB of data was retained in COS, so:

- At the beginning of May 2019, the standard storage capacity was billed. The monthly storage capacity was 60 GB, which exceeded the free tier, **so fees for the excessive 10 GB of standard storage capacity were charged**.

>
>
> - This example focuses on the relevant billing details for personal users during the validity period of the free tier. For detailed descriptions of billable items, monthly storage capacity calculation rules, and cost calculation formulas, see [Billable Items](https://intl.cloud.tencent.com/document/product/436/33776).
> - For more billing examples, see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).

## FAQs

For FAQs about billable usage and free tier, see [Billing](https://intl.cloud.tencent.com/document/product/436/10373).
