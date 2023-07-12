## Overview

CI can monitor various service capabilities. The monitoring data window of CI's statistics displays the monitoring metrics of image processing, media processing, content recognition, and document processing.

You can query the details of data processing in different storage classes for different time periods. The following describes how to view the monitoring data of a single bucket with a root account or sub-account.


## Querying with a Root Account

1. Log in to the [CI console](https://console.cloud.tencent.com/ci).
2. Click **Bucket Management** on the left sidebar to enter the bucket list.
3. Find the target bucket and click **Data Monitoring** on the right.
4. On the data monitoring page, view the information.



## Querying with a Sub-account

To query monitoring data with a sub-account in the console, you need to first grant the sub-account relevant permissions.

You can grant such permission by using a **Policy Template** or **Custom Access Policy**.


<a id="celie"></a>
### Using a policy template

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account and select **Users** > **User List** to enter the user list page.
2. Find the target sub-account and click **Authorize** in the **Operation** column on the right.

3. Search for and select the `QcloudMonitorFullAccess` policy in the pop-up window and click **OK** to associate it with the sub-account. Then, the sub-account can access monitoring reports.
>! This policy template grants the sub-account the **full access** to CM. To protect the security of your account, you can customize an access policy to grant only read permissions to the sub-account.

### Using a custom access policy

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account.
2. On the left sidebar, click **Policies** > **Create Custom Policy** > **Create by Policy Syntax**.
3. Select **Blank Template** and click **Next**.

4. Copy and paste the following policy syntax into the **Edit Policy Content** input box.
You can rename the policy as needed.
Policy syntax:
```shell
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action":[
                "monitor:GetMonitorData"
            ],
            "resource": "*"
        }
    ]
}
```
5. Click **Create Policy**.
After the policy is created successfully, you can associate it with the sub-account as instructed in [Authorizing by policy template](#celie).
