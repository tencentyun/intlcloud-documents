## Overview
This document shows you how to create a sub-account and grant permissions to it to manage SSM.
## Directions
1. Create a sub-account. Log in to the Tencent Cloud [CAM console](https://console.cloud.tencent.com/cam/overview) using the root account. In the left sidebar, click **Users** -> **User List**. On the **User List** page, click **Create User** to create a sub-account.
![](https://main.qcloudimg.com/raw/6c2f5ac34a9cdf2ef3b7a3142d6d0b10.png)
2. Create an API key. You can click the name of the sub-account to go to its **User Details** page. Click **API Key** -> **Create Key** to create SecretId and SecretKey. You can use this API key to access SSM.
>?If you do not need to manage SSM through APIs, you can authorize the sub-account directly.

![](https://main.qcloudimg.com/raw/eea20b23c0b97942f4aefce64904f640.png)
3. Authorize the sub-account. You can add the SSM policy to the newly created sub-account so that it can access SSM. On the **User Details** page of the sub-account, click **Permissions** > **Associate Policy** to go to the **Add Policy** page.
![](https://main.qcloudimg.com/raw/5b06780aa1a27c8ac39069d259621196.png)
4. Add a policy. On the **Add Policy** page, click **Select policies from the policy list**, choose the appropriate SSM policy, and click **Next** > **Confirm**. In this way, you can grant permissions to the sub-account to access SSM.
![](https://main.qcloudimg.com/raw/3d6efb2e195a679c9e7146798624a182.png)
