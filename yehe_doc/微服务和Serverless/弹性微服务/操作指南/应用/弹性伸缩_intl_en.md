## Overview

This document describes how to modify the number of service instances in the TEM console.

## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. In the left sidebar, click **Application Management** to go to the application list page and select a deployment region for your application.
3. Click the ID of the target application to go to the application details page.
4. Click **Edit and Update** in the **Auto-Scaling** module and configure the instance count change policy.
   - Scheduled Policy: specify the instance trigger time and the number of instances to trigger. You can configure multiple trigger conditions but only one of them can take effect.
     ![](https://main.qcloudimg.com/raw/460d5046bf2599d85bb2034fb7c3e915.png)
   - Metric-scaling Policy: enter an expected metric value. The system will calculate the scaling ratio according to current and expected metric values.
   ![](https://main.qcloudimg.com/raw/c494f5484323c6dce63667f6be2316d6.png)
5. Click **Submit** to modify the number of instances.
