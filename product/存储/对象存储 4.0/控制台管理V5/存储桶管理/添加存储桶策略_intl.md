## Overview

You can add a policy to a bucket in the COS Console to allow or forbid an account, IP, or IP range to access the COS resources. For more information about bucket policy and samples, see [Access Policy Overview](https://cloud.tencent.com/document/product/436/18023) and [Bucket Policy Samples](https://cloud.tencent.com/document/product/436/18031). The following section will guide you through how to add a bucket policy.

> !For each root account, the total number of created object ACLs, bucket ACLs, and bucket policies cannot exceed 1,000.

## Steps

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**.
3. Select the bucket to which to add a bucket policy and enter it.
![](https://main.qcloudimg.com/raw/8a4ceacd4892f0f9f660a6f6fa9dacd0.png)
2. Click **Permission Management** and find **Policy Permission Settings**. COS supports adding the bucket policy through **graphic settings** and **policy syntax**, which you can choose as you like.
![](https://main.qcloudimg.com/raw/d9e37ef39354e9edf9340565e67aedce.png)
 - **Graphic settings**
 Below is an example:
![](https://main.qcloudimg.com/raw/8acbe5db2599c3f5dc482c9e5fc1bf8e.png)
 - **Policy syntax**
 Click **Edit** and enter the policy syntax you define. COS provides policy syntax for a rich variety of scenarios. For more information, see [Bucket Policy Samples](https://cloud.tencent.com/document/product/436/18031).
   ![](https://main.qcloudimg.com/raw/d5fe3da89e17a9d507df3a1699311a80.png)
3. After confirming that the configuration information is correct, click **OK** or **Save**. At this point, sub-account can only access the resource range set by the policy after logging in to the COS Console.

