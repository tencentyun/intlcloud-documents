## Overview

COS introduces the Logging feature to record **bucket operation** requests, facilitating bucket usage and management. You can enable it in the COS console. For more information, see [Logging Overview](https://intl.cloud.tencent.com/document/product/436/16920).

>!
> - Currently, COS offers the logging feature only in Beijing, Shanghai, Guangzhou, Nanjing, Chongqing, Chengdu, Hong Kong (China), Singapore, Seoul, Toronto, Silicon Valley, and Mumbai regions.
>- Currently, only the **bucket owner** has permission to set Logging, and other users cannot see the **Logging** configuration item in the console. 
>- Logs are delivered once every 5 minutes and are not 100% accurate. Therefore, they are for reference only and cannot be used for usage measurement and billing.
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the source bucket that you want to enable Logging for.
4. On the left sidebar, select **Logging** > **Logging**, click **Edit**, and toggle on the feature.
5. Configure the configuration items of Logging as follows:
![](https://main.qcloudimg.com/raw/d5fa347da09d92b5f757e32c910739e3.png)
 - **Destination Bucket**: The **destination bucket** that stores the source bucket's logs must reside in the same region as the source bucket. We recommend you not set the source bucket itself as the destination bucket.
 - **Path Prefix**: A custom path prefix for the logs. If this field is left empty, logs will be delivered to the root directory of the destination bucket.
 - **Service Authorization**: CLS needs to be authorized to deliver logs to your bucket.
6. After confirming that everything is correct, click **Save**.
>? It takes several minutes or longer for the logs to be generated and delivered to the destination bucket.
>
7. Go to the destination bucket configured to view the generated logs.
![](https://main.qcloudimg.com/raw/ef5f9cd836f3f50ee3e21fa58fc69baf.png)
8. After downloading the logs, you can view them in detail. For more information, see [Logging Overview](https://intl.cloud.tencent.com/document/product/436/16920).


## Notes

1. To enable Logging, you need to create a log role in the CAM console and grant the role permissions to read/write logs of the source bucket.
2. If Logging is disabled yet the role is not deleted, the role's read/write permissions on the source bucket's logs still exist.
