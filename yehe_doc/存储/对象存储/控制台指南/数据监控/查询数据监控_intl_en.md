## Overview

COS allows you to monitor your stored data. The COS data monitoring window displays information regarding request quantity, traffic, return code, data retrieval, etc. You can also query the details and trends of data in different storage classes for different time periods. The following describes how to view the monitoring data of a single bucket with a root account or sub-account.

>?To view the summary of all data stored under your account, go to [Data Monitoring](https://console.cloud.tencent.com/cos5/monitor/overview) in the COS console.


## Querying with Root Account

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Find the target bucket and click **Monitor** on the right.
You can also select the target bucket and click **Data Monitoring** on the left sidebar on the bucket details page.
4. On the monitoring data page, view the information.
![](https://main.qcloudimg.com/raw/2af3c5e7b113003ca1379547903751ed.png)
Monitoring items are as described below:
 - Storage: Storage usage of each storage class.
 - Number of Objects: Number of objects (including incomplete multipart uploads) stored in the bucket.
 - Number of Incomplete Multipart Uploads: Number of incomplete multipart uploads stored in the bucket. If an ongoing upload is suspended or canceled, the corresponding files will be stored in the bucket as incomplete multipart uploads.
>?
>- To query the number of objects in a folder, see [Viewing Folder Details](https://intl.cloud.tencent.com/document/product/436/31633).
>- If versioning is enabled, multiple versions of an object are counted as separate objects.
>
 - Requests: Number of all requests (including GET and PUT requests), as well as read/write requests of STANDARD and STANDARD_IA.
 - Traffic: Public/Private network traffic, CDN origin-pull/cross-region replication traffic, and total upload traffic over public and private networks.
 - Return Code: Number of 2xx, 3xx, 4xx, and 5xx status codes as well as their proportion.
 - Data Retrieval: Statistics of data retrievals from STANDARD_IA.
>?
>- Under **Details** in the **Current** section, you can query monitoring data (including storage usage, number of objects, requests, traffic, return code, and data retrieval) of different time periods, such as today, yesterday, last 7 days, last 30 days, or a custom time period.
>- In the **This month** section, you can view data for the month, including the daily average storage usage of each storage class as well as total traffic (total public network traffic, total CDN origin-pull traffic, and total cross-region replication traffic).
>- **Storage** and **Number of Objects** show only data after March 1, 2020. For more detailed data, go to [Billing Center](https://console.cloud.tencent.com/expense/bill/dosageDownload), select a time period, and export the data.
>

## Querying with Sub-account

To query monitoring data with a sub-account in the console, you need to first grant the sub-account relevant permissions.

You can grant such permissions by using a **policy template** or **custom access policy**.


<a id="celie"></a>
### Authorizing by policy template

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account and select **Users** > **User List** to enter the user list page.
2. Find the target sub-account and click **Authorize** in the **Operation** column on the right.

3. Search for and select the `QcloudMonitorFullAccess` policy in the pop-up window and click **OK** to associate it with the sub-account. Then, the sub-account can access monitoring reports.

>! This policy template grants the sub-account the **full access** to CM. To protect the security of your account, you can customize an access policy to grant only read permissions to the sub-account.
>

### Authorizing by custom access policy

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account.
2. On the left sidebar, click **Policies** > **Create Custom Policy** > **Create by Policy Syntax**.
3. Select **Blank Template** and click **Next**.

4. Copy and paste the following policy syntax into the **Policy Content** input box.
You can rename the policy as needed.
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
![](https://main.qcloudimg.com/raw/f6a4b0d8573745139beb03cdb3a1b3ec.png)
4. Click **OK**.
After the policy is created successfully, you can associate it with the sub-account as instructed in [Authorizing by policy template](#celie).
