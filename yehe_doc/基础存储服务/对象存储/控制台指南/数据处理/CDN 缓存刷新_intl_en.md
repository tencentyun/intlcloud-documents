## Overview

CDN (Content Delivery Network，CDN) cache purging is a Tencent Cloud COS (Cloud Object Storage) feature based on [SCF (Serverless Cloud Function)](https://intl.cloud.tencent.com/document/product/583) to help users automatically purge their data cached on CDN edge servers. If you add a trigger rule to your bucket, then when you update files in the bucket, the SCF function provisioned by COS will be automatically triggered to purge your cached data.

> !
> - If you added a cache purging rule to your bucket in the COS console, the resulting purging function will also appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete this function; otherwise, your rule may not take effect.
> - All regions where SCF is available support CDN cache purging, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong, Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see the [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).
> - CDN cache purging may fail due to factors such as unstable network connection. In these cases, you can click **View Log** for the function you created in the COS console to open the SCF console where you can view the error log details for troubleshooting.
> - This feature depends on SCF which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF Product Pricing](https://intl.cloud.tencent.com/document/product/583/12281). The more often you use this feature, the more invocations you will consume in the free tier.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**. Select the bucket for which to add a CDN cache purging rule to open the bucket management page.
3. Click **Function Service**, and scroll down to the **CDN Cache Refresh Function** section.
![](https://main.qcloudimg.com/raw/b6618ad14cff7d6daf37520d78371cd2.png)
> !If you haven’t activated the SCF service, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and enable SCF service authorization as instructed.
4. Click **Add Function**, and configure the following in the pop-up window:
![](https://main.qcloudimg.com/raw/9881bbc4d5cf620c4cfac9060b061ce5.png)
	- **Function Name**: uniquely identifies a function, and cannot be modified after creation. You can view the function on the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
	-**Event Type**: an operation that triggers a function. Taking upload as an example, an upload may be performed by calling the [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) or [Post Object](https://intl.cloud.tencent.com/document/product/436/14690) API. If you select PUT as the Event Type, only uploads through the `PUT Object` API can trigger the function to purge your cache on CDN edge servers.
	-**Trigger Condition**: specifies the source file range for triggering the function. You can choose the whole bucket, or a range with a specified prefix or suffix. If you choose the latter, the rule only applies to the matched source files.
	-**Specified Domain**: specifies the CDN domain to cache.
	-**SCF Authorization**: CDN cache purging requires authorizing SCF to call the CDN API `PurgeUrlsCache`. In this way, SCF can replace your CDN cache with the latest data CDN pulls from the origin server on COS.
5. Click **Confirm** to add the function.
 - To view your CDN cache purging records, click **View Log**. 
 - To delete an unwanted CDN cache purging rule, click **Delete**.
