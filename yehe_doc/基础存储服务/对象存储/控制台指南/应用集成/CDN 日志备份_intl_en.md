## Overview

After a domain name is connected to [Content Delivery Network (CDN)](https://intl.cloud.tencent.com/document/product/228/2939), users' resource requests will be scheduled to CDN nodes. If a CDN node has the resource cached, it returns the resource directly. Otherwise, the request will be passed through to the origin server to pull the requested resource.

CDN nodes respond to most of the user requests. To facilitate access analysis, CDN packages access logs of the entire network at an hourly granularity.

The CDN log backup feature is provided by COS based on [SCF](https://www.tencentcloud.com/document/product/583) to dump CDN logs to COS, which facilitates access behavior analysis and service quality monitoring.

After you configure a log backup rule for a bucket, SCF will dump the CDN logs to the bucket according to the time granularity configured.

## Notes

- Once you added a CDN log backup rule to your bucket via the COS console, the backup function can be viewed in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- CDN log backup is supported in SCF-enabled regions, including Guangzhou, Shanghai, Hong Kong (China), Beijing, Chengdu, Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see the [SCF documentation](https://www.tencentcloud.com/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Application Integration** > **Data Backup** and find **CDN Log Backup**.
3. Click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. In the pop-up window, configure the following items:
![](https://main.qcloudimg.com/raw/381a243bc2333c2a4dbd56f436826a33.png)
 - **Function Name**: Uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: A COS bucket that stores the CDN logs
 - **Trigger Period**: A period to trigger the CDN log backup (a timer is used). Every day and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows the Local Standard Time. For detailed configuration policies, see [Timer Trigger Description](https://intl.cloud.tencent.com/document/product/583/9708).
 - **CDN Acceleration Domain**: One or multiple domains whose logs are to dump
 - **Destination Path**: A path to deliver the logs. You can deliver logs to the root directory or specify a path prefix.
 - **SCF Authorization**: (required) SCF needs to be authorized to read CDN logs and dump them to the specified bucket.
6. Click **Confirm**. After the CDN backup rule is created, you can view it in the list.
You can perform the following operations on the created CDN log backup rule:
 - Click **Log** to view the historical running status of CDN log backup. If an error is reported, you can click **Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **More** > **Edit** to modify the CDN log backup rule.
 - Click **More** > **Delete** to delete the unwanted CDN log backup rule.
