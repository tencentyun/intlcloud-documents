## Overview

Tencent Cloud provides the Cloud Monitor feature for all users by default. This feature helps you monitor and collect data from the Tencent Cloud products you are using. This document describes how to obtain the monitoring data.

## Directions
<dx-tabs>
::: CVM console
<dx-alert infotype="explain" title="">
CVM console provides a monitoring page, on which you can view the monitoring data of CPU, memory, network bandwidth and disks in the specified period.
</dx-alert>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. In the instance management page, click the ID/Name of the CVM to enter its details page and view the monitoring data.
3. Click the **Monitoring** tab to get the instance monitoring data.
:::
::: Cloud Monitor console
<dx-alert infotype="explain" title="">
Cloud Monitor console provides the monitoring data of all Tencent Cloud products. On the console, you can view the monitoring data of CPU, memory, network bandwidth and disks in the specified period.
</dx-alert>
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview).
2. Select **Cloud Product Monitoring** > **Cloud Virtual Machine** on the left sidebar.
3. Click the ID/Name of the CVM instance to enter its details page and view the monitoring data.
:::
:::  Cloud Monitor dashboard
Specify required CVM metrics and create a dashboard, on which you can view monitoring data in intuitive charts, helping you analyze metrics through trends and exceptional values.
1. Log in to the Cloud Monitor console and select **Dashboard** > [Default Dashboard](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=8).
2. Create a dashboard as instructed in [Create Dashboard](https://intl.cloud.tencent.com/document/product/248/35282) and get the monitoring data.
:::
::: API
You can use the `GetMonitorData` API to get the monitoring data for all Tencent Cloud products. For more information, see [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881).
:::
</dx-tabs>
