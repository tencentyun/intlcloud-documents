## Overview
This document describes how to reset a CVD instance to reinitialize its system disk.
When resetting a CVD instance, you can choose whether to unbind the current user by selecting **Unbind user** or **Bind the same user after reset** as needed.
>! The system disks of the instances will be reset to the specified image. The data will be cleared and cannot be recovered.

## Directions
### Resetting one CVD instance
1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. Select the target instance and click **More** > **Actions** > **Reset** in the **Operation** column on the right.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cd011d711db9d9e95c20d7667067501f.png" style="zoom:67%;" />
### Resetting multiple CVD instances
1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. Select all the target CVD instances and click **Reset** at the top of the list to batch reset them.
![](https://qcloudimg.tencent-cloud.cn/raw/c90b0421f521f2f422e82691ce351b79.png)

## Notes
1. The system disks of the instances will be reset. The data will be cleared and cannot be recovered. Ask users to back up their data first.
>? The data disk (if any) will not be affected.

2. You cannot reset standard and graphic instances at the same time.
3. The snapshots of the instance's system disk will also be deleted.
