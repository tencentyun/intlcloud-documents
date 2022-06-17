## Overview
This document describes how to perform batch operations on Lighthouse instances in the same region, such as starting and shutting down instances and resetting passwords.


## Notes
- For a batch operation, all instances must be in the same region.
- All selected instances must support the operation.
For example, Windows instances don't support SSH keys, so you cannot batch bind SSH keys when Windows and Linux instances are selected at the same time.


## Directions
This document describes how to batch shut down instances. 

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the target instances in a region.
![](https://qcloudimg.tencent-cloud.cn/raw/6c5aff016746b4fe7bd82d53f36d3253.png)
2. Select **Shut down** at the top of the page.
3. In the **Shut down** pop-up window, click **OK**.
