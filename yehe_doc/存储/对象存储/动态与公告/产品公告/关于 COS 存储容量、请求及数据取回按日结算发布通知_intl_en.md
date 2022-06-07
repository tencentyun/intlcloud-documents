## Overview

Starting from July 1, 2022, the settlement cycle of COS **storage usage, request, and data retrieval** billable items will be changed from **monthly** to **daily** for you to better manage your fees. This change will be performed on a rolling basis. The change time will be as notified to you by Message Center, email, or SMS. The generated bills will remain unchanged and you do not need to perform any operations.

>?
>Billing mode and billing cycle: COS is pay-as-you-go (postpaid) by default.
> - Monthly settled resources: Fees incurred from 00:00 on January 1 to 23:59 on January 31 will be deducted on February 1. The record will be posted to the bill for February by deduction cycle and to the bill for January by billing cycle. 
> - Daily settled resources: Fees incurred from 00:00 to 23:59 on January 31 will be deducted on February 1. The record will be posted to the bill for February by deduction cycle and to the bill for January by billing cycle.

## Release Time

Starting from July 1, 2022, the settlement cycle will be changed from monthly to daily on a rolling basis. The change time will be as notified to you by Message Center, email, or SMS. After the change is completed, the bill for a day will be issued the next day. We recommend you pay attention to the bill changes.

## Change Details

### Billing cycle

| Billable Item                               | Before Change                          | After Change                         |
| ------------------------------------ | ------------------------------- | ------------------------------ |
| Storage usage, request, and data retrieval | Settled monthly. Fees incurred in a month will be settled and billed on the first day of the next month. | Settled daily. Fees incurred on a day will be settled and billed on the next day.       |
| Traffic and management feature              | Settled daily. Fees incurred on a day will be billed on the next day.  | Unchanged.   |


### Unit prices of billable items

The unit prices of billable items after this change are as described below:

<table>
<thead>
<tr>
<th width="10%">Billable Item</th>
<th>Description</th>
<th>Pricing</th>
<th>Billing Cycle</th>
</tr>
</thead>
<tbody><tr>
<td>Storage usage</td>
<td>Billed by storage usage and storage period</td>
<td>The price in USD/GB/month is relevant to the billing cycle, where "month" refers to 30 days. If settled daily, the price needs to be converted as follows: daily unit price = monthly unit price / 30. For example, if the monthly unit price of STANDARD storage usage in Beijing region is 0.024 USD/GB/month, its daily unit price is 0.024 / 30 = 0.0008 USD/GB/day.</td>
<td>Daily</td>
</tr>
<tr>
<td>Request</td>
<td>Billed by the number of requests sent to COS</td>
<td>The price in USD/10,000 requests is irrelevant to the billing cycle. The price does not need to be converted if settled daily. For example, if the price of STANDARD read and write requests in Beijing region is 0.002 USD/10,000 requests, it remains unchanged no matter whether settled daily or monthly.</td>
<td>Daily</td>
</tr>
<tr>
<td>Data retrieval</td>
<td>Billed by the actual amount of retrieved data</td>
<td>The price in USD/GB is irrelevant to the billing cycle. The price does not need to be converted if settled daily. For example, if the price of STANDARD_IA data retrieval in Beijing region is 0.002 USD/GB, it remains unchanged no matter whether settled daily or monthly.</td>
<td>Daily</td>
</tr>
</tbody></table>

>?
>- Storage usage: It will be billed **by month of 30 days** if settled monthly or by the **actual number of days in each month** if settled daily.
>- Notes on bill fluctuations: Even if the monthly usage remains the same, the storage usage fees will still fluctuate. If you use storage capacity for a whole month, the usage will be billed by 31 days for January, 28 (or 29) days for February, and 30 days for April.

### Billing formula

After this change, the billing formula of each billable item for different settlement cycles are as described below:

<table>
   <tr>
      <th>Billable Item</th>
      <th>Subitem</th>
      <th>Billing Formula</th>
      <th>Billing Cycle</th>
   </tr>
   <tr>
      <td rowspan=2>Storage usage</td>
      <td rowspan=2>Storage usage</td>
      <td>Storage usage fees = monthly storage usage unit price * monthly storage usage</td>
      <td>Monthly</td>
   </tr>
   <tr>
      <td>Storage usage fees = daily storage usage unit price * daily storage usage = monthly storage usage unit price / 30 * sum of 5-minute storage usage / 288</td>
      <td>Daily</td>
   </tr>
   <tr>
      <td rowspan=8>Request</td>
      <td rowspan=2>Read request</td>
      <td>Read request fees = unit price per 10,000 requests * monthly accumulated number of requests / 10,000</td>
      <td>Monthly</td>
   </tr>
   <tr>
      <td>Read request fees = unit price per 10,000 requests * daily accumulated number of requests / 10,000</td>
      <td>Daily</td>
   </tr>
   <tr>
      <td rowspan=2>Write request</td>
      <td>Write request fees = unit price per 10,000 requests * monthly accumulated number of requests / 10,000</td>
      <td>Monthly</td>
   </tr>
   <tr>
      <td>Write request fees = unit price per 10,000 requests * daily accumulated number of requests / 10,000</td>
      <td>Daily</td>
   </tr>
   <tr>
      <td rowspan=2>Retrieval request</td>
      <td>Retrieval request fees = unit price per 10,000 requests * monthly accumulated number of requests / 10,000</td>
      <td>Monthly</td>
   </tr>
   <tr>
      <td>Retrieval request fees = unit price per 10,000 requests * daily accumulated number of requests / 10,000</td>
      <td>Daily</td>
   </tr>
   <tr>
      <td rowspan=2>Object monitoring</td>
      <td>Object monitoring fees = unit price per 10,000 monitored objects * monthly accumulated number of objects / 10,000</td>
      <td>Monthly</td>
   </tr>
   <tr>
      <td>Object monitoring fees = unit price per 10,000 monitored objects / 30 * daily accumulated number of objects / 10,000</td>
      <td>Daily</td>
   </tr>
   <tr>
      <td rowspan=2>Data retrieval</td>
      <td rowspan=2>Data retrieval</td>
      <td>Data retrieval fees = unit price per GB * monthly amount of retrieved data</td>
      <td>Monthly</td>
   </tr>
   <tr>
      <td>Data retrieval fees = unit price per GB * daily amount of retrieved data</td>
      <td>Daily</td>
   </tr>
</table>

## FAQs

### How do I view bills?

You can log in to the Tencent Cloud console to view and download bills in [Billing Center > Bills](https://console.cloud.tencent.com/expense/bill/overview).

**Directions**

1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/).
2. Click **[Billing Center](https://console.cloud.tencent.com/expense)** in the top-right corner to enter the overview page.
3. Click **Bills** > **[Bill Details](https://console.cloud.tencent.com/expense/bill/summary)** to enter the **Bill Details** page.
4. On the **Bill by Instance** tab, select **COS** from the drop-down list to view your COS usage by region, billing mode, transaction type, etc.
5. Download bills in **[Download Center](https://console.cloud.tencent.com/expense/bill/downloadCenter)**.

### How do I view prices?

For the pay-as-you-go (postpaid) pricing of COS, see [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos). You can also estimate your costs by using the [Price Calculator](https://buy.cloud.tencent.com/price/cos/calculator).

### How do I view the information of billable items?

For more information on COS billable items, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/436/32534). For more information on the billable items involved in this change, see the following documents:
- [Storage Usage Fees](https://intl.cloud.tencent.com/document/product/436/40099)
- [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100)
- [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097)


## Questions?

If you have any questions about this change, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.