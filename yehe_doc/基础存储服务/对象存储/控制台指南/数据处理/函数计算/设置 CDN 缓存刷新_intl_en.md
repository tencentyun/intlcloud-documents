## Overview

CDN cache purge is a data purge feature provided by COS based on the [SCF](https://www.tencentcloud.com/document/product/583) service. It can automatically purge the data cached on CDN edge nodes. After you add a trigger rule for a bucket, when a file is updated to the bucket, the SCF function preconfigured by COS will be automatically triggered to purge the cached data.

> !
> - If you added a cache purge rule for your bucket in the COS console, the resulting purge function will also appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **Do not** delete this function; otherwise, your rule may not take effect.
> - Regions where SCF is available support CDN cache purge, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see [Serverless Cloud Function](https://www.tencentcloud.com/document/product/583).
> - CDN cache purge may fail due to factors such as unstable network connection. In these cases, you can click **View Log** for the function created in the COS console to enter the SCF console and view the error log details for troubleshooting.
> - The CDN cache purge feature depends on the SCF service, which provides a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). Excessive usage will be billed at SCF prices. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281). For this feature, the more often you purge the cache, the more invocations you will need to use.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar and click the name of the target bucket.
3. Click **Function Service** > **CDN Cache Purge Function** on the left sidebar.
![](https://main.qcloudimg.com/raw/b6618ad14cff7d6daf37520d78371cd2.png)
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
4. Click **Add Function** and configure the following in the pop-up window:
![](https://main.qcloudimg.com/raw/9881bbc4d5cf620c4cfac9060b061ce5.png)
	- **Function Name**: It uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
	- **Event Type**: An event is an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) or [Post Object](https://intl.cloud.tencent.com/document/product/436/14690) API. If you select `PUT` as the event type, only uploads through the `PUT Object` API can trigger the function to purge the cache on CDN edge nodes.
	- **Trigger Condition**: You can specify the file source scope of the triggered files, such as all buckets, specified prefix, or specified suffix. After you specify a prefix or suffix, the rule only applies to the matched file sources.
	-**Specified Domain**: Specify the CDN domain name to be purged.
	-**SCF Authorization**: CDN cache purge requires authorizing SCF to call the CDN API `PurgeUrlsCache`. In this way, SCF can replace your CDN cache with the latest data CDN pulls from the COS origin.
5. Click **Confirm**.
 - Click **Log** to view the historical operations of CDN cache purge.
 - Click **Delete** to delete an unwanted CDN cache purge rule.
