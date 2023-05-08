## Overview

Tencent Push Notification Service provides you with a troubleshooting tool for message push exceptions such as message delivery or push failures. You can use this tool to troubleshoot issues on your own or query device details (including the bound accounts and tags) via an account or token.

## Use Cases

1. A developer successfully pushes a message to the testing device via the console, but this message is not displayed in the notification bar of the device. Using a token to query the device details detects that the notification bar is disabled. Enable it on the device, trigger registration again, and send a message to the device again. The message is now displayed in the notification bar.
2. An operator fails to push a message to a specified account. Using the account and bound account type to query the token in the troubleshooting tool detects that the account hasn't been associated with a token yet. Please submit a ticket to check whether the API for [Android](https://www.tencentcloud.com/document/product/1024/30715) or [iOS](https://www.tencentcloud.com/document/product/1024/30727#.E8.AE.BE.E7.BD.AE.E8.B4.A6.E5.8F.B7) was called to bind an account.
	![](https://qcloudimg.tencent-cloud.cn/raw/2c1559443566760e17b61c649e28b140.png)
3. After completing the Tencent Push Notification Service integration, a developer pushes a message to a certain batch of device tokens, but an online user reports that the push message hasn't been reported. Querying the obtained token and `pushID` of the user in the troubleshooting tool detects that the token is not in the push list.


## Directions

### Querying via an account

1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns).
2. In the left sidebar, choose **Message Management** > **Troubleshooting Tools**.
3. Select the product and application to be searched from the drop-down list, and select **Query by account** for the **Query Method**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/981819129693db6ff03842e68ca342a7.png)
4. Enter the user account and click **Query**.
5. Select the token associated with the account to view device details.
> ?
>- Account: Refers to the unique ID of the user bound to the token, including OpenID and UID.
>- Token list: Displays tokens in reverse chronological order by the binding time. A maximum of 10 tokens are listed in a page. If the account is bound to multiple devices, the message will be pushed to the last device bound to this account. To push the message to all devices bound to this account, change the push settings via the [console](https://console.cloud.tencent.com/tpns) or the [API](https://www.tencentcloud.com/document/product/1024/33764).

### Querying via a token

1. Select **Query through token** for the **Query Method** on the **Troubleshooting Tools** page.
2. Enter a token and click **Query**. You will see the device details on the right.
> ? 
> - Token: refers to the unique 36-character ID assigned to each device by Tencent Push Notification Service.
> - If you want to obtain the device token, depending on your device type, please see the [Android](https://www.tencentcloud.com/document/product/1024/30713) or [iOS](https://www.tencentcloud.com/document/product/1024/30726) SDK documentation.

### Push query

1. On the **Troubleshooting Tools** page, click the **Push Query** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/515c21d2a8d51ea56a3bbc2f73b510ef.png)
2. Enter the `pushid` (required) and the device token (required) to be queried, and click **Query** to view the troubleshooting results.
> ?Obtain `pushid` as follows:
> 1. Choose **Message Management** > **Task List** in the left sidebar to obtain the `PushID` to be queried.
> ![](https://qcloudimg.tencent-cloud.cn/raw/c470a99dabdce3d59f03ab677b440893.png)
> 2. Obtain it from the response parameter of the push API.
3. Choose **Message Management** > **Task List** in the left sidebar, and switch from **Created on Console** to **Create via API**. Then you can view API push data.
![](https://qcloudimg.tencent-cloud.cn/raw/f68e6a1e6382bbe7ec4449af95629e50.png)
4. If the query result does not match the actual situation, or the problem persists, you can view the [FAQs about push](#.E6.8E.A8.E9.80.81.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98) or [contact our online customer service](https://cloud.tencent.com/act/event/Online_service) with the `pushID` and token for assistance.

## FAQs

### Device query

1. In what situations will the device token expire?
   - The token is valid for 90 days. If the device hasn’t been connected to the Tencent Push Notification Service server for 90 consecutive days, the device will be considered unavailable.
   - If the application has been uninstalled from the device, the token will be considered as an invalid token.
2. I have enabled the notification bar, but why is “notification bar status: disabled” displayed in the device details?
After the notification bar is enabled, send the registration request from the client again to sync the notification bar status to the Tencent Push Notification Service server.

### Push

1. Push by account or tag fails but push by token succeeds. Why does this happen?
On the **Query device detail** page, verify that the token is associated with the target account or tag to implement push by account or tag.
2. The push message is in the completed status and the device is normal. Why can’t I receive the message on my mobile phone?
 - Check that you select the same environment for iOS and token. For more information, see [Push Environment Selection Description](https://www.tencentcloud.com/document/product/1024/34214).
 - Check whether you entered the same app package name as in the **[Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns)** > **Message Management** > **Basic Config**. If different, check whether the [Multi-Package Name Push](https://www.tencentcloud.com/document/product/1024/35393) feature is enabled.
 - If you’re using Android version P or later, add and use the Apache HTTP client library. To do this, add the following configuration to the AndroidManifest application node.
```
 <uses-library android:name="org.apache.http.legacy" android:required="false"/>
```
 - If you’re using a Mi phone, check whether the message is included in the ordinary notifications.
 - If you’re using a Meizu phone, check whether the message is included in the message box.
 - If you’re using a vivo phone, check whether the notification bar is manually enabled.
 - If you’re using a vivo or Huawei phone, check whether the notification banners and sounds are manually enabled.
 - Do not contain “test” and other sensitive words in your notifications because such notifications may be blocked by vendor channels.
 - Note that the vivo and OPPO push channels must be approved by vendors before being used.
