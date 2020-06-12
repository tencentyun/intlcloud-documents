## Overview
You can log in to the COS Console to enable logging for a bucket so that COS logs various requests related to **bucket operations**. This feature can help you use and manage your buckets better. For more information, see [Logging Overview](https://intl.cloud.tencent.com/document/product/436/16920).

>
>- Currently, COS logging is available in Beijing, Shanghai, Guangzhou, Chengdu, and Toronto regions.
>- Currently, only the **bucket owner** has permission to set logging, with the **Logging* panel invisible to other users in the console. 
>- Logs are shipped every 5 minutes. As COS doesn’t guarantee logs are 100% correct, they are for reference only, and cannot serve as a basis for billing.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and then the bucket for which to enable logging.
![](https://main.qcloudimg.com/raw/2cb54182f933fe1dce75e2199a301bd0.png)
2. Select the **Advanced Configuration** tab, find the **Logging** section, and click **Edit**.
![](https://main.qcloudimg.com/raw/242facfd32074aea52a7f694273a9086.png)
3. Toggle on the **Status** button to begin the configuration.
![](https://main.qcloudimg.com/raw/4f3a62cbc636be16254547a271204096.png)
4. Configure the log shipping information as follows:
 - **Destination Bucket**: the **source bucket ** for which logging is enabled and the **destination bucket ** that stores the logs must be in the same region. It is not recommended to use the source bucket itself as the destination bucket.
 - **Target prefix**: a custom path prefix for easy log search. If not specified, it defaults to the root path of the destination bucket.
 - **Service Authorization**: you need to authorize the CLS service to ship logs to your bucket.
![](https://main.qcloudimg.com/raw/d5fa347da09d92b5f757e32c910739e3.png)
5. Click **Save** to enable logging.
>Note that it may take minutes or longer to ship logs to your destination bucket.
6. Now, you can view your logs in the destination bucket you configured to save logs.
![](https://main.qcloudimg.com/raw/ef5f9cd836f3f50ee3e21fa58fc69baf.png)

## Notes
1. To enable logging, you need to create a log role in the CAM Console, and grant it read/write permission on the logs in the destination bucket.
2. When logging is disabled, if the log role is not deleted, its read/write permission on the logs in the destination bucket will not be revoked.
