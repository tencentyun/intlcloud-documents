## Overview
COS can monitor your stored data. The COS data monitoring window displays data regarding request quantity, traffic, return codes, data reading, etc. You can also query the details and trends of data in different storage classes according to different time periods. The following describes how to view the monitoring data of a single bucket using a root account or sub-account.

>To view the summary of all data stored in your account, go to the [Monitoring Management](https://console.cloud.tencent.com/cos5/monitor/overview) page on the COS console.


## Querying with a root account

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Find the bucket whose statistics you want to view and click <img src="https://main.qcloudimg.com/raw/c288d6a69541eeeb393bc9beeef39851.png"  style="margin:0;"> in the Monitoring column as shown below:
![](https://main.qcloudimg.com/raw/9c4319d2a97c46b568bd37e75bffc09b.png)
3. Open the data monitoring page as shown below. The different monitoring categories are as follows:
 - Storage: queries the storage usage in different storage classes.
 - Number of Objects: the number of objects present in a bucket.
 >
 >- To count the number of objects in a folder, see [View Folder Details](https://intl.cloud.tencent.com/document/product/436/31633).
 >- If you have versioning enabled, object versions with the same name are counted as a single object in the bucket.
 - Requests: allows you to count the number of Read/Write requests for STANDARD and STANDARD_IA data.
 -Traffic: allows you to view the public network traffic, private network traffic, CDN origin-pull traffic, and upload traffic.
 -Return Code: allows you to view the statistics on 2XX, 3XX, 4XX, and 5XX status codes.
 - Reads: allows you to view the statistics on STANDARD data reads, and STANDARD_IA data retrievals.


![](https://main.qcloudimg.com/raw/2af3c5e7b113003ca1379547903751ed.png)

>
>- Under **Details** in the **Current** section, you can query monitoring details including storage usage, number of objects, requests, traffic, return codes, and reads based on different time periods, such as today, yesterday, last 7 days, last 30 days, last 3 months, and last 6 months.
>- In the **This month** section, you can view data for the month, including the daily average storage usage of each storage class and total traffic (accumulated public network traffic, accumulated CDN origin-pull traffic, and accumulated cross-region replication traffic).


## Querying with a sub-account
To query monitoring reports with a sub-account using the console, you need to first grant permission for the sub-account to do so.

You can grant such permission by using a **Policy Template** or **Custom Access Policy**.


<a id="celie"></a>
### Using a policy template

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using the root account, and select **Users** > **User List** to enter the user list page.
2. Locate the sub-account, and click **Grant Permission** under the Operation column on the right.
![](https://main.qcloudimg.com/raw/03804c04df5e91fc0472e8d0297f694d.png)
2. Search and select the `QcloudMonitorFullAccess` policy in the policy list and click **OK** to attach it to the sub-account. Then the sub-account should be able to access monitoring reports.
![](https://main.qcloudimg.com/raw/c2e07335d2e68e2f077138ff9d73837f.png)
>This policy template grants **full permission** for cloud monitoring to a sub account. To better protect the security of your account, you can customize an access policy to only grant read permission to your sub-accounts.

### Using a custom access policy

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using the root account, and select **Policies** > **Create Custom Policy** > **Create by Policy Syntax**.
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

5. Click **Done**. After the policy is created successfully, you can associate it with a sub-account. For directions, see [Configuring by Policy Template](#celie).