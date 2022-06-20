This document describes the pricing details and free tiers of each billable item in TDMQ for CMQ.

## Pay-as-You-Go

[](id:API)
### API call price

TDMQ for CMQ adopts linear pricing for API calls. **API call fees = (number of API calls for message sending + number of API calls for message consumption + number of API calls for message acknowledgment) * API call unit price**.

The unit price of API call (USD/10000 calls/hour) is as shown below:

<table><tr>
<th rowspan="2"><nobr>Region</nobr></th>
</tr><tr>
<th>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu</th>
<th>Hong Kong (China), Singapore, Seoul, Tokyo, Silicon Valley, Toronto, Frankfurt, Virginia, Moscow</th>
<th>Shenzhen Finance, Beijing Finance, Shanghai Finance</th>
</tr><tr>
<td>Unit price (USD/10000 calls/hour)</td>
<td>0.002512</td>
<td>0.003265</td>
<td>0.004019</td>
</tr>
</table>


The maximum message body size is 1 MB, and the number of API calls is calculated at different rates based on the message size:

| Message Size | Rate |
| :--------------- | :--- |
| N ≤ 2 KB          | 1    |
| 2 KB < N ≤ 4 KB    | 2    |
| 4 KB < N ≤ 16 KB   | 4    |
| 16 KB < N ≤ 100 KB | 16   |
| 100 KB < N ≤ 1 MB  | 64   |

For example, one 10 KB message (publishing or subscribing) request will be charged as **four** API calls.

>? If batch sending/consumption is used, fees will be calculated separately based on the number of messages sent/consumed in batches. For example, if ten messages are batch sent and each is 2 KB in size, then they will be calculated as 10 * 2 = 20 API calls.


[](id:msg)
### Message storage price

>? Billing for the message rewind feature will start on July 11, 2022.

TDMQ for CMQ adopts linear billing for the maximum message storage capacity you set after enabling the [message rewind](https://intl.cloud.tencent.com/document/product/1111/42997) feature. **Message storage fees = storage capacity set for message rewind * message storage unit price**.

The unit price of message storage (USD/GB/hour) is as shown below:

| Region | Guangzhou, Shanghai, Nanjing, Beijing, Chengdu | Hong Kong (China), Singapore, Seoul, Tokyo, Silicon Valley, Toronto, Frankfurt, Virginia, Moscow | Shenzhen Finance, Beijing Finance, Shanghai Finance |
| :------------------- | :--------------------------- | :----------------------------------------------------------- | :--------------------------- |
| Unit price (USD/GB/hour) | 0.0003                       | 0.0003                                         | 0.0006             |

The number of message replicas is 3 by default and cannot be adjusted currently.

For example, messages of queue A created in Guangzhou region are very important to the business, so message rewind is enabled, and a message rewind space of 10 GB is set. Then, the fees incurred on the next day will be 0.0003 * 3 * 10 * 24 = 0.216 USD.

>?
>- No message storage fees will be incurred if you don't enable message rewind for the queue.
>- No matter how much storage capacity is actually used, fees will be always charged based on the set maximum storage capacity.


[](id:resource)
### Queue/Topic resource usage price

TDMQ for CMQ adopts linear billing for queue/topic resource usage beyond the free tier. **Queue/topic resource usage fees = (number of queues + number of topics) * resource usage unit price**.

The unit price of queue/topic resource usage (USD/piece/day) is as shown below:

| Region | Guangzhou, Shanghai, Nanjing, Beijing, Chengdu | Hong Kong (China), Singapore, Seoul, Tokyo, Silicon Valley, Toronto, Frankfurt, Virginia, Moscow | Shenzhen Finance, Beijing Finance, Shanghai Finance |
| :----------------- | :--------------------------- | :----------------------------------------------------------- | :--------------------------- |
| Unit price (USD/piece/day) | 0.2512                       | 0.3265                                                       | 0.4018                       |

>!The queue/topic resource usage fees in TDMQ for CMQ are charged by day; that is, a queue or topic resource created at any time on a natural day will incur a full day's fees on the next natural day even if its actual usage time is less than 24 hours.


## Free Tiers

TDMQ for CMQ offers certain free tiers to each root account for pay-as-you-go billable items in each region:

| Billable Item           | Free Tier | Accumulation Method       |
| :--------------------------- | :------- | :------------- |
| API call          | 10 million | Accumulated monthly by region |
| Message storage         | 10 GB      | Accumulated monthly by region |
| Queue resource usage (during the promotional period) | 50 queues | By region |
| Topic resource usage (during the promotional period) | 50 topics | By region |

The free tiers will be used first to deduct the cumulative usage of all clusters in each region under each root account, and they are shared between different queues/topics in the same region.

>? After the promotional period ends, the free tiers for queue resource usage and topic resource usage will be reset to 5 each (by region).
