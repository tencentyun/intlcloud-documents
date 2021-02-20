## Overview

You can add a policy for a bucket via the COS console to allow/forbid an account, IP, or IP range to access the COS resources. For more information about bucket policy and examples, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023) and [Examples of Bucket Policies](https://intl.cloud.tencent.com/document/product/436/18031). The following describes how to add a bucket policy.

>! Each root account can create up to 1,000 bucket ACL rules.

## Prerequisites

You have created a bucket. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**. Then, click the bucket for which you want to add a bucket.
3. Click **Permission Management** > **Permission Policy Settings**. Then, you can add a bucket policy using **Visual editor** or **JSON**. For more information about the configuration items, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).
   ![](https://main.qcloudimg.com/raw/3e3c1c923384785190720b8505e94025.png)
 - **Visual editor**
   Below is an example:
   ![](https://main.qcloudimg.com/raw/950c03ba2eb714c102b68b57d025792d.png)
 - **JSON**
   Click **Edit** to input the user-defined policy syntax. COS provides policy syntax for various scenarios. For more information, please see [Examples of Bucket Policies](https://intl.cloud.tencent.com/document/product/436/18031).
     ![](https://main.qcloudimg.com/raw/b4e280ccbd67b081dcb59c4039f4d3b0.png)
4. Click **Save**. In this way, if a sub-account logs in to the COS console, it can only access resources allowed by the policy.
