This document describes the billable items, billing modes, and instance prices of CKafka Pro Edition.

## Billable Items

The billable items are as follows:


| Item      | Description                                                         |
| --------- | ------------------------------------------------------------ |
| Peak bandwidth | A throughput of 40 MB indicates that the outbound and inbound peak bandwidth is 40 MB. The replicas of an instance share the throughput equally. For example, for a throughput of 40 MB and three replicas, you should purchase a peak bandwidth of 120 MB/s. |
| Disk capacity | <li>The disk capacity varies by instance specification. </li><li>CKafka Pro Edition currently supports SSD and HDD cloud disks and will support premium cloud disks starting April 2021.</li> |
| Partition | <li>The number of partitions varies by instance specification, and additional partitions can be purchased separately for the Pro Edition. </li><li>Topics are free of charge for the Pro Edition, and the maximum number of available topics is equal to the number of partitions/the number of replicas.</li><li>The number of partitions cannot be reduced. </li><li>The instance-level partition limit applies to the number of replicas. For example, if an instance has one topic with 2 replicas and each with 4 partitions, and two topics with 3 replicas and each with 3 partitions, the total number of partitions in this instance is (1 * 2 * 4) + (2 * 3 * 3) = 26.</li> |

## Billing Modes

The CKafka service can be billed as an instance by using a **prepaid monthly subscription** plan.

When purchasing Pro Edition instances, you need to estimate the peak bandwidth, number of partitions, and disk capacity of your business. The total fees of the purchased instances are (basic package price + partition package price * number of additional partitions / 100 + disk capacity price * disk capacity / 100) * number of months.

> ?Currently, the monthly subscription billing mode does not support capacity reduction in advance. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=消息服务 CKafKa&step=1) to apply for capacity reduction. The backend will perform the reduction operation for you before your next billing cycle starts. Then, fees will be charged based on the reduced specification.

## Pro Edition Pricing

CKafka Pro Edition provides more flexible specification selection modes and more stable upgrade/downgrade capabilities. You can purchase and scale instances according to your specific business needs.

**Basic package**

After you select the peak bandwidth value for an instance, it will be automatically matched with a corresponding basic package. The basic package in each tier includes a certain number of topics and partitions and disk capacity. The maximum number of available topics is equal to the number of partitions/the number of replicas.

The tiers of peak bandwidth (x) are as follows:

| Peak Bandwidth Tier (MB/s) | Maximum Number of Topics | Minimum Number of Partitions | Maximum Number of Partitions | Minimum Disk Capacity (GB) | Maximum Disk Capacity (GB) |
| -------------------- | ------------------- | ----------------------- | ----------------------- | ------------------ | ------------------ |
| x = 40               | 1000                | 2000                    | 2400                    | 100                | 5000               |
| x = 120              | 1000                | 2000                    | 2800                    | 200                | 10000              |
| x = 320              | 1000                | 2000                    | 3200                    | 500                | 25000              |
| x = 920              | 1400                | 2800                    | 3600                    | 1000               | 50000              |
| x = 1200             | 1600                | 3200                    | 6400                    | 1000               | 50000              |
| x = 1600             | 4000                | 8000                    | 16000                   | 4000               | 100000             |
| x = 2000             | 5000                | 10000                   | 20000                   | 4000               | 100000             |
| x = 2400             | 6000                | 12000                   | 24000                   | 4000               | 100000             |
| x = 2800             | 7000                | 14000                   | 28000                   | 4000               | 100000             |
| x = 3200             | 8000                | 16000                   | 32000                   | 4000               | 100000             |

  >?
  >
  >- The fees of topics and partitions in a package are already included in the package fees, so no additional fees will be incurred for them.
  >
  >
  > - If you need CKafka instances with higher specifications, please contact your Tencent Cloud rep or [submit a ticket](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory) for assistance.

The price of basic peak bandwidth package varies by tier as detailed below:

| Tier | Peak Bandwidth Range (MB/s) | Price (Monthly Subscription) |
| --------- | -------------------- | ------------------------------------------- |
| Basic I   | 40–100               | Starting at 310 USD/month and 47 USD/month for each extra 20 MB/s    |
| Basic II   | 120–300               | Starting at 522 USD/month and 45 USD/month for each extra 20 MB/s    |
| Basic III  | 320–600               | Starting at 948 USD/month and 44 USD/month for each extra 20 MB/s    |
| Basic IV  | 620–900               | Starting at 1,806 USD/month and 39 USD/month for each extra 20 MB/s    |
| Basic V  | 920–1,200               | Starting at 2,370 USD/month and 30 USD/month for each extra 20 MB/s    |
| Premium  | 1,600–3,200               | Starting at 3,175 USD/month and 780 USD/month for each extra 400 MB/s    |

For example, a 180 MB/s instance falls into the Basic II tier with 60 MB/s added to 120 MB/s, so the price of the package is 522 + 45 * (60 / 20) = 657 (USD/month)

**Partition package pricing**

After you select the peak bandwidth value, if the number of partitions in the corresponding basic package cannot meet your needs, you can purchase partition packages separately. The number of partitions can be increased in increments of 100 as priced below:

| Tier     | Number of Partitions | Partition Package Price (Monthly Subscription) |
| -------- | --------------------- | --------------------------- |
| Any tier | 100                   | 16 USD/month                   |

**Disk expansion pricing**

To purchase a CKafka Pro Edition instance, you need to purchase a disk of a certain minimum size. The disk capacity can be expanded in increments of 100 GB as priced below:

| Tier     | Disk Type       | Disk Capacity (GB) | Disk Price (Monthly Subscription) |
| -------- | -------------- | ------------------ | -------------------- |
| Any tier | SSD cloud disk | 100                | 16 USD/month            |
| Any tier | HDD cloud disk     | 100                | 8 USD/month             |

