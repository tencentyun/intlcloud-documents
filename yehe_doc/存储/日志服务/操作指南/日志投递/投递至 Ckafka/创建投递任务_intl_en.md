## Overview

CLS uses CKafka instances to consume log topic data. This section describes how to enable CKafka consumption for a log topic.

## Prerequisites

Tencent Cloud CKafka has been activated, and a CKafka consumption instance and a message queue topic have been created in the same region as the log topic.

>? For details about how to create a CKafka instance, see [Creating Instances and Topics](https://intl.cloud.tencent.com/document/product/597/40039).
>

## Supported Regions

Supported regions:

| Region | Zone |
|---------|---------|
| Guangzhou | 3, 4 |
| Beijing | 3, 4, 5 |
| Shanghai | 2, 3, 4 |
| Bangkok | 1 |

>! Shipping to CKafka is supported only in above regions.
>

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** in the left sidebar.
3. Click the log topic name/ID for which CKafka consumption needs to be configured to go to its details page.
4. Click the **Ship to CKafka** tab.
5. Click **Edit** on the right. Toggle the switch to enable **Ship to CKafka**, and select a CKafka instance for consumption and a corresponding message queue topic.

6. Click **Save** to enable CKafka consumption. If the status of CKafka consumption is displayed as "Enabled", it means that it has been enabled successfully.


>! To cleanse the log data before shipping to CKafka, please see [CLS Dump to CKafka](https://intl.cloud.tencent.com/document/product/614/38885).
>

