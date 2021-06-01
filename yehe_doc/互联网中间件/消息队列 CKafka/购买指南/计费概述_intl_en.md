This document describes the billable items, billing modes, and instance prices of CKafka Pro Edition.

## Billable Items

The billable items are as follows:


| Item      | Description                                                         |
| --------- | ------------------------------------------------------------ |
| Peak bandwidth | A throughput of 40 MB/s indicates that the outbound and inbound peak bandwidth is 40 MB/s. Please keep in mind that the replicas of an instance share the throughput equally. For example, for a throughput of 40 MB/s and three replicas, you should purchase a peak bandwidth of 120 MB/s. |
| Disk capacity | <li>The disk capacity varies by instance specification. </li><li>CKafka Pro Edition currently supports SSD and Premium Cloud Storage.</li> | 
| Partition | <li>The number of partitions varies by instance specification, and additional partitions can be purchased separately for the Pro Edition. </li><li>Topics are free of charge for the Pro Edition, and the maximum number of available topics is equal to the number of partitions/the number of replicas. </li><li>The number of partitions cannot be reduced. </li><li>The instance-level partition limit applies to the number of replicas. For example, if an instance has 1 topic with 2 replicas and each with 4 partitions, and 2 topics with 3 replicas and each with 3 partitions, then the total number of partitions in this instance is (1 x 2 x 4) + (2 x 3 x 3) = 26.</li> |

## Billing Modes

The CKafka service can be billed as an instance using a **prepaid monthly subscription** plan.

When purchasing Pro Edition instances, you need to estimate the peak bandwidth, the number of partitions, and the disk capacity of your business. The total fees of the purchased instances are (basic package price + partition package price x number of additional partitions/100 + disk capacity price x disk capacity/100) x number of months.

> ?Currently, the monthly subscription billing mode does not support capacity reduction in advance. You can [submit a ticket](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory) to apply for capacity reduction. The backend will perform the reduction operation for you before your next billing cycle starts. Then, fees will be charged based on the reduced specification.

## Pro Edition Pricing

CKafka Pro Edition provides more flexible specification selection modes and more stable upgrade capabilities. You can purchase instances or expand your instances' capacity according to your business needs.

**Basic package**

After you select the peak bandwidth for an instance, it will be automatically matched with a corresponding basic package. The basic package in each tier includes a certain number of partitions. Topics are free of charge, and the number of available topics is equal to the number of partitions/the number of replicas.

The peak bandwidth tiers (x) are as follows:

| Peak Bandwidth Tier (MB/s) | Number of Partitions |
| -------------------- | ----------------------- |
| 40 ≤ x < 120          | 2000                    |
| 120 ≤ x < 320         | 2000                    |
| 320 ≤ x < 920         | 2000                    |
| 920 ≤ x < 1200        | 2800                    |
| x = 1200             | 3200                    |
| x = 1600             | 8000                    |
| x = 2000             | 10000                   |
| x = 2400             | 12000                   |
| x = 2800             | 14000                   |
| x = 3200             | 16000                   |

  >?
  >
  >- The fees of partitions in a package are already included in the package fees, so no additional fees will be incurred for them.
  >
  >- If you need CKafka instances with higher specifications, please contact your Tencent Cloud sales rep or [submit a ticket](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory) for assistance.

The price of the basic peak bandwidth package varies by tier, as detailed below:

| Tier | Peak Bandwidth Range (MB/s) | Price (Monthly Subscription) |
| --------- | -------------------- | ------------------------------------------- |
| Basic I   | 40–100               | Starting at 360 USD/month and 53 USD/month for each extra 20 MB/s    |
| Basic II   | 120–300               | Starting at 630 USD/month and 51 USD/month for each extra 20 MB/s    |
| Basic III  | 320–600               | Starting at 1,200 USD/month and 49 USD/month for each extra 20 MB/s    |
| Basic IV  | 620–900               | Starting at 2,340 USD/month and 43 USD/month for each extra 20 MB/s    |
| Basic V  | 920–1,200               | Starting at 3,090 USD/month and 34 USD/month for each extra 20 MB/s    |
| Premium  | 1,600–10,000               | Starting at 4,150 USD/month and 856 USD/month for each extra 400 MB/s    |

For example, a 180 MB/s instance falls into the Basic II tier with 60 MB/s added to 120 MB/s, so the price of the package is 630 + 51 x (60/20) = 783 (USD/month)

**Partition package pricing**

After you select the peak bandwidth, if the number of partitions in the corresponding basic package cannot meet your needs, you can purchase additional partition packages separately. The number of partitions can be increased in increments of 100, as detailed below:

| Tier     | Number of Partitions | Partition Package Price (Monthly Subscription) |
| -------- | --------------------- | --------------------------- |
| Any tier | 100                   | 35 USD/month                   |

**Disk capacity expansion pricing**

To purchase a CKafka Pro Edition instance, you need to purchase a disk of a certain minimum size. The disk capacity can be expanded in increments of 100 GB, as detailed below:

| Tier     | Disk Type       | Disk Capacity (GB) | Disk Price (Monthly Subscription) |
| -------- | -------------- | ------------------ | -------------------- |
| Any tier | SSD | 100                | 16 USD/month            |
| Any tier | Premium Cloud Storage | 100                | 6 USD/month             |

