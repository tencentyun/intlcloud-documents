## Overview

Your self-built system can directly receive iPaaS alarm notifications through API callbacks. API callbacks can push alarm notifications to URLs that are accessible over the public network through GET requests. You can take further actions based on the alarm notifications you receive from API callbacks.

## Notes

- Currently, alarm callback does not have an authentication mechanism and does not support HTTP authentication.
- When a created alarm policy is triggered or the alarm is resolved, the alarm messages will be pushed through the API callbacks. API callbacks also support repeated alarms.


## Directions

1. Log in to the iPaaS console and select [**Alarm settings**](https://ipaas.tencentcloud.com/login) > **Notification templates**.
2. Click **Create** to enter the **Create notification template** page.
3. After configuring the basic information, enter a URL accessible over the public network as the callback API address (such as `domain name or IP[:port][/path]`) in the API callback module, and iPaaS will push alarm messages to this address promptly.
4. Enter the [alarm policy list](https://ipaas.tencentcloud.com/login), click the name of the target policy to enter the **Edit alarm policy** page, and click the notification template.
5. Alarm messages will be pushed to URLs that are accessible over the public network through GET requests.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e3923ed1c42655beebb357262da09548.png)
