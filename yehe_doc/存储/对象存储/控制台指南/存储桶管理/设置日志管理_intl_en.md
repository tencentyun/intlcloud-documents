## Overview

You can log in to the COS console to enable log management for a bucket, which records various requests related to **bucket operations**. Log management facilitates buckets usage and management. For more information, see [Log Management Overview](https://intl.cloud.tencent.com/document/product/436/16920).

>!
>
>- Currently, COS offers the logging feature only in the Beijing, Shanghai, Guangzhou, Nanjing, Chongqing, Chengdu, Hong Kong (China), Singapore, Toronto, Silicon Valley, and Mumbai regions.
>- Currently, only the **bucket owner** has permission to set log management, and the **Log Management** configuration item will not be displayed to other users when they log in to the console. 
>- Log data is delivered once every 5 minutes. COS does not guarantee 100% accuracy of the log data. Such data is for reference only and does not serve as a basis for usage measurement and billing.

## Operation Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the source bucket that needs the log management enablement.
2. Choose **Log Management** -> **Log Storage** on the left, click **Edit**, and change the current status to "On".
   ![](https://main.qcloudimg.com/raw/242facfd32074aea52a7f694273a9086.png)
3. Configure the configuration items of log storage as follows:
 - **Destination Bucket**: the **source bucket** for which log management is enabled and the **destination bucket ** that stores the logs must be in the same region. COS does not recommend you use the source bucket itself as the destination bucket.
 - **Path Prefix**: enter a custom path prefix that makes it easy for you to find logs. If this field is left empty, it will default to the root path of the destination bucket.
 - **Service Authorization**: you need to authorize the CLS service to deliver access logs to your bucket.
   ![](https://main.qcloudimg.com/raw/d5fa347da09d92b5f757e32c910739e3.png)
4. After confirming that the entered information is correct, click **Save**. The log management feature is now enabled.
>?Log generation and delivery to the destination bucket may take several minutes or longer.
5. Find the destination bucket that you configured to store logs, and you can see the generated log files.
   ![](https://main.qcloudimg.com/raw/ef5f9cd836f3f50ee3e21fa58fc69baf.png)
6. After log files are downloaded, you can view log details in them. For the descriptions of the fields in the log files, see [Log Management Overview](https://intl.cloud.tencent.com/document/product/436/16920).


## Notes

1. To enable the log management feature, you need to create a log role in the CAM console and grant it read/write permission to the logs of the source bucket.
2. When the log management feature is disabled, if the role is not deleted, its read/write permission to the logs of the source bucket will not be revoked.
