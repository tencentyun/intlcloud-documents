## Overview
Currently, to avoid end users from being disturbed, vendors are gradually starting to limit the number and frequency of notification messages pushed by application developers by type. The message type is mainly identified by the channel ID (`ChannelID`). TPNS divides messages into two types based on the types provided by major vendors:
- General message (default): this type is suitable for messages about group announcements, operational events, trending news, etc., which is mainly user-oriented universal content.
- Notification message/private message: this type is suitable for personal notification-related messages such as chat messages, order status changes, and transaction reminders. The number of notification messages is unlimited.

The message type can be specified when you call the push API.

**Directions:**
1. If you need to use vendor notification messages, apply for the channel ID as instructed in the following documents:
   - [OPPO Application Guide](#oppozhinan)
   - [Mi Application Guide](#xiaomizhinan)
   - [Vivo Application Guide](#vivozhinan)

After you get the channel ID, specify it when calling the push API.
Meizu and Huawei channels do not support notification messages currently, and they don't limit the number of messages.
2. If you do not need to use notification/private messages of a vendor and only need a customized channel ID to group messages based on your application's business message types, you can configure the channel ID based on the corresponding vendor's configuration description:

| Push Channel | Configuration Description |
| --------    | -------  |
| TPNS    |   <li>On the application, call the channel ID creating API in the SDK for Android to create a channel ID </li><li>Specify the corresponding channel ID (no limit) when calling the TPNS [server API](https://intl.cloud.tencent.com/document/product/1024/33764).</li>|
| Huawei |   <li>On the application, call the channel ID creating API in the SDK for Android to create a channel ID </li><li>Specify the corresponding channel ID (no limit) when calling the TPNS [server API](https://intl.cloud.tencent.com/document/product/1024/33764). </li>  |
| Mi    | <li>Create a channel ID in the Mi Open Platform Console or through the corresponding Mi server API </li><li>Specify the corresponding channel ID when calling the TPNS server API. </li> |
| OPPO    |   <li>On the application, call the SDK for Android to create a channel ID </li><li>Register the same channel ID in the OPPO Console </li><li>Specify the corresponding channel ID when calling the TPNS server API. </li> |
| Meizu    | No instructions on channel are provided. |
| vivo   | <li>Call the server API to create the Channel ID .</li><li>If you want to specify the Channel ID, call  the TPNS [Push API](https://intl.cloud.tencent.com/document/product/1024/33764#android-.E6.99.AE.E9.80.9A.E6.B6.88.E6.81.AF).</li>| 

3. If you do not need notification messages of a vendor and customized channel ID, you do not need to perform relevant operations, and TPNS will specify a default channel ID for all messages of your application and group them into the default type.

<span id="oppozhinan"> </span>
## How to Apply for OPPO Notification Channel
### OPPO notification channel overview
The default channel on the Opush platform is the public message channel. Now, the "private message" channel is provided to push user personalized messages, with no limit on the number of pushes. The comparison between "public message" and "private message" is as follows:

| Type | Public Message | Private Message |
| -------- | ---------------- | ------------ |
| Push content | Universal content for multiple users such as trending news, new product promotions, platform announcements, community topics, and lucky draws. | Content closely related to individual users such as changes of orders, package delivery notifications, subscribed content updates, interactive comments, and loyalty program point updates. |
| Push object | Multiple users (single user is also allowed). | Only single user. |
| Maximum number of pushes | All public message channels share a total number of pushes; if the daily limit is reached, they will stop pushing messages on the day. The current maximum number of daily pushes is the total number of all registered users * 2. | Unlimited. |
| Configuration method | Default. | You need to register the channel with the Opush platform and set the corresponding channel attribute to "Private Message". |

>Official reminder from OPPO: you must not use the private message channel to push universal messages (such as trending news and new product promotions), as the backend will monitor the push content, and if you violate the operational rules, Opush has the right to disable your private channel access, and all consequences arising therefrom, such as exceptional API calls and delivery failures of messages sent through the private message channel shall be borne by you.

### Application for OPPO private message channel
1. Log in to the [Opush platform](https://push.oppo.com) and select **App Configuration** > **Create Channel** to create a channel. The channel ID and name are required and must be the same as those on the application client. Other configuration items are optional.
>Once the channel ID is set, it cannot be randomly changed or deleted.

2. Currently, the OPPO private message channel can take effect only after you apply for it through email. Please send an application email to Opush according to the following requirements. For more information, please see [Opush Channel Upgrade Beta Invitation](https://open.oppomobile.com/wiki/doc#id=10614).
```
Standard for applying for the public/private message beta eligibility: total number of users for Opush ≥ 300,000
Application method: send an email to push@oppo.com for application. You can use the following email template:
Application ID: XXX
Application name: XXX
Total number of users: XXX
Dedicated private channel name:
Dedicated private channel ID:
WeChat account of business contact:
I apply for connection to the Opush beta public/private message service for the XX application. I undertake to comply with the operational rules and will not use the private message channel to push any marketing messages.
```

### Using OPPO private message channel
1. Create a notification channel for the client in either of the following ways:
(1). Use the corresponding Android API to create a notification channel. For more information, please see [Create and Manage Notification Channels](https://developer.android.google.cn/training/notify-user/channels).
(2). Use the TPNS SDK (v1.1.5.4 or above) to create a notification channel. For more information, please see [Creating Notification Channel](https://intl.cloud.tencent.com/document/product/1024/30715).
2. Configure RESTful API push.
Set the `oppo_ch_id` parameter in the Android structure of the RESTful API request parameters so as to implement delivery based on notification channel. For more information, please see [Push API Parameter Description](https://intl.cloud.tencent.com/document/product/1024/33764).
>Currently, notifications pushed through the OPPO private message channel can be delivered only through RESTful APIs but not the console.

Below is a sample push:

```
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
```

<span id="xiaomizhinan"> </span>
## How to Apply for Mi Notification Channel
### Mi notification channel overview
Mi Push notification channels can be divided into "general messages" (default) and "notification messages".
- General message (default): this type is suitable for messages about trending news, new product promotions, platform announcements, community topics, and lucky draws, which is mainly user-oriented universal content.
- Notification message: this type is suitable for personal notification-related messages such as chat messages, order status changes, package delivery notifications, transaction reminders. and IOT system notifications. The number of notification messages is unlimited.

Notes on general and notification message limits:

| Type | General Message (Default) | Notification Message |
| -------- | ---------------- | ------------ |
| Push content | Universal content for multiple users such as trending news, new product promotions, platform announcements, community topics, and lucky draws. | Personal notification-related content such as chat messages, order status changes, package delivery notifications, transaction reminders, and IoT system notifications. |
| Limit on the number of pushes | <li>If the number of daily connected MIUI devices is below 10,000, the number of allowed pushes on the day will be 50,000 <li>If the number of daily connected MIUI devices is greater than or equal to 10,000, the number of allowed pushes on the day will be 5 times the number of daily connected MIUI devices<li>Note: the number of messages arrived at devices is counted as the number of pushes</li> | Unlimited.  |
| Configuration method | Default. | You need to apply to the Mi Push team for a channel of the desired message type, which will be enabled after your application is approved (for more information on the application method, please see the section below). |

### Applying for Mi notification message
Currently, you need to send an email to Mi's official team at mipush-permission@xiaomi.com to apply for the permission of sending notification messages to Mi devices. The email needs to contain the following content:
```
1. Email subject: Notification Message Permission Application - XX Company
2. Email body template: 
I apply for connection to the Mi Push notification message channel for the XX application. I undertake to comply with the operational rules and will not use the notification message channel to push any general messages.
Name of your application and corresponding `AppId` on Mi Push.
Notification message categories that are applied for, use cases, and application reasons.
You can apply for the following categories as needed:
A. Personal status changes
B. Personal resource changes
C. IM messages
D. Personal order status changes
E. Personal agenda reminders
F. Reminders for subscribed content updates
G. Personal transaction reminders
H. Personal family reminders
3. Estimated ratio of notification messages to general messages.
4. Sample notification message. If you apply for multiple categories, provide at least one sample for each category. You can use a previously sent message as a sample and specify the `messageID`.
5. Contact information (such as email).
```

Sample notification messages:

| Message Category | messageID | Title | Content |
| -------- | ---------------- | ------------ |-----|
| Personal family IoT reminder | xxxxxxxx | Mi Home smart camera_master bedroom  | Someone moved at 23:59 in the protected zone. |
| Personal transaction reminder | xxxxxxxx | Fund transaction reminder | Your application for purchasing xx USD of the xx fund has been submitted. |

>a. The operational team of Mi Push will reply to you with the review result in 5 business days.
>b. If your application is approved, you need to send the name that you want to display (on clients) for the channel to Mi as required. Then, the Mi Push team will create the channel of the corresponding notification message category (you cannot create it by yourself) and provide you with the `channel_id`.

### Using Mi Notification Message
Currently, Mi notification messages can be delivered only through RESTful APIs but not the console.
Set the `xm_ch_id` parameter in the Android structure of the RESTful API request parameters so as to implement delivery based on the Mi notification channel. For more information, please see the parameter description of the [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
Below is a sample push:
``` json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
    "title": "Mi notification message",
    "content": "Test content",
    "android": {
        "xm_ch_id": "channel_id of Mi notification message"
  }
}
```
<span id="vivozhinan"> </span>
## How to Apply for Vivo System Message
### Vivo message categorization overview
The Vivo message categorization feature divides push messages into operation messages and system messages.

| Message Category | Quota | Notification Bar Message Display | Frequency Control Rule After June 1, 2020 |
| -------- | ---------------- | ------------ |-----|
| Operation message | Number of SDK subscriptions * 2 | Collapsed when the application is not active and displayed when the application is active | The maximum number of messages one user can receive from one application per day is 5. |
| System messages | Number of SDK subscriptions *2 | Displayed no matter whether the application is active | An unlimited number of messages can be received. |

>
>1. Before June 1, 2020, no matter whether the message categorization feature is enabled, the frequency control rule remains the same, and the daily upper limit for "public messages (full push, group push, tag push)" per application per user is 5, while the number of messages for single push is unlimited. From June 1, 2020 on, the frequency control rule specifies that the upper limit for "operation messages" per application per user is 5, and if any user experience-related complaint is raised, the number will be adjusted accordingly.
>2. There is no message box on Funtouch OS 10 and above, so messages will be displayed on the narrow bar when the application is not active.
>3. Both the system message quota and operation message quota will automatically change with the number of SDK subscriptions. If special circumstances require an increase in the system message quota, please submit an application as instructed in **Vivo system message application** below.

### Vivo system message application
1. System messages can only be created through the Vivo server API but not on the Vivo web operation platform. The API has a new request field ```classification```, where "0" indicates operation message and "1" indicates system message. If the parameter is left empty, 0 will be used by default. For more information, please see the [Vivo server API documentation](https://dev.vivo.com.cn/documentCenter/doc/362).
2. The upper limit for system message volume is the number of SDK subscriptions * 2 by default. When the system message quota is insufficient, you can send an email to push@vivo.com to apply for increasing the quota as described in the template below:
```
Subject: Application for Increasing the Quota of IM/System Messages for App XXX
Body: ...
Application name: ...
Package name: ...
Application overview: ...
IM/system message volume required (in 10,000 messages): ...
Description of specific push scenario: such as personal user chat and merchant chat
```

### Vivo system message usage
Currently, Mi notification messages can be delivered only through RESTful APIs but not the console.
Set the `vivo_ch_id` parameter in the Android structure of the RESTful API request parameters to "1" so as to implement delivery of Vivo system messages. For more information, please see the parameter description of the [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
Below is a sample push:

``` json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
    "title": "Vivo system notification",
    "content": "Test content",
    "android": {
        "vivo_ch_id": "1"
  }
}
```
