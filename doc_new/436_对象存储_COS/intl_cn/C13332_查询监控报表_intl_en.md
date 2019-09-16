## Overview

COS can monitor stored data. In the monitor window, you can find details and trends of various metrics, including basic information such as number of requests, traffic, and data reads as well as statistics on return codes.



## Directions
### Querying with a Root Account

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Find the bucket whose statistics you want to view and click <img src="https://main.qcloudimg.com/raw/c288d6a69541eeeb393bc9beeef39851.png"  style="margin:0;"> in the Monitor column as shown below:
![](https://main.qcloudimg.com/raw/0f472bf8920d5a27c71fae249345dc9e.png)
3. Enter the monitoring page as shown below:
![](https://main.qcloudimg.com/raw/3afedfb0911ffba4549670914da2c463.png)

>?
> - In the **Current** section, you can switch between current data and data of this month, including storage capacity, number of read and write requests, traffic, return codes, and data reads. The time granularities available include today, yesterday, last 7 days, and last 30 days.
> - In the **This Month** section, you can view data for the month, including the daily average storage capacity of each storage class and total traffic (accumulated public network traffic, accumulated CDN origin-pull traffic, and accumulated cross-region replication traffic).

### Querying with a Sub-account
To query monitoring reports with a sub-account, you need to first grant the sub-account permission to do so. You can grant the permission using a policy template or a custom access policy.

#### Granting a Sub-account Permission to Access Monitoring Reports
<a id="celie"></a>
#### Configuring with a Policy Template

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using the root account, click **Users** in the left sidebar, and click a sub-account.
![](https://main.qcloudimg.com/raw/482b09f65e41238be79052cda852f2c8.png)
2. Select the `QcloudMonitorFullAccess` policy in the policy list and click OK to add it to the sub-account. Then the sub-account should be able to access monitoring reports.
![Aaron Swartz](https://main.qcloudimg.com/raw/c1ffcc2c93a36a9c565b78b549b01d9b.png)
>! This policy template will grant a sub-account full access to Cloud Monitor. For more account security, you can customize an access policy to grant Read access to your sub-accounts.

#### Configuring with a Custom Access Policy

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using the root account and select **Policies** > **Create a Custom Policy**.
![](https://main.qcloudimg.com/raw/17b0f09122c4d2679735898458b9f8f1.png)
2. Click **Create by Policy Syntax**.
![](https://main.qcloudimg.com/raw/3e65df3bbd8ddfc73b5b3f6f26bb8274.png)
3. Use the blank template to create a new policy.
![](https://main.qcloudimg.com/raw/43f2263d11c2684ad10d9857fd18cf2b.png)
4. Copy and paste the following policy syntax into the **Edit Policy Content** input box in the blank template. You can rename the policy as needed.
Policy syntax:
```shell
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "monitor:GetMonitorData"
            ],
            "resource": "*"
        }
    ]
}
```
Edit the policy content in the input box:
![Aaron Swartz](https://main.qcloudimg.com/raw/18e892e58e8c6c9966a169ad22e1d963.png)
5. Click **Create a Policy**. After the policy is created successfully, you can associate it with a sub-account. For directions, see [Configuring by Policy Template](#celie).
