## Performance Description
Data Lake Compute private clusters are billed by compute unit (CU). A CU offers a computing power approximately equal to that of a 1-core 4 GB MEM server. You can estimate the number of required CUs based on your actual business conditions or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Billing Modes
Data Lake Compute supports pay-as-you-go and monthly subscription billing modes as detailed below. For more information, see [Postpaid Billing](https://intl.cloud.tencent.com/document/product/555/30328) and [Prepaid Billing](https://intl.cloud.tencent.com/document/product/555/42701) respectively.

<table>
<thead>
<tr>
<th>Data Engine Type</th>
<th>Billing Mode</th>
<th>Description</th>	
</tr>
</thead>
<tbody>
<tr>
<td>Public engine</td>
<td>Pay-as-you-go</td>
<td><li> Requires no configuration management. <li> Incurs no fees when idle and is billed by scanned data volume. <li> Works well in temporary computing scenarios with a small amount of data.</td>
</tr>
<tr>
<td rowspan=2>Private engine</td>
<td>Pay-as-you-go</td>
<td><li> Scales private resources elastically as needed. <li> Incurs no fees when suspended and is billed by used CUs. <li> Works well in irregular computing scenarios with a fixed amount of data.</td>
</tr>
<tr>
<td>Monthly subscription</td>
<td><li>Scales private resources elastically as needed. <li>Makes available at any time with no need of startup. The elastically scaled resources are pay-as-you-go. <li>Works well in stable computing tasks with a large amount of data.</td>
</tr>
</tbody></table>

Data Lake Compute provides data storage capabilities. To try them out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
When you use Data Lake Compute, data stored to COS will be billed according to the billing rules of COS.



## Pricing
### Public engine
A public engine is billed by scanned data volume in successful query tasks, with a bill generated every clock-hour. You can view specific bills in the [Billing Center](https://console.cloud.tencent.com/expense/overview).
<b>Public engine fees = hourly scanned data volume * unit price</b>

| Billable Item | Price (USD/GB) | 
|---------|---------|
| Scanned data volume	| 0.0045| 

>! 
>- Fees will be incurred if the query task succeeds or the task is manually canceled but data is scanned. No fees will be incurred when resources are being scheduled or if the query task fails.
>- If less than 34 MB of data is scanned for a single SQL task, it will be billed as 34 MB (about 0.00015 USD).

When you use a public engine, since Data Lake Compute adopts serverless architecture, it needs to schedule compute resources for task execution for the first time over a period of time, which may take a longer time.

### Private engine
>! To purchase a data engine with more than 128 CUs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance, and we will reserve resources for you.

#### Pay-as-you-go
A data engine is pay-as-you-go and elastically scalable. When you purchase it, the system will freeze the fees for 1-hour usage of the minimum cluster specification. A bill will be generated every clock-hour. You can view specific bills in the [Billing Center](https://console.cloud.tencent.com/expense/overview).

<b>Private engine fees = hourly number of used CUs * unit price</b>
>! In pay-as-you-go billing mode, the engine will keep running at the purchased minimum cluster count. You can suspend the engine when you don't need to use clusters in order to avoid fees.

#### Monthly subscription
In monthly subscription billing mode, the engine will keep running at the purchased minimum cluster count. If elastic scaling is triggered, added cluster resources will be pay-as-you-go. You can view specific bills in the [Billing Center](https://console.cloud.tencent.com/expense/overview). A monthly subscribed engine won't incur pay-as-you-go fees if it is not scaled.

<b>Monthly subscription fees = cluster specification * minimum cluster count * number of purchase months * monthly subscription unit price</b>

<b>Monthly subscription scaling fees = cluster specification * number of added clusters * pay-as-you-go unit price</b>

Example: If you purchase a monthly subscribed private data engine with a specification of 16 CUs, a minimum cluster count of 2, and a maximum cluster count of 5 for one month, the monthly subscription fees will be 16 * 2 * 1 * 22 = 704 USD, and the engine will run for one month with two 16-CU clusters without incurring additional fees. If the engine is scaled out to five clusters for one hour, then three added 16-CU clusters will incur pay-as-you-go fees of 16 * (5 - 2) * 1 * 0.05 = 2.4 USD.


#### Unit price
>? The available regions are as displayed on the purchase page.

The prices of Data Lake Compute CU in different regions are as follows:

| Region | Monthly Subscription Price (USD/CU/Month) | Pay-as-You-Go Price (USD/CU/Hour) |
|---------|---------|---------|
| Hong Kong (China)	| 22	| 0.05 | 
