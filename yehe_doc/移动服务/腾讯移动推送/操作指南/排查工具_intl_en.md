## Introduction

TPNS provides you with a troubleshooting tool for message push exceptions such as message delivery or push failures. You can use this tool to query device details (including the associated accounts and tags) via an account or token.

## Use Cases

1. A developer successfully pushes a message to the testing device via the console, but this message is not displayed in the notification bar of the device. Using a token to query the device in the troubleshooting tool detects that the notification bar is disabled. Enable it and send a message to the device again. The message is now displayed in the notification bar.
2. An operator fails to push a message to a specified account. Using the account to query the token in the troubleshooting tool detects that the account hasn’t been associated with a token yet. Please submit a ticket to check whether the API for [Android](https://intl.cloud.tencent.com/document/product/1024/30715) or [iOS](https://intl.cloud.tencent.com/document/product/1024/30727) was called to bind an account.
![](https://main.qcloudimg.com/raw/867d6c62be726c6fb8af6ca4922ae16f.png)

## Directions

### Querying via an account

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Select **Toolbox** -> **Troubleshooting Tools** on the left sidebar.
3. Select the product and device from the drop-down list to be searched, and select **Query by account** for the **Query Method**.
![](https://main.qcloudimg.com/raw/ab3ee41ac3fcab0fe15b83b455a55d24.png)
4. Enter the user account and click **Query**.
5. Select the token associated with the account to view device details.
> ?
>- Account: refers to the unique ID of the user bound to the token, including OpenID and UID.
>- Token list: displays tokens in reverse chronological order by binding time. A maximum of 10 tokens are listed in a page. If the account is bound to multiple devices, the message will be pushed to the last device bound to this account. To push the message to all devices bound to this account, please change the push settings via the [console](https://console.cloud.tencent.com/tpns) or the [API](https://intl.cloud.tencent.com/document/product/1024/33764).

### Querying via a token

1. Select **Query through token** for the **Query Method** on the **Troubleshooting Tools** page.
2. Enter a token and click **Query**. You will see the device details on the right.
> ? 
>- Token: refers to the unique ID assigned to each device by TPNS. A token string cannot exceed 36 characters.
>- If you want to obtain the device token, depending on your device type, please see the [Android](https://intl.cloud.tencent.com/document/product/1024/30713) or [iOS](https://intl.cloud.tencent.com/document/product/1024/30726) SDK documentation.

## FAQs

1. In what situations will the device token expire?
A:
	- The token is valid for 90 days. If the device hasn’t been connected to the TPNS server for 90 consecutive days, the device will be considered as an unavailable device.
	- If the application has been unmounted from the device, the token will be considered as an invalid token.
2. I have enabled the notification bar, but why is “notification bar status: disabled” displayed in the device details?
After the notification bar is enabled, please send the registration request from the client again to sync the notification bar status to the TPNS server.
3. The account or tag push fails but the token push succeeds. Why does this happen?
On the **Query device detail** page, verify that the token has been associated with the target account or tag to implement the account or tag push.
4. The push message is in the completed status and the device is normal. Why can’t I receive the message on my mobile phone?
A:
	- Check that you selected the same environment for iOS and the token. For more information, see [Push Environment Selection Description](https://intl.cloud.tencent.com/document/product/1024/34214).
	- Verify whether you entered the exact application package name in the configuration management. If multiple package names are used, verify whether the [multi-package name push feature](https://intl.cloud.tencent.com/document/product/1024/35393) is enabled.
	- If you’re using Android version P or later, add and use the Apache HTTP client library. To do this, add the following configuration to the AndroidManifest application node.
		```
		<uses-library android:name="org.apache.http.legacy" android:required="false"/>
		```
	- If you’re using a Mi phone, check whether the message is included in the ordinary notifications.
	- If you’re using a Meizu phone, check whether the message is included in the message box.
	- If you’re using an OPPO phone, check whether the notification bar is manually enabled.
	- If you’re using a Vivo phone, check whether the notification bar and channel are manually enabled.
	- Do not contain “test” and other sensitive words in your notifications because such notifications may be blocked by vendor channels.
	- Please note that the Vivo and OPPO push channels must be approved by vendors before being used.
