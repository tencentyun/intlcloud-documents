## Overview
This document describes how to edit the tags of resources.

## Usage Limits

There are several limits on editing tags:
- Quantity: Each Tencent Cloud resource allows up to 50 tags.
- Tag key limits:
  - A tag key cannot start with `qcloud`, `tencent`, or `project`.
  - A tag key can contain up to 255 characters, including numbers, letters, and `+=.@-`.
- Tag value limits: A tag value can contain up to 127 characters, including numbers, letters and `+=.@-`. It can be left empty if necessary.


## Prerequisites
Log in to the [CVM console](https://console.cloud.tencent.com/cvm).

## Directions

<dx-tabs>
::: Single instance

1. Open the tag editing page.
   - **List view**: Select the target instance and click **More** > **Instance Settings** > **Edit Tags**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7f5ff3c9a726569805f3d085ffd8f8dd.png)
   - **Tab view**: Select the target instance and click **More Actions** > **Instance Settings** > **Edit Tags**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e558f115b9e41be9afd18c7649c9a823.png)
2. Add, modify or delete the tags in the pop-up window.
:::
::: Multiple instances


<dx-alert infotype="explain" title="">
You can batch edit tags for up to 20 resources at a time.
</dx-alert>


1. On the instance management page, select the target instances and click **More Actions** > **Instance Settings** > **Edit Tags**.
![](https://qcloudimg.tencent-cloud.cn/raw/d07d2ab7830b9f4431bd23826892938c.png)
2. Add, modify, and delete tags in the pop-up window.
:::
</dx-tabs>

## References

For information on how to use tags, please see [User Guide on Tags](https://intl.cloud.tencent.com/document/product/213/19548).

