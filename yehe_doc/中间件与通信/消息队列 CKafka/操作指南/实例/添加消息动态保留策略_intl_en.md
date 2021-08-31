## Overview

After you set the message retention time, expired messages will be deleted. In case of message surges, normal production and consumption cannot be performed after the disk is full. If you set a dynamic retention policy, when the disk utilization reaches a certain percentage, a certain proportion of data will automatically expire to avoid the above issue.

This document describes how to configure a dynamic message retention policy in the CKafka console.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance basic information page, enable **dynamic retention policy**.
   The default dynamic policy reduces the message retention time by 10% when the disk load reaches 90%.

4. Click **View** to view the message retention time of each topic.

5. Click **Configuration** in the top-right corner of the dynamic retention policy module to set the dynamic policy and minimum retention time.

   - Dynamic Policy: after message retention time adjustment is triggered, the broker will delete the oldest historical data according to the new retention time. This feature has a certain delay.
   - Minimum Retention Time: it can be 1 minute to 30 hours. If the dynamic retention time is lower than this parameter, no dynamic adjustment will be triggered.

