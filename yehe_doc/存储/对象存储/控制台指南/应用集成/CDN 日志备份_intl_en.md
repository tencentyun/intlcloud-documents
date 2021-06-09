## Overview

After a domain name is connected to [Content Delivery Network (CDN)](https://intl.cloud.tencent.com/document/product/228/2939), users’ resource requests will be scheduled to CDN nodes. If a CDN node has the resource cached, it returns the resource directly. Otherwise, the request will be passed through to the origin server to pull the requested resource.

CDN nodes respond to most of the user requests. To facilitate access analysis, CDN packages access logs of the entire network at an hourly granularity.

COS introduces the [SCF](https://intl.cloud.tencent.com/document/product/583)-based CDN Log Backup feature for users to dump CDN logs to COS, so that they can analyze access behaviors, monitor service quality, and do more.

After you configure a log backup rule for a bucket, SCF will dump the CDN logs to the bucket according to the time granularity configured.

## Notes

- Once you added a CDN log backup rule to your bucket via the COS console, the backup function can be viewed in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- SCF-available regions support backing up CDN logs to COS, including Guangzhou, Shanghai, Hong Kong (China), Beijing, Chengdu, Singapore, Mumbai, Toronto, Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Application Integration**. Then, find **CDN Log Backup**.
3. Click **Configure Backup Rules** to go to the configuration page.
4. Click **Add Function**.
>! If you haven’t activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. On the page that is displayed, configure the following items:
![](https://main.qcloudimg.com/raw/381a243bc2333c2a4dbd56f436826a33.png)
 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: a COS bucket that stores the CDN logs
 - **Trigger Period**: a period to trigger the CDN log backup (a timer is used). Every day and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, please see [Cron Documentation](https://intl.cloud.tencent.com/document/product/583/9708).
 - **CDN Acceleration Domain**: one or multiple domains whose logs are to dump
 - **Destination Path**: a path to deliver the logs. You can deliver logs to the root directory or specify a path prefix.
 - **SCF Authorization**: (required) SCF needs to be authorized to read CDN logs and dump them to the specified bucket.
6. Click **Confirm**. After the CDN backup rule is created, you can view it in the list.
![](https://main.qcloudimg.com/raw/1435b905753fbd432693d6f5d69f2c46.png)
You can perform the following operations on the created CDN log backup rule:
 - Click **View Log** to view the historical running status of CDN log backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to modify the CDN log backup rule.
 - Click **Delete** to delete an unwanted CDN log backup rule.
