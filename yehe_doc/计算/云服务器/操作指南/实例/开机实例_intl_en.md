## Overview
This document describes how to start up an instance via the console or an API.

## Directions
<dx-tabs>
::: Starting up an instance via the console

#### Starting up one instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. On the instance management page, proceed according to the actually used view mode:
   - **List view**: in the row of the target instance, select **More** > **Instance Status** > **Start Up** in the **Operation** column on the right as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/900a2d8fb4a48ef1e9746922d6447666.png)
   - **Tab view**: on the page of the target instance, select **Start Up** in the top-right corner as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/c62f67a3415635ddf535442b4b73343c.png)


#### Starting up multiple instances
Select the instances you want to start up, and click **Start up** at the top of the list to start the selected instances, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/dd734cf2e58b3e9d1ee1114bb94fe41a.png)

:::
::: Starting up instances via API
Use the [StartInstances](https://intl.cloud.tencent.com/document/product/213/33236) API to start up an instance.

:::
</dx-tabs>

## Subsequent Operations
Once the instance starts up, you can perform the following operations:
- **Logging in to the instance**: depending on the instance type, log in to the [Linux instance](https://intl.cloud.tencent.com/document/product/213/5436) or the [Windows instance](https://intl.cloud.tencent.com/document/product/213/5435).
- **[Initializing cloud disks](https://intl.cloud.tencent.com/document/product/362/31596)**: initialize the cloud disks mounted to the instance by formatting, partitioning, and creating a file system.
