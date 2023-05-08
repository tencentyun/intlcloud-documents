## Overview

Currently, to avoid end users from being frequently disturbed, vendors are gradually restricting the number and frequency of notification messages pushed by application developers by type. The message type is mainly identified by the channel ID (`ChannelID`). Tencent Push Notification Service classifies messages into two types based on the types provided by major vendors:

- General message (default): This type is suitable for messages about group announcements, operational events, trending news, etc., which mainly contains user-oriented universal content.
- Notification message/private message: This type is suitable for personal notification-related messages such as chat messages, order status changes, and transaction reminders. The number of notification messages is unlimited.

The message type can be specified when you call the push API.
​Meizu currently does not support message classification or limit the number of messages.

#### Directions

1. If you need to use vendor notification messages, apply for or create a channel ID as instructed in the following sections:
	- [OPPO](#oppozhinan)
	- [Mi](#xiaomizhinan)
	- [vivo](#vivozhinan)
	- [Huawei](#huaweizhinan)
	- [HONOR](#rongyaozhinan)
>?From Android 8.0 (API level 26 or higher) on, to enable popping up notification bar notifications, you must first create notification channels for the application and assign channels for the notifications to pop up. Otherwise, notifications will not be displayed in the notification bar. By assigning a notification to a specific notification channel, the notification will be displayed in the notification bar as the enabled behavior feature for that notification channel. Instead of managing all of your application's notifications directly, you can implement personalized control over each of your application's notification channels, such as controlling the on/off, visual, and auditory options for each channel.
>You can configure multiple notification channels (up to seven as recommended) for an application. Each of the application's notification channels is distinguished by a notification channel ID (`channel_id`) and is displayed in the application's notification settings as the text defined by the notification channel name (`channel_name`).
>Once a notification channel is created, the device user has full control, and the developer cannot modify the notification behavior. For a duplicate code call for the same notification channel ID (`channel_id`), only the different notification channel name (`channel_name`) and channel description parameter will take effect, and other visual, auditory, and importance options will not be changed.
>

2. If you need to manage channels by vendor, customize channel IDs to classify messages based on your application's business message types. You can make vendor-based configurations as below:
<table>
<thead>
<tr>
<th>Push Channel</th>
<th>Configuration</th>
</tr>
</thead>
<tbody><tr>
<td>Tencent Push Notification Service channel</td>
<td><ul><li>On the application, call the channel ID creating API in the SDK for Android to create a channel ID.</li><li>Specify the corresponding channel ID (no limit) when calling the Tencent Push Notification Service <a href="https://www.tencentcloud.com/document/product/1024/33764">server API</a>.</li></ul></td>
</tr>
<tr>
<td>Huawei</td>
<td><ul><li><a href = "https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-0000001149358835#section1653845862216">Apply for the self-help message classification permission for an application</a> in the Huawei console. After the self-help message classification permission takes effect, the messages pushed by the application will be classified by the `hw_category` field.</li><li>Specify the `hw_category` parameter when calling the Tencent Push Notification Service <a href = "https://intl.cloud.tencent.com/document/product/1024/33764">server API</a>.</li><li>Huawei's ChannelID is used as a channel policy to customize the message notification mode and is not used to classify messages.</li></ul></td>
</tr>
<tr>
<td>Mi</td>
<td><ul><li>Create a channel ID in the Mi open platform console or through the corresponding Mi server API.</li><li>Specify the corresponding channel ID when calling the Tencent Push Notification Service <a href="https://intl.cloud.tencent.com/document/product/1024/33764">server API</a>.</li></td>
</tr>
<tr>
<td>OPPO</td>
<td><ul><li>On the application, call the SDK for Android to create a channel ID.</li><li>Register the same channel ID in the OPPO console.</li><li>Specify the corresponding channel ID when calling the Tencent Push Notification Service <a href="https://intl.cloud.tencent.com/document/product/1024/33764">server API</a>.</li></ul></td>
</tr>
<tr>
<td>Meizu</td>
<td>No instructions on channels are provided.</td>
</tr>
<tr>
<td>vivo</td>
<td><ul><li>You can configure using vivo system messages or operation messages but cannot customize the notification channel.</li><li>Specify the value of the `vivo_ch_id` parameter when calling the Tencent Push Notification Service <a href="https://intl.cloud.tencent.com/document/product/1024/33764">server API</a>.</li></ul></td>
</tr>
<tr>
<td>HONOR</td>
<td><ul><li>You can configure using HONOR "service and communication" or "information and marketing" messages but cannot customize the notification channel.</li><li>Specify the value of the `hw_importance` parameter when calling the Tencent Push Notification Service <a href="https://intl.cloud.tencent.com/document/product/1024/33764">server API</a>.</li></ul></td>
</tr>
</tbody></table>
3. If you need neither vendor notification messages nor a custom channel ID, Tencent Push Notification Service will specify a default channel ID for all messages of your application and group them into the default type.

## OPPO Notification Channel Application Guide[](id:oppozhinan)

### OPPO notification channel overview

The default channel on the OPPO PUSH platform is the public message channel. Now, the private message channel is provided to push personalized messages to individual users, with no limit on the number of pushes. The table below compares the public and private message channels.
<table>
<thead>
<tr>
<th colspan = "2">Type</th>
<th>Public Message Channel</th>
<th>Private Message Channel</th>
</tr>
</thead>
<tbody><tr>
<td colspan = "2">Push content</td>
<td>Universal content for users, for example, trending news, new product promotions, platform announcements, community topics, and lucky draws</td>
<td>Content closely related to individual users such as changes of orders, package delivery notifications, subscribed content updates, interactive comments, and loyalty program point updates</td>
</tr>
<tr>
<td rowspan = "2">Single user push limit (number of messages per day)</td>
<td>News (third-level category)</td>
<td>5</td>
<td>Unlimited</td>
</tr>
<tr>
<td>Other application types</td>
<td>2</td>
<td>Unlimited</td>
</tr>
<tr>
<td colspan = "2">Maximum number of pushes</td>
<td>All public message channels share a total number of pushes. If the daily limit is reached, they will stop pushing messages on the day. The current maximum number of daily pushes is twice the total number of all registered users.</td>
<td>Unlimited</td>
</tr>
<tr>
<td colspan = "2">Configuration method</td>
<td>Default</td>
<td>You need to register the channel with the OPPO PUSH platform and set the corresponding channel attribute to "Private Message"</td>
</tr>
</tbody></table>

>! Official reminder from OPPO: You must not use the private message channel to push universal messages (such as trending news and new product promotions). The backend will monitor the push content. If you violate the operational rules, OPush has the right to disable your private channel access, and you shall bear all consequences arising therefrom, such as exceptional API calls and failure to deliver messages sent through the private message channel.
>

### Applying for the OPPO private message channel
[](id:localtion)

1. Log in to the [OPPO PUSH platform](https://push.oppo.com) and choose **App Configuration** > **Create Channel** to create a channel. The channel ID and name are required and must be the same as those on the application client. Other configuration items are optional.
>! Once the channel ID is set, it cannot be randomly changed or deleted.
>
![](https://main.qcloudimg.com/raw/20c0242e7558cdfac1bd6d6a79f0a219.png)
2. Currently, the OPPO private message channel can take effect only after you apply for it through email. Please send an application email to the OPPO PUSH platform according to the following requirements. For more information, see [OPPO PUSH Channel Upgrade Beta Invitation](https://open.oppomobile.com/new/developmentDoc/info?id=11227).


### Using the OPPO private message channel

1. Create a notification channel for the client in either of the following ways:
	(1) Use the corresponding Android API to create a notification channel. For more information, see [Create and Manage Notification Channels](https://developer.android.google.cn/training/notify-user/channels).
	(2) Use the Tencent Push Notification Service SDK (v1.1.5.4 or above) to create a notification channel. For more information, see [Creating Notification Channel](https://www.tencentcloud.com/document/product/1024/30715).
2. Configure RESTful API push.
Set the `oppo_ch_id` parameter in the Android structure of the RESTful API request parameters to implement delivery based on the notification channel. For more information, see [Push API](https://www.tencentcloud.com/document/product/1024/33764).
>! Currently, notifications pushed through the OPPO private message channel can be delivered only through RESTful APIs but not the console.
>
Sample push:
<dx-codeblock>
:::  json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a1c2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
    "title": "Test title",
    "content": "Test content",
    "android": {
        "oppo_ch_id": "Private message channel ID"}
  }
}
:::
</dx-codeblock>

## Mi Notification Channel Application Guide[](id:xiaomizhinan)

### Mi notification channel overview 	

The notification channels of Mi Push are divided into two categories: "private message" and "public message". For more information, see [Mi Push Message Categorization Rules](https://dev.mi.com/distribute/doc/details?pId=1655)

- Public message channel: Suitable for pushing universal content for users, for example, trending news, new product promotions, platform announcements, community topics, and lucky draws.
- Private message channel: Suitable for personal notification-related content such as chat messages, order status changes, package delivery notifications, transaction reminders, and IoT system notifications. The number of pushes for notification messages is unlimited.
Mi Push uniformly manages the number of push messages and push rate (QPS). For more information, see [Mi Push Message Restrictions](https://dev.mi.com/distribute/doc/details?pId=1656#_2).

Restrictions on public and private messages are as follows:

<table>
<thead>
<tr>
<th>Message Type</th>
<th>Message Content</th>
<th>Message Quantity Limit</th>
<th>Application Method</th>
</tr>
</thead>
<tbody><tr>
<td>Default</td>
<td>See <a href="https://dev.mi.com/distribute/doc/details?pId=1655#_3">Public Message Scenario Description</a></td>
<td>1 message per application per device per day</td>
<td>No application needed</td>
</tr>
<tr>
<td>Public message</td>
<td>Universal content for users, for example, trending news, new product promotions, platform announcements, community topics, and lucky draws</td>
<td>5-8 messages per application per device per day</td>
<td rowspan="2">Apply on the Mi Push platform. For more information, see <a href="https://dev.mi.com/distribute/doc/details?pId=1655#_4">Channel Application and Access Methods</a>.</td>
</tr>
<tr>
<td>Private message</td>
<td>Personal notification-related content such as chat messages, order status changes, package delivery notifications, transaction reminders, and IoT system notifications</td>
<td>Unlimited</td>
</tr>
</tbody></table>

### Applying for a push volume increase for Mi Push

Log in to the Mi push operation platform and choose **Application Management** > **Notification Category** to apply for the Mi notification message channel. For more information, see [Mi Push Notification Message Channel](https://dev.mi.com/console/doc/detail?pId=2086#_0_1).

>!In order to use Mi Push in a compliant manner, be sure to abide by [Mi Push Operation Rules](https://dev.mi.com/distribute/doc/details?pId=1657).
>

### Using the Mi notification message channel

Currently, Mi notification messages can be delivered only through RESTful APIs but not the console.
Set the `xm_ch_id` parameter in the Android structure of the RESTful API request parameters to implement delivery based on the Mi notification channel. For more information, see the [push API parameter description](https://www.tencentcloud.com/document/product/1024/33764).
Sample push:

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
     "title": "Mi notification message",
     "content": "Test content",
     "android": {
        "xm_ch_id": "channel_id of the Mi notification message"
     }
	   }
}
```

<span id="vivozhinan"> </span>
## vivo System Message Channel Application Guide

### vivo message classification overview

vivo classifies push messages into operation messages and system messages.
To improve users' message notification experience and create a good push ecosystem, vivo push service will implement unified message management for different application categories from April 3, 2023. For more information, see [vivo push message restrictions](https://dev.vivo.com.cn/documentCenter/doc/695).

<table>
<thead>
<tr>
<th colspan = "2">Message Type</th>
<th>Application Category</th>
<th>Push Quantity Limit</th>
<th>Message Quantity Limit</th>
</tr>
</thead>
<tbody><tr>
<td colspan = "2">System message</td>
<td>/</td>
<td>Number of valid users with the notification bar enabled x 3
(You can apply for an unlimited limit via email.)</td>
<td>No limit</td>
</tr>
<tr>
<td  colspan = "2" rowspan = "2">Operation message</td>
<td>News
(With the Internet News Information Service License)</td>
<td>Number of valid users with the notification bar enabled x 3</td>
<td>5</td>
</tr>
<tr>
<td>Others</td>
<td>Number of valid users with the notification bar enabled x 2</td>
<td>2</td>	
</tr>
</tbody></table>

If the number of pushes exceeds the daily limit, error code 10070 (for operation messages) or 10073 (for system messages) is returned.

> ?
>1. Before June 1, 2020, no matter whether the message classification feature is enabled, the frequency control rule remains the same: up to 5 **public messages (full push, group push, tag push)** per application per user per day, and no limit on the number of messages per push. From June 1, 2020 on, the frequency control rule specifies that the upper limit for **operation messages** per application per user is 5, and if any user experience-related complaint arises, the number will be adjusted.
>2. Funtouch OS 10 or later does not provide a message box, and messages are displayed on the narrow bar when the application is not active.
>3. Both the system message quota and operation message quota will automatically change with the number of SDK subscriptions. If special circumstances require an increase in the system message quota, please submit an application as instructed in the next section.
>4. If a vivo user receives more than 5 operational messages a day, the extra messages beyond the limit (5 messages) are delivered through the Tencent Push Notification Service channel, instead of the vivo channel.
>5. If you have applied to vivo to increase the operating message limit, please contact us so that we can configure it on the backend; otherwise, the new limit will not take effect.
>

[](id:vivo_system)
### Applying for vivo system messages

The system message quota is three times the number of SDK subscriptions by default. To increase the [system message quota](https://dev.vivo.com.cn/documentCenter/doc/359), send an application email based on the template below to push@vivo.com:
```plaintext
Subject: Application for Increasing the Quota of Instant Messages/System Messages for App XXX
Body: …
Application name: …
Package name: …
Application overview: …
Instant Messages/System message quota required (unit: 10,000): ...
Specific push scenarios, such as personal user chat and merchant chat
```

### Using vivo system messages

Currently, vivo notification messages can be delivered only through RESTful APIs but not the console.
Set the `vivo_ch_id` parameter in the Android structure of the RESTful API request parameters to **1** to implement delivery of vivo system messages. For more information, see [Push API](https://www.tencentcloud.com/document/product/1024/33764).
>?
>- The vivo push platform will conduct daily inspection of system messages according to the message classification criteria. It checks whether developers send operation messages through the system message channel, and imposes corresponding penalties (may disable the message push feature in worst cases) based on the degree and frequency of violations.
>- Please refer to the [message classification](https://dev.vivo.com.cn/documentCenter/doc/359) document to operate strictly in accordance with the platform message classification. For the penalty rules, see Message Classification Feature Description > V. Operation Supervision and Penalty > 3. Penalty Rules in this document.

Sample push:

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
     "title": "vivo system notification",
     "content": "Test content",
     "android": {
        "vivo_ch_id": "1"
     }
   }
}
```

<span id="huaweizhinan"> </span>

## Huawei Message Classification User Guide

### Huawei message classification overview

Starting from EMUI 10.0, Huawei Push intelligently categorizes notification messages into two levels: "service and communication" and "information and marketing". Versions earlier than EMUI 10.0 don't categorize notification messages and have only one level, where all messages are displayed through the "default notification" channel, which is equivalent to the service and notification category on EMUI 10.0. From January 5, 2023 on, the number of information and marketing messages pushed per day will be capped according to the type of application, while there will be no limit to the number of service and communication messages pushed per day.
Huawei's response code 256 indicates that the number of information and marketing messages sent of the current day exceeds the limit, and you need to adjust the sending policy. For more information, see [here](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-restriction-description-0000001361648361?ha_source=hms5).
![](https://qcloudimg.tencent-cloud.cn/raw/8b5ded2fd11711c69227432e9eb0c571.png)

The table below compares the display style of messages at different levels.

| Message Level | Displayed in the Notification Center | Displayed in the Status Bar | Notification for Screen Lock | Ringtone | Vibration |
| -------- | ---------------- | -------------- | -------- | ---- | ---- |
| Service and communication     | Normal         | Supported           | Supported     | Supported | Supported |
| Information and marketing     | Normal         | Not supported             | Not supported       | Not supported   | Not supported   |

If you want service and notification messages to be sent silently, you can add the `hw_importance` field and specify its value as `1`. For more information, see the parameter description of [Push API](https://www.tencentcloud.com/document/product/1024/33764).

Classification rules:

- Intelligent message classification
Intelligent classification algorithms will automatically categorize your messages according to classification criteria based on multiple dimensional factors such as the content you send.
- Self-help message classification
Starting from July 1, 2021, the Huawei Push service will begin to receive developers' applications for self-help message classification. After their applications are approved, developers can classify messages by themselves according to Huawei Push's classification specifications.

### Applying for self-help message classification permission
The self-help classification permission for Huawei notification messages can take effect only after you apply for it. For more information, see [Message Classification Methods](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-0000001149358835#section1653845862216).

>!
> - If the application does not provide the self-help message classification feature, its push messages will be automatically classified by intelligent classification.
> - If the application provides the self-help message classification feature, the classification information provided by developers is trusted, and intelligent classification is not implemented for messages.
> 

### Using self-classified messages

Self-classified messages can be delivered only through APIs but not the console. After successfully obtaining the permission for self-help message classification, you can use the feature as follows:

Configure the `hw_category` field in the `Android` request structure of the RESTful API to deliver self-classified messages. For more information, see the parameter description in [Push API](https://www.tencentcloud.com/document/product/1024/33764).

Sample push:

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
        "title": "Account logged out:",
        "content": "Your account has been logged out due to login from an unusual login location.",
        "android": {
            "hw_category":"VOIP"
        }
    }
}
```

### Creating a Huawei notification channel

Huawei Push supports customizing notification channels for applications. To create a notification channel on the client, use either of the following methods:

1. Use the Android API to create a notification channel. For more information, see [Create and Manage Notification Channels](https://developer.android.google.cn/training/notify-user/channels).
2. Use the Tencent Push Notification Service SDK (version 1.1.5.4 or later). For more information, see [Creating a notification channel](https://www.tencentcloud.com/document/product/1024/30715) in the API Documentation.

### Using a Huawei notification channel

Currently, notifications pushed through Huawei's custom channel can be delivered only through a RESTful API but not the console. After a notification channel is created, you can:

Configure the `hw_ch_id` field in the Android request structure of the RESTful API to push messages through the Huawei notification channel. For more information, see the parameter description in [Push API](https://www.tencentcloud.com/document/product/1024/33764).

>! 
> - If you select China as the data processing location when you apply for the Huawei push service for your application in the Huawei push console, the custom channel feature is no longer applicable to your application. Your push messages will be classified as service and communication messages or information and marketing messages based on the message levels determined by the smart classification system or the self-help message classification permission. For more information, see [Notification Channel Customization](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/android-custom-chan-0000001050040122).
> - The custom channel feature requires the self-help message classification permission for your application. Please apply for it as instructed above.
>

Sample push:

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
        "title": "Huawei notification message",
        "content": "Test content",
        "android": {
            "hw_ch_id": "channel_id of the Huawei notification message"
        }
    }
}
```

[](id:rongyaozhinan)
## HONOR Message Classification User Guide

### HONOR message classification overview

According to the application type, message content, and message sending scenario, HONOR Push classifies push messages into "information and marketing" messages and "service and communication" messages. The number of "information and marketing" messages pushed per day will be capped according to the type of application, while there will be no limit to the number of "service and communication" messages pushed per day. For more information, see [here](https://developer.hihonor.com/cn/kitdoc?category=%E5%9F%BA%E7%A1%80%E6%9C%8D%E5%8A%A1&kitId=11002&navigation=guides&docId=notification-push-standards.md&token=).
You can manage the default display mode and message style for different message levels as follows:

| Message Level | Notification Bar Drop-down List Display | Icon Display | Notification for Screen Lock | Ringtone | Vibration |
| -------- | ---------------- | -------------- | -------- | ---- | ---- |
| Service and communication     | Normal         | Supported           | Supported     | Supported | Supported |
| Information and marketing     | Normal         | Not supported             | Not supported       | Not supported   | Not supported   |

- If the `importance` field is `1`, the message is an "information and marketing" message, its default display mode is silent notification, and it is displayed only in the notification bar drop-down list.
- If the `importance` field is `2`, the message is a "service and communication" message, and its default display modes are notification for screen lock and notification bar drop-down list display.

Classification rules:

- Intelligent message classification
Intelligent classification algorithms will automatically categorize your messages according to classification criteria based on multiple dimensions such as the application type and message content.
- Self-help message classification
Developers can classify messages by themselves according to message classification specifications.
Currently, the self-help message classification rule is adopted for all messages by default. HONOR Push will fully trust the classification results provided by developers and display the corresponding information. With the continuous complement and evolution of HONOR Push capabilities, the classification method will be gradually updated and upgraded. For more information, see [here](https://developer.hihonor.com/cn/kitdoc?category=%E5%9F%BA%E7%A1%80%E6%9C%8D%E5%8A%A1&kitId=11002&navigation=guides&docId=notification-class.md&token=).

>!Please comply with HONOR's push message classification rules. Violations will be punished by HONOR. For violations and corresponding penalties, see [here](https://developer.hihonor.com/cn/kitdoc?category=%E5%9F%BA%E7%A1%80%E6%9C%8D%E5%8A%A1&kitId=11002&navigation=guides&docId=notification-penalty-standards.md&token=).
> 

### Using self-classified messages

Self-classified messages can be delivered only through APIs but not the console. You can use the feature as follows:

Configure the `hw_importance` field in the `Android` request structure of the RESTful API to deliver self-classified messages. For more information, see the parameter description in [Push API](https://www.tencentcloud.com/document/product/1024/33764).

Sample push:

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
        "title": "HONOR：",
        "content": "Self-classified message",
        "android": {
            "hw_importance":2
        }
    }
}
```




