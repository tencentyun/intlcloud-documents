
>! This feature has been in beta test in Beijing, Shanghai, and Guangzhou, Nanjing, and Chongqing regions free of charge since August 15, 2022.
>

## Overview

Scheduled SQL analysis can be simply understood as crontab SQL. You can configure a scheduling policy, and the system will execute SQL queries on the source log topic regularly based on the policy and save query results to the specified target log topic. 

![](https://qcloudimg.tencent-cloud.cn/raw/742252b4378a0ba18267ada7c251af51.jpg)

## Prerequisites

- The CLS service has been activated, and key-value index has been enabled.
- Make sure that the current account has the permission to configure scheduled SQL analysis. For more information, see [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).


## Use cases

- For a query with a high data volume, you can use the scheduled SQL analysis feature to break it down into multiple queries with a low data volume each to avoid query failure and timeout.
For example, if the original SQL query involves data of one day, you can split it into 24 queries for execution once every hour.
- Generate daily and weekly reports.
- Aggregate logs, which can greatly reduce index and log storage fees.
For example, aggregating 1-minute historical logs into 1-hour logs can effectively save the storage costs.
- Filter and save data to a new log topic. Scheduled SQL analysis can meet the needs in some simple filtering scenarios through WHERE and WHEN statements. However, as a SQL query can only return up to 10,000 results, data integrity cannot be guaranteed, and the query is not conducted by real-time stream computing. Therefore, this feature is only applicable to use cases with a small amount of data that don't require real-time computing. For similar use cases, we recommend you use this feature.

## Use limits

- Up to 10,000 results can be returned per query, and the excess will be truncated.

- Cross-region query is not supported. The source and target log topics must be in the same region.
