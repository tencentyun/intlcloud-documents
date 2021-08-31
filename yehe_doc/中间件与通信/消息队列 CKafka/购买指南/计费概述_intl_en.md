>?Existing pay-as-you-go instances will be charged from 0:00:00 July 15, 2021.

This document describes the product specifications, billable items, billing modes, and instance prices of CKafka.

## Product Specifications

CKafka instances are divided into Standard Edition and Pro Edition according to their specifications. The comparison of the two editions are as follows:

| Item | Pro Edition | Standard Edition |
| :------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Version | Compatible with open-source versions 0.10, 1.1, and 2.4, which can be freely selected upon purchase | Compatible with open-source versions 0.10 and 1.1. v1.1 is installed by default. Customized versions are not supported |
| Instance type | Dedicated instance (each instance has a separate cluster of independent virtual nodes) | Shared physical node resources |
| Stability SLA | 99.995% | 99.95% |
| Instance specification | There are no fixed models, and the specifications can be customized according to the actual business scenario | There are 8 fixed instance types, including small, standard, and advanced |
| Topic/Partition specification | The topic/partition capacity is much larger than that on the Standard Edition under the same bandwidth. Additional partition packages can be purchased within a certain range to increase the upper limit | Each model has a fixed upper limit |
| Scalability | Its scalability is high, and the upper limits of bandwidth, topics/partitions, and disks can be increased separately | Its scalability is low, and its disk can be expanded separately |
| Performance tuning | The performance can be customized according to the business scenario with fewer parameter restrictions | The numbers of topics and partitions are limited according to the different instance specifications |
| Automatic disk cleanup | Available. Expired data is cleared regularly | Unavailable. You need to <a href="https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory">submit a ticket</a> for assistance when the disk is full |
| Broker repair and upgrade | Targeted upgrades are available, and the upgrade process is fast and almost imperceptible with high stability | Subject to shared cluster resources, upgrades for problem fixes take a long time |
| High availability | Custom multi-AZ deployment in the same region is supported to improve the disaster recovery capabilities | Multi-AZ deployment in the same region is not supported. It relies on backend migration and requires you to <a href="https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory">submit a ticket</a> to apply, which generally takes 10 business days for processing |
| Advanced features | Timed rebalance (you can customize the rebalance execution time during upgrade to avoid business peak hours. For more information, please see [Upgrading Instances](https://intl.cloud.tencent.com/document/product/597/40650)). Advanced monitoring (this includes network stability analysis and request delay analysis. For more information, please see [Querying Advanced Monitoring Information](https://intl.cloud.tencent.com/document/product/597/40038)). Dynamic message retention policy adjustments based on disk utilization (for more information, please see [Adding Dynamic Message Retention Policies](https://intl.cloud.tencent.com/document/product/597/40211)) | None |
| Technical support | Parameter optimization consulting services are supported, helping you customize parameter configurations for certain special business scenarios. You can <a href="https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory">submit a ticket</a> to apply for parameter optimization consulting services | Basic troubleshooting and problem fixing |

> ?
>
> The automatic disk cleanup feature is enabled for the **Pro Edition** by default. When the instance disk is full, the oldest data will be automatically cleared to ensure that the instance is available.

## Billable Items

The billable items are as follows:

| Item | Pro Edition | Standard Edition | Description |
| :-------- | :----- | :----- | :----------------------------------------------------------- |
| Peak bandwidth | ✔ | ✔ | Throughput refers to the outbound and inbound bandwidth peak. For example, a throughput of 40 MB indicates that the outbound and inbound peak bandwidth is 40 MB. The replicas of an instance share the throughput equally. For example, for a throughput of 40 MB and three replicas, you should purchase a bandwidth with a throughput of 120 MB/s. |
| Disk capacity | ✔ | ✔ | <li>The disk capacity varies by instance specification. </li><li>CKafka Standard Edition supports SSD cloud disks. CKafka Pro Edition supports SSD and premium cloud disks.</li> |
| Partition | ✔ | - | <li>The number of partitions varies by instance specification, and additional partitions can be purchased separately for the Pro Edition. </li><li>Topics are free of charge for the Pro Edition, and the maximum number of available topics is equal to the number of partitions/the number of replicas. </li><li>The number of partitions cannot be reduced. </li><li>The instance-level partition limit applies to the number of replicas. For example, if an instance has one topic with two replicas and each with four partitions, and two topics with three replicas and each with three partitions, then the total number of partitions in this instance will be (1 * 2 * 4) + (2 * 3 * 3) = 26.</li> |

## Billing Modes

| Mode | Pro Edition | Standard Edition | Description |
| :------- | :----- | :----- | :----------------------------------------------------------- |
| Monthly subscription | ✔ | - | The total fees of a purchased Pro Edition instance are (basic package price + partition package price * number of additional partitions / 100 + disk capacity price * disk capacity / 100) * number of months. For detailed prices, please see [Pro Edition pricing](). |
| Pay-as-You-Go | ✔ | ✔ | <li>The total fees of a purchased Pro Edition instance are (basic package price + partition package price * number of additional partitions / 100 + disk capacity price * disk capacity / 100) * number of hours. For detailed prices, please see [Pro Edition pricing](). </li><li>The total fees of a purchased Standard Edition instance are (basic package price + disk capacity price * disk capacity / 100) * number of hours. For detailed prices, please see [Standard Edition pricing]().</li> |

> ?
>
> In the pay-as-you-go billing mode, you can select configuration items such as traffic specification and disk capacity as needed, which are billed by the hour (a usage duration that is shorter than one hour will be calculated as one hour). Bills are generated once a month. After you purchase a pay-as-you-go instance, the system will allocate corresponding instance resources. Therefore, in this billing mode, the instance is billed by the instance price multiplied by the service time, regardless of whether the instance is used after purchase.
>
> Currently, capacity reduction in advance is not supported. You can [submit a ticket](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory) to apply for capacity reduction. The backend will perform the capacity reduction operation for you before your next billing cycle starts. After, fees will be charged based on the reduced specifications.

## Monthly Subscription

### Pro Edition pricing

CKafka Pro Edition provides more flexible specification selection modes and more stable upgrade capabilities. You can purchase and scale instances according to your specific business needs.

**Basic package**

After you select the peak bandwidth value for an instance, it will be automatically matched with a corresponding basic package. The basic package in each tier includes a certain number of partitions, and topics are not billed separately. The number of available topics in the package is equal to the number of partitions/the number of replicas.

The tiers of peak bandwidth (x) are as follows:

| Peak Bandwidth Tier (MB/s) | Number of Partitions in the Package |
| :------------------- | :---------------------- |
| 40 ≤ x < 120          | 2,000                    |
| 120 ≤ x < 320         | 2,000                    |
| 320 ≤ x < 920         | 2,000                    |
| 920 ≤ x < 1,200        | 2,800                    |
| x = 1,200             | 3,200                    |
| x = 1,600             | 8,000                    |
| x = 2,000             | 10,000                   |
| x = 2,400             | 12,000                   |
| x = 2,800             | 14,000                   |
| x = 3,200             | 16,000                   |

> ?
>
> - The fees for the partitions in a package are already included in the package fees, so they will not incur additional fees.
> - If you need CKafka instances with higher specifications, please contact your Tencent Cloud rep or [submit a ticket](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory) for assistance.

The price of the basic peak bandwidth package varies by tier, as detailed below:

| Tier | Peak Bandwidth Range (MB/s) | Price (Monthly Subscription) |
| :-------- | :------------------- | :------------------------------------------ |
| Basic I   | 40–100               | Starting at 360 USD/month and 53 USD/month for each extra 20 MB/s    |
| Basic II   | 120–300               | Starting at 630 USD/month and 51 USD/month for each extra 20 MB/s    |
| Basic III  | 320–600               | Starting at 1,200 USD/month and 49 USD/month for each extra 20 MB/s    |
| Basic IV  | 620–900               | Starting at 2,340 USD/month and 43 USD/month for each extra 20 MB/s    |
| Basic V  | 920–1,200               | Starting at 3,090 USD/month and 34 USD/month for each extra 20 MB/s    |
| Premium  | 1,600–10,000               | Starting at 4,150 USD/month and 856 USD/month for each extra 400 MB/s    |

For example, a 180 MB/s instance falls into the Basic II tier with 60 MB/s added to 120 MB/s, so the price of the package is 630 + 51 * (60 / 20) = 783 (USD/month)

**Partition package pricing**

After you select the peak bandwidth value, if the number of partitions in the corresponding basic package cannot meet your needs, you can purchase additional partition packages separately. The number of partitions can be increased in increments of 100, as priced below:

| Tier     | Number of Partitions | Partition Package Price (Monthly Subscription) |
| :------- | :-------------------- | :-------------------------- |
| Any tier | 100                   | 35 USD/month                   |

**Disk expansion pricing**

To purchase a CKafka Pro Edition instance, you need to purchase a disk of a certain minimum size. The disk capacity can be expanded in increments of 100 GB, as priced below:

| Tier     | Disk Type       | Disk Capacity (GB) | Disk Price (Monthly Subscription) |
| :------- | :----------- | :----------------- | :------------------- |
| Any tier | SSD cloud disk   | 100                | 16 USD/month            |
| Any tier | Premium cloud disk | 100                | 6 USD/month             |

## Pay-as-You-Go

### Standard Edition pricing

CKafka Standard Edition is available in 8 instance types such as small and standard based on the **peak throughput** and the **disk capacity**.

**Instance pricing**

| Instance Type | Peak Throughput (MB/s) | Disk Capacity (GB) | Number of Instance-Level Topics | Number of Instance-Level Partitions | Price (USD/Hour) |
| :-------- | :----------------- | :------------- | :---------------- | :-------------------- | :---------------- |
| Small    | 40                 | 300            | 25                | 60                    | 0.09              |
| Standard    | 100                | 1,000           | 40                | 100                   | 0.25              |
| Advanced    | 150                | 2,500           | 50                | 150                   | 0.57              |
| Large    | 180                | 4,000           | 150               | 300                   | 0.82              |
| Xlarge L1 | 300                | 6,000           | 250               | 500                   | 1.06              |
| Xlarge L2 | 400                | 6,000           | 250               | 500                   | 1.34              |
| Xlarge L3 | 600                | 6,000           | 350               | 600                   | 1.80              |
| Xlarge L4 | 900                | 9,000           | 450               | 700                   | 2.68              |

**Disk expansion pricing**

| Disk Type | Disk Capacity (GB) | Price (USD/Hour) |
| :--------- | :------------- | :---------------- |
| Premium cloud disk | 100            | 0.01              |

> ? If you need CKafka instances with higher specifications, please contact your Tencent Cloud rep or [submit a ticket](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory) for assistance.

### Pro Edition pricing

CKafka Pro Edition provides more flexible specification selection modes and more stable upgrade capabilities. You can purchase and scale instances according to your specific business needs.

**Basic package**

After you select the peak bandwidth value for an instance, it will be automatically matched with a corresponding basic package. The basic package in each tier includes a certain number of partitions, and topics are not billed separately. The number of available topics in the package is equal to the number of partitions/the number of replicas.

The tiers of peak bandwidth (x) are as follows:

| Peak Bandwidth Tier (MB/s) | Number of Partitions in the Package |
| :------------------- | :---------------------- |
| 40 ≤ x < 120          | 2,000                    |
| 120 ≤ x < 320         | 2,000                    |
| 320 ≤ x < 920         | 2,000                    |
| 920 ≤ x < 1,200        | 2,800                    |
| x = 1,200             | 3,200                    |
| x = 1,600             | 8,000                    |
| x = 2,000             | 10,000                   |
| x = 2,400             | 12,000                   |
| x = 2,800             | 14,000                   |
| x = 3,200             | 16,000                   |

> ?
>
> - The fees for the partitions in a package are already included in the package fees, so they will not incur additional fees.
> - If you need CKafka instances with higher specifications, please contact your Tencent Cloud rep or [submit a ticket](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory) for assistance.

The price of the basic peak bandwidth package varies by tier, as detailed below:

| Tier | Peak Bandwidth Range (MB/s) | Price (Pay-as-You-Go) |
| :-------- | :------------------- | :----------------------------------------------- |
| Basic I   | 40–100               | Starting at 0.55 USD/hour and 0.09 USD/hour for each extra 20 MB/s    |
| Basic II   | 120–300               | Starting at 0.96 USD/hour and 0.08 USD/hour for each extra 20 MB/s    |
| Basic III   | 320–600               | Starting at 1.83 USD/hour and 0.07 USD/hour for each extra 20 MB/s    |
| Basic IV   | 620–900               | Starting at 3.57 USD/hour and 0.06 USD/hour for each extra 20 MB/s    |
| Basic V   | 920–1,200               | Starting at 4.72 USD/hour and 0.05 USD/hour for each extra 20 MB/s    |
| Premium  | 1,600–10,000               | Starting at 6.34 USD/hour and 1.31 USD/hour for each extra 400 MB/s    |

For example, a 180 MB/s instance falls into the Basic II tier with 60 MB/s added to 120 MB/s, so the price of the package is 0.96 + 0.08 * (60 / 20) = 1.2 (USD/hour)

**Partition package pricing**

After you select the peak bandwidth value, if the number of partitions in the corresponding basic package cannot meet your needs, you can purchase additional partition packages separately. The number of partitions can be increased in increments of 100, as priced below:

| Tier     | Number of Partitions | Partition Package Price (Pay-as-You-Go) |
| :------- | :-------------------- | :-------------------------- |
| Any tier | 100                   | 0.05 USD/hour                   |

**Disk expansion pricing**

To purchase a CKafka Pro Edition instance, you need to purchase a disk of a certain minimum size. The disk capacity can be expanded in increments of 100 GB, as priced below:

| Tier     | Disk Type       | Disk Capacity (GB) | Disk Price (Pay-as-You-Go) |
| :------- | :----------- | :----------------- | :------------------- |
| Any tier | SSD cloud disk   | 100                | 0.03 USD/hour            |
| Any tier | Premium cloud disk | 100                | 0.01 USD/hour             |

