This document describes the pricing details and free tiers of each billable item of TDMQ for Pulsar virtual cluster.

## Pay-as-You-Go

### API call price

TDMQ for Pulsar virtual cluster adopts tiered pricing for API calls. <b>API call fees = (number of API calls for message sending + number of API calls for message consumption) * API call unit price</b>.

The unit price of API call (USD/million calls) is as shown below:

<table><tr>
<th rowspan="2"><nobr>Billing Tier</nobr></th>
<th rowspan="2"><nobr>API Calls (Million/Month)</nobr></th>
<th colspan="3"><p align="center">Call Unit Price (USD/Million Calls) </p></th>
</tr><tr>
<th>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu</th>
<th>Hong Kong (China), Singapore, Seoul, Silicon Valley, Toronto, Frankfurt</th>
<th>Shenzhen Finance, Beijing Finance</th>
</tr><tr>
<td>Tier 1</td>
<td>N ≤ 1,000</td>
<td>0.3265</td>
<td>0.2512</td>
<td>0.4019</td>
</tr><tr>
<td>Tier 2</td>
<td>1,000 < N ≤ 5,000</td>
<td>0.2939</td>
<td>0.226</td>
<td>0.3617</td>
</tr><tr>
<td>Tier 3</td>
<td>5,000 < N ≤ 10,000</td>
<td>0.2449</td>
<td>0.1884</td>
<td>0.3014</td>
</tr><tr>
<td>Tier 4</td>
<td>10,000 < N ≤ 50,000</td>
<td>0.2122</td>
<td>0.1633</td>
<td>0.2612</td>
</tr><tr>
<td>Tier 5</td>
<td>N > 50,000</td>
<td>0.1959</td>
<td>0.1507</td>
<td>0.2411</td>
</tr></table>


The maximum message body size is 5 MB, and the number of API calls is calculated at different rates according to the message size:

| Message Size | Rate |
|:----------|:----------|
| N ≤ 2 KB          | 1    |
| 2 KB < N ≤ 4 KB    | 2    |
| 4 KB < N ≤ 16 KB   | 4    |
| 16 KB < N ≤ 100 KB | 16   |
| 100 KB < N ≤ 1 MB  | 64   |
| 1 MB < N ≤ 5 MB    | 256  |

For example, one 10 KB message (publishing or subscribing) request will be charged as **4** API calls.
<dx-alert infotype="explain" title="">
The number of API calls for consuming messages refers to the number of messages pushed by the broker to consumers, which may be numerically greater than the number of messages actually acknowledged by consumers. Scenarios where this happens include: <ol style = "margin-bottom: 0px;">
<li>When a large number of messages are retained, consumers will prefetch a certain number of messages during connection, and multiple unacknowledged messages will be recorded as multiple API calls for consuming messages. In this case, the number of API calls for consuming messages will be greater than the number of messages actually acknowledged by consumers.</li>
<li>When tag messages are consumed, multiple consumers are usually started. In this case, the number of API calls for consuming messages will be greater than the number of messages actually acknowledged by consumers.</li></ol>
</dx-alert>




### Message storage price

TDMQ for Pulsar virtual cluster adopts linear billing for message storage. <b>Message storage fees = message storage size * message storage unit price</b>.
>? TDMQ for Pulsar stores a message in three copies by default. Therefore, the billable storage capacity is three times of the total message size.
>
The unit price of message storage (USD/GB/hour) is as shown below:

| Region | Guangzhou, Shanghai, Nanjing, Beijing, Chengdu | Hong Kong (China), Singapore, Seoul, Silicon Valley, Toronto, Frankfurt | Shenzhen Finance, Beijing Finance |
| :------------------- | :--------------------------- | :--------------------------------------------- | :----------------- |
| Unit price (USD/GB/hour) | 0.0003                       | 0.0003                                         | 0.0006             |

>?
>1. When the message retention policy is set to persistent retention, even if a message is consumed, it will still be persistently stored according to the maximum retention time, resulting in additional message storage fees.
>2. In TDMQ for Pulsar, message data is stored on the Bookie storage node of the BookKeeper cluster in the form of ledger. Even if deletion after consumption is configured, when the ledger is turned on, the async cleaner will not clear the message data. If some messages are not consumed for a long time, other messages in the same ledger may keep consuming the storage space, resulting in additional message storage fees.

### Partition topic resource usage price

TDMQ for Pulsar virtual cluster adopts linear billing for partition topic resource usage. <b>Partition topic resource usage fees = number of partition topics * partition topic resource usage unit price</b>.

The number of partition topics in TDMQ for Pulsar refers to the sum of all partitions of all topics; that is, if there are two three-partition topics, the number of partition topics is 2 * 3 = 6.

The unit price of partition topic resource usage (USD/piece/day) is as shown below:

| Region | Guangzhou, Shanghai, Nanjing, Beijing, Chengdu | Hong Kong (China), Singapore, Seoul, Silicon Valley, Toronto, and Frankfurt | Shenzhen Finance, Beijing Finance |
| :----------------- | :--------------------------- | :--------------------------------------------- | :----------------- |
| Unit price (USD/piece/day) | 0.025                        | 0.032                                          | 0.040              |

>!The partition topic resource usage fees in TDMQ for Pulsar virtual cluster are charged by day; that is, a partition topic resource created at any time on a natural day will incur a full day's fees on the next natural day even if its actual usage time is less than 24 hours.

## Free Tiers

TDMQ for Pulsar offers certain free tiers to each root account for pay-as-you-go billable items in each region:

| Billable Item           | Free Tier | Accumulation Method       |
| :--------------- | :------- | :------------- |
| API call          | 10 million | Accumulated monthly by region |
| Message storage         | 1 GB      | Accumulated monthly by region |
| Partition topic | 2000    | Accumulated monthly by region |

The free tiers will be used first to deduct the cumulative usage of all clusters in each region under each root account, and they are shared between different clusters in the same region.
