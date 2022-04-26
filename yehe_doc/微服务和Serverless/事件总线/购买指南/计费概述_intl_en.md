>!
> 1. EventBridge is currently in beta test, during which you can use it free of charge.
> 2. EventBridge will start billing from May 9th, 2022.

This document introduces the billing mode and billable items of Tencent Cloud EventBridge.

## Billing Mode
EventBridge is provided in a **Pay-as-you-go** manner.

|**Type**|**Pay-as-you-go**|
|-----|------|
|**Billing mode**| Bill by the number of events published to event buses and settled on an hourly basis|
|**Unit price**| USD/million events |
|**Use cases**| Low or fluctuating message volumes |


## Pricing Details

### Free tier

Events published to **default event buses for Tencent Cloud services** are free of charge.

### Billable items and pricing

#### Fee

You are billed by the number of events published to your **custom event buses**, such as custom applications, message queues and databases. Details are as follows:

<table><tr>
<th rowspan="2"><nobr>Billing Tier</nobr></th>
<th rowspan="2"><nobr>Total Events (Million/Month)</nobr></th>
<th colspan="2"><p align="center">Unit Price (USD/Million) </p></th>
</tr><tr>
<th>Guangzhou, Nanjing, Shanghai, Hangzhou, Shenzhen, Beijing, Chengdu, Chongqing, Tianjin, Changsha</th>
<th>Hong Kong (China), Singapore, Frankfurt, Toronto, Seoul, Silicon Valley</th>
</tr><tr>
<td >Tier 1</td>
<td>N ≤ 1,000</td>
<td>0.64</td>
<td>0.832</td>
</tr><tr>
<td>Tier 2</td>
<td>1,000 < N ≤ 5,000</td>
<td>0.576</td>
<td>0.7488 </td>
</tr><tr>
<td>Tier 3</td>
<td>5,000 < N ≤ 10,000</td>
<td>0.48</td>
<td>0.624</td>
</tr><tr>
<td>Tier 4</td>
<td>10,000 < N ≤ 50,000</td>
<td> 0.416</td>
<td> 0.5408</td>
</tr><tr>
<td>Tier 5</td>
<td>N > 50,000</td>
<td>0.384</td>
<td>0.4992</td>
</tr></table>


Every 64 KB of data is counted as one event. When the data is less than 64 KB, it is rounded up. For example, 256 KB is counted as 4 events, and 220 KB is also counted as 4 events.


## Billing Examples
If you receive 3 million events in a month, with 2 million sent to the default event buses for Tencent Cloud services, and 1 million sent to your custom event buses, you will be billed as follows:

- Total events: 3 million 
- Default Tencent Cloud service events: 2 million (free of charge)
- Custom events: 1 million
- Cost for the current month = 1 million * 0.64 USD / 1 million = 0.64 USD

## Other Fees
You may also need to pay for the usage of other Tencent Cloud services related with EventBridge, such as COS and CKafka. Check the pricing details of the other services in relevant documentations.
