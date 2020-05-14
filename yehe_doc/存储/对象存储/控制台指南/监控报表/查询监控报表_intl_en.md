## Overview
COS can monitor stored data. In the COS monitor window, you can query the details and trends of data from different storage classes by different periods, including the number of requests, traffic, statistics on return codes, and data reads.



## Querying with a Root Account

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Find the bucket whose statistics you want to view and click <img src="https://main.qcloudimg.com/raw/c288d6a69541eeeb393bc9beeef39851.png"  style="margin:0;"> in the Monitoring column as shown below:
![](https://main.qcloudimg.com/raw/9c4319d2a97c46b568bd37e75bffc09b.png)
3. Enter the monitoring page as shown below:
![](https://main.qcloudimg.com/raw/2af3c5e7b113003ca1379547903751ed.png)

>
> - In the **Current** section, you can find the storage capacity and number of objects for different storage classes. The **Details** section allows you to view statistics on storage capacity, objects, read and write requests, traffic, return codes, and data reads. The time granularities available include today, yesterday, last 7 days, last 30 days, last 3 months, and last 6 months.
> - In the **This month** section, you can view data for the month, including the daily average storage capacity of each storage class and total traffic (accumulated public network traffic, accumulated CDN origin-pull traffic, and accumulated cross-region replication traffic).
> - **Storage** and **Number of Objects** only show data after March 01, 2020. For more detailed data, please go to [Billing Center](https://console.cloud.tencent.com/expense/bill/dosageDownload).

## Querying with a Sub-Account
To query monitoring reports with a sub-account, you need to first grant the sub-account permission to do so. You can grant the permission using a policy template or a custom access policy.

#### Granting a sub-account permission to access monitoring reports
<a id="celie"></a>
#### Configuring with a policy template

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using the root account, and select **Users** > **User List** to enter the user list page.
2. Locate the sub-account, and click **Grant Permission** under the Operation column on the right.
![](https://main.qcloudimg.com/raw/03804c04df5e91fc0472e8d0297f694d.png)
2. Search and select the `QcloudMonitorFullAccess` policy in the policy list and click **OK** to attach it to the sub-account. Then the sub-account should be able to access monitoring reports.
![](https://main.qcloudimg.com/raw/c2e07335d2e68e2f077138ff9d73837f.png)
> This policy template will grant a sub-account full access to Cloud Monitor. For more account security, you can customize an access policy to grant Read access to your sub-accounts.

#### Configuring with a custom access policy

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using the root account, and select **Policies** > **Create Custom Policy** > **Create by Policy Syntax**.
2. Use the blank template to create a new policy.
![](https://main.qcloudimg.com/raw/4a61be28b1ab0146eca948215aad0f2e.png)
3. Copy and paste the following policy syntax into the **Policy content** input box in the blank template. You can rename the policy as needed.
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
![](https://main.qcloudimg.com/raw/f6a4b0d8573745139beb03cdb3a1b3ec.png)

5. Click **Done**. After the policy is created successfully, you can associate it with a sub-account. For directions, see [Configuring by Policy Template](#celie).
