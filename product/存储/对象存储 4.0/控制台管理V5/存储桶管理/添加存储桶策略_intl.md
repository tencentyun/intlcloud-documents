## Overview

You can add a policy to a bucket in the COS Console to allow or forbid an account, IP, or IP range to access the COS resources. For more information about bucket policy and samples, see [Access Policy Overview](https://intl.cloud.tencent.com/document/product/436/18023) and [Bucket Policy Samples](https://intl.cloud.tencent.com/document/product/436/18031). The following section will guide you through how to add a bucket policy.

> For each root account, the total number of created object ACLs, bucket ACLs, and bucket policies cannot exceed 1,000.

## Steps

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**.
3. Select the bucket to which to add a bucket policy and enter it.
![](https://main.qcloudimg.com/raw/cce97e71006f02e42729873b911ad0e0.png)
4. Click **Permission Management** and find **Bucket Policy**. COS supports adding the bucket policy through **Generator** and **Strategy grammer**, which you can choose as you like.
![](https://main.qcloudimg.com/raw/4bb021375a39023a729461b987e4568c.png)
 - **Graphic settings**
 Below is an example:
![](https://main.qcloudimg.com/raw/56918d31ca17e475dc5ec7eb23949bb2.png)
 - **Strategy grammar**
 Click **Edit** and enter the policy syntax you define. COS provides policy syntax for a rich variety of scenarios. For more information, see [Bucket Policy Samples](https://intl.cloud.tencent.com/document/product/436/18031).
   ![](https://main.qcloudimg.com/raw/773c123bdab260bea196f6830eb288e2.png)
5. After confirming that the configuration information is correct, click **OK** or **Save**. At this point, sub-account can only access the resource range set by the policy after logging in to the COS Console.

