## Overview
This document describes how to reset a CVD instance to reinitialize its system disk.
When resetting a CVD instance, you can choose whether to unbind the current user by selecting **Unbind user** or **Bind the same user after reset** as needed.
>! The system disks of the instances will be reset to the specified image. The data will be cleared and cannot be recovered.

## Directions
### Resetting one CVD instance
1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. Select the target instance and click **More** > **Actions** > **Reset** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/845726836f614617444d3c23389c5571.png)
### Resetting multiple CVD instances
1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. Select all the target CVD instances and click **Reset** at the top of the list to batch reset them.
![](https://qcloudimg.tencent-cloud.cn/raw/d28f9bebd33c9240c7e291fff2a2aa13.png)

## Notes
1. The system disks of the instances will be reset. The data will be cleared and cannot be recovered. Ask users to back up their data first.
>? The data disk (if any) will not be affected.

2. You cannot reset standard and graphic instances at the same time.
3. The snapshots of the instance's system disk will also be deleted.
