## Overview

This document describes how to query the alarm history in cloud native monitoring.

## Prerequisites

Before querying alarm history, you need to perform the following operations:
- You've created a TPS instance as instructed in [Creating TPS Instance](https://intl.cloud.tencent.com/document/product/457/38824).
- The cluster to be monitored has been associated with the corresponding instance. For more information, see [Associating with cluster](https://intl.cloud.tencent.com/document/product/457/38825).
- The information that needs to be collected has been added to the [data collection configuration](https://intl.cloud.tencent.com/document/product/457/38826) of the cluster.
- Alarm policies are configured. Refer to [Configuring Alarm Policy](https://intl.cloud.tencent.com/document/product/457/38828).

## Directions


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** on the left sidebar.
2. On the instance list page, select an instance name that needs to query alarm history to go to its details page.
3. On **Alarm history** page, select an time range to query the alarm history as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/1c00ed84dd12db38b5d7b23b8a0c9d72.png)
