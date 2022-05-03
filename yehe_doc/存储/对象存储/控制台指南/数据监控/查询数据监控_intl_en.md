## Overview

COS can monitor your stored data. The COS data monitoring window displays data regarding request quantity, traffic, return code, data retrieval, etc. You can also query the details and trends of data in different storage classes according to different periods. The following describes how to view the monitoring data of a single bucket using a root account or sub-account.

>?To view the summary of all data stored under your account, please go to [Data Overview](https://console.cloud.tencent.com/cos5/monitor/overview) in the COS console.


## Querying with a Root Account

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Locate the desired bucket and click **Monitor** on its right. Alternatively, you can click the desired bucket and then choose the **Data Monitoring** tab on the page that is displayed. The monitoring items are described as follows:
3. Go to the data monitoring page as shown below. The different monitoring items are as follows:
 - Storage Usage: storage usage of each storage class
 - Number of Objects: number of objects (including incomplete multipart uploads) stored in the bucket
 - Number of incomplete multipart uploads: number of incomplete multipart uploads stored in the bucket. If an ongoing upload is suspended or canceled, the corresponding files will be stored in the bucket as incomplete multipart uploads.
 >?
 >
 >- To query the number of objects in a folder, please see [Viewing Folder Details](https://intl.cloud.tencent.com/document/product/436/31633).
 >- If versioning is enabled, multiple versions of an object are counted as separate objects.
 - Request Count: number of all requests (including all GET requests and PUT requests), as well as the read/write requests of STANDARD and STANDARD_IA
 - Traffic: public/private network traffic, CDN origin-pull/cross-region replication traffic, and total upload traffic of public and private network
 - Return Code: number of 2xx, 3xx, 4xx, and 5xx status code as well as their proportion
 - Data Retrieval: statistics of data retrievals for STANDARD_IA
   ![](https://main.qcloudimg.com/raw/2af3c5e7b113003ca1379547903751ed.png)

>?
>
>- Under **Details** in the **Current** section, you can query monitoring data (including storage usage, number of objects, requests, traffic, return code, and data retrieval) of different periods, such as today, yesterday, last 7 days, last 30 days, or a custom period.
>- In the **This month** section, you can view data for the month, including the daily average storage usage of each storage class and total traffic (accumulated public network traffic, accumulated CDN origin-pull traffic, and accumulated cross-region replication traffic).
>- **Storage** and **Number of Objects** show only data after March 01, 2020. For more detailed data, please go to [Billing Center](https://console.cloud.tencent.com/expense/bill/dosageDownload), select a period, and export the data.

## Querying with a Sub-account

To query monitoring data with a sub-account via the console, you need to first grant the sub-account permission to query the monitoring data.

You can grant such permission by using a **Policy Template** or **Custom Access Policy**.


<a id="celie"></a>

### Using a policy template

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) using the root account, and select **Users** > **User List** to enter the user list page.
2. Locate the sub-account, and click **Authorize** in the **Operation** column on the right.
   ![](https://main.qcloudimg.com/raw/03804c04df5e91fc0472e8d0297f694d.png)
3. Search and select the `QcloudMonitorFullAccess` policy in the policy list and click **OK** to attach it to the sub-account. Then the sub-account should be able to access monitoring reports.
   ![](https://main.qcloudimg.com/raw/c2e07335d2e68e2f077138ff9d73837f.png)
>!This policy template grants **full permission** for cloud monitoring to a sub-account. To better ensure the security of your account, you can customize an access policy to grant only read permission to your sub-accounts.

### Using a custom access policy

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) using the root account, and select **Policies** > **Create Custom Policy** > **Create by Policy Syntax**.
2. Use the blank template to create a new policy.
   ![](https://main.qcloudimg.com/raw/4a61be28b1ab0146eca948215aad0f2e.png)
3. Enter the following policy syntax into the **Edit Policy Content** input box in the blank template. You can rename the policy, making it easy to find as needed.
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

4. Click **Done**. After the policy is created successfully, you can attach it to a sub-account. For directions, please see [Configuring by Policy Template](#celie).
