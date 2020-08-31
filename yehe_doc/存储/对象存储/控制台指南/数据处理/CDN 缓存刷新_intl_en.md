## Overview

CDN cache purging is a Tencent Cloud COS feature based on [SCF](https://intl.cloud.tencent.com/document/product/583) to help users automatically purge their data cached on CDN edge servers. If you add a trigger rule to your bucket, then when you update files in the bucket, the SCF function provisioned by COS will be automatically triggered to purge your cached data.

> !
> - If you added a cache purging rule to your bucket in the COS Console, the resulting purging function will also appear in the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete this function; otherwise, your rule may not take effect.
> - All regions where SCF has been available support CDN cache purging, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong, Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see the [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).
> - CDN cache purging may fail due to factors such as unstable network connection. In these cases, you can click **View Log** for the function you created in the COS console to open the SCF console where you can view the error log details for troubleshooting.
> - This feature depends on SCF which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF Product Pricing](https://intl.cloud.tencent.com/document/product/583/12281). The more often you use this feature, the more invocations you will consume in the free tier.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**. Select the bucket for which to add a CDN cache purging rule to open the bucket management page.
3. Click **Function Service**, and scroll down to the **CDN Cache Refresh Function** section.
![](https://main.qcloudimg.com/raw/b6618ad14cff7d6daf37520d78371cd2.png)
> !If you haven’t activated the SCF service, you can do so by using the [SCF Console](https://console.cloud.tencent.com/scf), and enable SCF service authorization as instructed.
4. Click **Add Function**, and configure the following in the pop-up window:
	- **Function Name**: uniquely identifies a function, and cannot be modified after creation. You can view the function from the [SCF](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) console.
	- **Event Type**: an operation that triggers the function. Taking upload as an example, an upload may be performed by calling the [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) or [Post Object](https://intl.cloud.tencent.com/document/product/436/14690) API. If you select PUT for Event Type, only uploads through the `PUT Object` API can trigger the function to purge your cache on CDN edge servers.
        - **Trigger Condition**: specifies the scope of file sources the trigger event applies to, e.g. the whole bucket, or only those matching a specified prefix or suffix. 
	- **Specified Domain**: specifies the CDN domain to cache.
	- **SCF Authorization**: CDN cache purging requires authorizing SCF to call the CDN API `PurgeUrlsCache`. In this way, SCF can replace your CDN cache with the latest data CDN pulls from the origin server on COS.
![](https://main.qcloudimg.com/raw/9881bbc4d5cf620c4cfac9060b061ce5.png)
5. Click **OK** to add the function.
6. You can view your CDN cache purging records by clicking **View Log**. To delete an unwanted CDN cache purging rule, simply click **Delete**.
