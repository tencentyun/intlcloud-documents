When you push messages, if your users have disabled notifications on their mobile devices, the messages will be unable to reach them. After you enable supplementary in-app message push, push messages will be displayed in the form of in-app banners for higher reach rate when the app is running in the foreground, so that your users will not miss important notifications.

## Use Cases
An operator of a credit card app wants to send an important app push message to user W, notifying the user that a repayment will be overdue soon. But user W has disabled notifications for the app and thus cannot receive app push messages. In this case, the operator can enable supplementary in-app message push, so that the message can be displayed to user W as an in-app message when user W opens the app.
![]()

## Prerequisites

### Allowing in-app message display on Android terminals

1. In the `build.gradle` file under the app directory, add the following dependency:
```
implementation 'com.tencent.tpns:tpns-inmsg:[version]-release' // `[version]` is the SDK version number, which can be found in the release notes of SDK for Android.
```
2. Call the SDK API to enable in-app message display. Below is the sample code:
```
XGPushConfig.enableShowInMsg(context, true);
```

>! In-app message display on an Android terminals depends on the WebView framework. Make sure to configure WebView data directories; otherwise, your app may crash. For more information, see the **In-App Message Display** section of [API Documentation](https://intl.cloud.tencent.com/document/product/1024/30715).
>


### Allowing in-app message display on iOS terminals

The SDK for iOS allows in-app message display by default. For more information about in-app message settings, see [API Documentation](https://intl.cloud.tencent.com/document/product/1024/30727).


## Description

### Using the console

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. On the left sidebar, select **Message Management** > **Task List** to go to the task management page
3. Click **Create Push** and enable **Supplementary In-App Message Push**.
![]()
>? 
> - After this feature is enabled, for users with app notifications disabled, push messages will be displayed in the form of in-app banners for higher reach rate when the app is running in the foreground.
> - This setting applies to this push task (push_id) only.
> 

### Using RESTful APIs

When calling RESTful APIs, you can set the `supply_inapp_msg` parameter to `true` to implement supplementary in-app message push. For more information, see [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
Below is a sample push:
```
{
   "audience_type": "all",
    "message_type": "notify",
		 "supply_inapp_msg": true 
    "message": {
        "title": "Important notes",
        "content": "July 1 is your repayment date. Please make your payment on time.",
        "android": {
        	 "custom_content":"{\"key\":\"value\"}"
        }
    }
}
```


### Viewing supplementary push data

After enabling supplementary in-app message push, you can go to **Task List** ＞ **Learn More** ＞ **Supplementary Message Push** to view the data of supplementary push.
![]()

#### Metrics

**Attempted**: the number of devices that you plan to send the message in the push task to via in-app messaging, without deduplication
**Sent To**: the number of devices that the message in the push task is sent to via in-app messaging, without deduplication
**Reached**: the number of devices that the message in the push task is sent to and reaches via in-app messaging, without deduplication
**Reach Rate**: Reached/Sent To x 100%
**Impressions**: the number of times that the message in the push task is sent and shown to users via in-app messaging, without deduplication
**Clicked**: the number of times the message in the push task is shown to and clicked by users via in-app messaging, without deduplication
**Click Rate**: Clicked/Impressions x 100%
**Reach Growth Rate**: Reached of supplementary in-app message push/Reached of push x 100%
>?Description of **Reach Growth Rate**: for example, when supplementary in-app message push is not enabled for a push task, the number of devices that the message reaches via app push is merely 2000; when supplementary in-app message push is enabled for the push task, the number of devices that the message reaches via app push is 2000 and that via in-app messaging is 1000, then the total number of devices that the message reaches in the push task is 3000, which means that there is a 50% increase.
>



