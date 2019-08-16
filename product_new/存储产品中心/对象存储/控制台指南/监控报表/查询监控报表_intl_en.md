## Overview

COS is capable of monitoring stored data and displaying details and trends of various metrics in the monitor window, including basic information such as requests, traffic, and data reads as well as return code statistics.



## Directions
### Querying with a Root Account

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Find the bucket for which you want to view the statistics and click <img src="https://main.qcloudimg.com/raw/c288d6a69541eeeb393bc9beeef39851.png"  style="margin:0;"> in the Monitor column as shown below:
![](https://main.qcloudimg.com/raw/1389c4be85304d4e5193017e7e9adee2.png)
3. Enter the monitoring pager as shown below:
![](https://main.qcloudimg.com/raw/45346a072ddff035e2b13a42af03a8dc.png)

>- In the **Current Data** section, you can switch between current data and month-to-date data, including storage capacity, number of read and write requests, traffic, return codes, and data reads. The time granularities available include today, yesterday, past 7 days, and past 30 days.
> - In the **Month-to-date Data** section, you can view the daily average storage capacity in each storage class and total traffic (accumulated public network traffic, accumulated CDN origin-pull traffic, and accumulated cross-region replication traffic) in the current month.

### Querying with a Sub-account
You need to first grant a sub-account permission to query monitoring reports before it can do so by logging in to the console. You can grant the permission using a policy template or a custom access policy.

#### Configuring Permission to Access Monitoring Reports for a Sub-account
<a id="celie"></a>
#### Configuring by Policy Template

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using the root account, click **Users** in the left sidebar, and click a created sub-account.
![](https://main.qcloudimg.com/raw/03804c04df5e91fc0472e8d0297f694d.png)
2. Search for the `QcloudMonitorFullAccess` policy in the policy list and click OK to add it to the sub-account so that the sub-account can access monitoring reports.
![Aaron Swartz](https://main.qcloudimg.com/raw/b95fb564490b29f93595cc1489dbe19e.png)
> This policy template will grant full access to Cloud Monitor. If you want to protect account security, you can customize an access policy to grant the sub-account read permission only.

#### Configuring by Custom Access Policy

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using the root account and select **Policies** > **Create a Custom Policy**.
![](https://main.qcloudimg.com/raw/8f7f1b6f1b0772453b6e5df9f4ecf9cb.png)
2. Click **Create by Policy Syntax**.
![](https://main.qcloudimg.com/raw/93f9e7a548d6b7439c654ca7df9bfcf9.png)
3. Select the blank empty template to create the policy.
![](https://main.qcloudimg.com/raw/588a262be122d028b266879a3fb5f3cd.png)
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
![Aaron Swartz](https://main.qcloudimg.com/raw/9d26a12371c4e718c41816c065f49cac.png)

5. Click **Create a Policy**. After the policy is created successfully, you can associate it with the sub-account for authorization. For directions, see [Configuring by Policy Template](#celie).
