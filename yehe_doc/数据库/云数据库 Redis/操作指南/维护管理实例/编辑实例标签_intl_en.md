## Overview
A tag consists of a tag key and value. It can be used to tag TencentDB for Redis instances. If you have multiple types of resources under your Tencent Cloud account which are correlated in many ways, and your resources are growing and becoming increasingly difficult to manage, you can use tags to group and categorize resources that serve the same purpose or are associated with each other. In this way, when performing daily Ops or troubleshooting, you can quickly search for resources and perform batch operations for more efficient Ops.

## Billing
Tag management is a free service provided by Tencent Cloud for your Tencent Cloud account. You can simply go to the [console](https://console.cloud.tencent.com/tag/resources) to use this service.

## Notes
- A tag consists of one tag key and one tag value (tagKey:tagValue).
- Up to 50 tags can be bound to an instance.
- For each instance, a tag key can correspond to only one tag value.

## Prerequisites
- You have [applied for a TencentDB for Redis instance](https://intl.cloud.tencent.com/document/product/239/37712).
- The current tags of the instance need to be edited.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Enter the **Edit Tag** page in any of the following ways:
   - In the **Operation** column of the target instance, select **More** > **Edit Tag**.
   - Click the target instance ID and click <img src="https://qcloudimg.tencent-cloud.cn/raw/c3386f46a3b0588a84b3c0bf6f952200.png" style="zoom:66%;" /> on the right of **Tag** in the **Configuration** section on the **Instance Details** page.
5. On the **Edit Tag** page, select an appropriate tag key in the **Tag Key** drop-down list and select the tag value in the **Tag Value** drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/2efbe2d7e4d64953ff44decf585bf5b1.png)
6. (Optional) If existing tags don't meet your business requirements, perform the following operations: 
 1. In the top-right corner of the current page, click **Manage Tags**.   
 2. On the **Manage Tags** page, click **Create Tag**.
 3. On the **Create Tag** page, read the notes on tag configuration.
 4. Set a new tag key in the **Tag Key** input box and enter the tag value in the **Tag Value** input box. The requirements for the tag key are as follows:
    - It can contain 1–127 characters.
    - It can contain letters and digits.
    - It can contain the following special symbols: plus sign, equal sign, underscore, hyphen, dot, colon, slash, @, parentheses, and brackets.
  5. Click **OK**.
  6. Go back to the **Edit Tag** page of the database instance. Click **Reload** in the **Tag Key** drop-down list, select the created tag key, and select the tag value.
7. Click **OK**.

## References
For more information on tag management, see [Tag](https://intl.cloud.tencent.com/document/product/651).

