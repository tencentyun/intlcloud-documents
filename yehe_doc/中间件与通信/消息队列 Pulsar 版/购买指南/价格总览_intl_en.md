# Pricing Overview
This document describes the pricing details and free tiers of TDMQ for Pulsar's each billable item.
## Pay-as-You-Go
### API call price
TDMQ for Pulsar adopts tiered pricing for API calls. **API call fees = (number of API calls for message sending + number of API calls for message consumption) * API call unit price**.

The unit price of API call (USD/million calls/hour) is as shown below:

| Billing Tier | Number of Calls (Million/Month) | Guangzhou, Shanghai, Nanjing, Beijing, and Chengdu | Hong Kong (China), Singapore, Seoul, Silicon Valley, Toronto, and Frankfurt | Shenzhen Finance and Beijing Finance |
|:----------|:----------|:----------|:----------|:----------|
| Tier 1 | 0–1,000 | 0.25 | 0.33 | 0.40 |
| Tier 2 | 1,000–5,000 | 0.23 | 0.29 | 0.36 |
| Tier 3 | 5,000–10,000 | 0.19 | 0.24 | 0.30 |
| Tier 4 | 10,000–50,000 | 0.16 | 0.21 | 0.26 |
| Tier 5 | >50,000 | 0.15 | 0.20 | 0.24 |

### Message storage price
TDMQ for Pulsar adopts linear billing for message storage. **Message storage fees = message storage size * message storage unit price**.

The unit price of message storage (USD/GB/hour) is as shown below:

| Region | Guangzhou, Shanghai, Nanjing, Beijing, and Chengdu | Hong Kong (China), Singapore, Seoul, Silicon Valley, Toronto, and Frankfurt | Shenzhen Finance and Beijing Finance |
|:----------|:----------|:----------|:----------|
| Unit price (USD/GB/hour) | 0.0003 | 0.0003 | 0.0006 |

### Partition topic resource usage price
TDMQ for Pulsar adopts linear billing for partition topic resource usage. **Partition topic resource usage fees = number of partition topics * partition topic resource usage unit price**.

The number of partition topics in TDMQ for Pulsar refers to the sum of all partitions of all topics; that is, if there are two 3-partition topics, the number of partition topics is 2 * 3 = 6.

The unit price of partition topic resource usage (USD/piece/day) is as shown below:

| Region | Guangzhou, Shanghai, Nanjing, Beijing, and Chengdu | Hong Kong (China), Singapore, Seoul, Silicon Valley, Toronto, and Frankfurt | Shenzhen Finance and Beijing Finance |
|:----------|:----------|:----------|:----------|
| Unit price (USD/piece/day) | 0.03 | 0.03 | 0.04 |

## Free tiers
TDMQ for Pulsar offers certain free tiers to each root account for pay-as-you-go billable items:
- 10 million free API calls per month.
- 1 GB of free message storage per month.
- 2,000 free partition topics per month.

The free tiers will be used first to deduct the cumulative usage of all clusters under each root account, and they are shared between different clusters.

