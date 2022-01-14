## Overview

Currently, to avoid end users from being frequently disturbed, vendors are gradually starting to limit the number and frequency of notification messages pushed by application developers by type. The message type is mainly identified by the channel ID (`ChannelID`). TPNS divides messages into two types based on the types provided by major vendors:

- General message (default): this type is suitable for messages about group announcements, operational events, trending news, etc., which is mainly user-oriented universal content.
- Notification message/private message: this type is suitable for personal notification-related messages such as chat messages, order status changes, and transaction reminders. The number of notification messages is unlimited.

The message type can be specified when you call the push API.

#### Directions

1. If you need to use vendor notification messages, apply for or create a channel ID as instructed in the following sections:
	- [OPPO](#oppozhinan)
	- [Mi](#xiaomizhinan)
	- [vivo](#vivozhinan)
	- [Huawei](#huaweizhinan)
	

 After you get the channel ID, specify it when calling the push API. Meizu and Huawei channels do not support notification messages currently, and they don't limit the number of messages.
2. If you do not need to use vendor notification/private messages and only need a custom channel ID to group messages based on your application's business message types, you can configure the channel ID based on the corresponding vendor's configuration description:
<table>
<thead>
<tr>
<th>Push Channel</th>
<th>Configuration Description</th>
</tr>
</thead>
<tbody><tr>
<td>TPNS</td>
<td><ul><li>On the application, call the channel ID creating API in the SDK for Android to create a channel ID.</li><li>Specify the corresponding channel ID (no limit) when calling the TPNS <a href="https://intl.cloud.tencent.com/document/product/1024/33764">server API</a>.</li></ul></td>
</tr>
<tr>
<td>Huawei</td>
<td><ul><li>On the application, call the channel ID creating API in the SDK for Android to create a channel ID.</li><li>Specify the corresponding channel ID (no limit) when calling the TPNS <a href="https://intl.cloud.tencent.com/document/product/1024/33764">server API</a>.</li></ul></td>
</tr>
<tr>
<td>Mi</td>
<td><ul><li>Create a channel ID in the Mi open platform console or through the corresponding Mi server API.</li><li>Specify the corresponding channel ID when calling the TPNS server API. </li></td>
</tr>
<tr>
<td>OPPO</td>
<td><ul><li>On the application, call the SDK for Android to create a channel ID.</li><li>Register the same channel ID in the OPPO console.</li><li>Specify the corresponding channel ID when calling the TPNS server API.</li></ul></td>
</tr>
<tr>
<td>Meizu</td>
<td>No instructions on channels are provided.</td>
</tr>
<tr>
<td>vivo</td>
<td><ul><li>Call the server API to create the channel ID.</li><li>Specify the corresponding channel ID when calling the TPNS <a href="https://intl.cloud.tencent.com/document/product/1024/33764">server API</a>.</li></ul></td>
</tr>
</tbody></table>
3. If you do not need vendor notification messages nor a custom channel ID, you do not need to perform relevant operations, and TPNS will specify a default channel ID for all messages of your application and group them into the default type.

## OPPO Notification Channel Application Guide[](id:oppozhinan)

### OPPO notification channel overview

The default channel on the OPPO PUSH platform is the public message channel. Now, the private message channel is provided to push personalized messages to individual users, with no limit on the number of pushes. The table below compares the public and private message channels.

| Type | Public Message Channel | Private Message Channel |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Push content | Universal content for multiple users, for example, trending news, new product promotions, platform announcements, community topics, and lucky draws | Content closely related to individual users such as changes of orders, package delivery notifications, subscribed content updates, interactive comments, and loyalty program point updates |
| Push object | Multiple users (single user is also allowed) | Only single user |
| Maximum number of pushes | All public message channels share a total number of pushes; if the daily limit is reached, they will stop pushing messages on the day. The current maximum number of daily pushes is twice the total number of all registered users | Unlimited |
| Configuration method | Default | You need to register the channel with the OPPO PUSH platform and set the corresponding channel attribute to **Private Message** |

>! Official reminder from OPPO: you must not use the private message channel to push universal messages (such as trending news and new product promotions). The backend will monitor the push content, and if you violate the operational rules, Opush has the right to disable your private channel access, and all consequences arising therefrom, such as exceptional API calls and delivery failures of messages sent through the private message channel, shall be borne by you.
>

### Applying for the OPPO private message channel

1. Log in to the [OPPO PUSH platform](https://push.oppo.com) and choose **App Configuration** > **Create Channel** to create a channel. The channel ID and name are required and must be the same as those on the application client. Other configuration items are optional.
>! Once the channel ID is set, it cannot be randomly changed or deleted.
>
![]()
2. Currently, the OPPO private message channel can take effect only after you apply for it through email. Please send an application email to the OPPO PUSH platform according to the following requirements. For more information, see [OPPO PUSH Channel Upgrade Beta Invitation](https://open.oppomobile.com/wiki/doc#id=11096).


### Using the OPPO private message channel

1. Create a notification channel for the client in either of the following ways:
	(1) Use the corresponding Android API to create a notification channel. For more information, see [Create and Manage Notification Channels](https://developer.android.google.cn/training/notify-user/channels).
	(2) Use the TPNS SDK (v1.1.5.4 or above) to create a notification channel. For more information, see [Creating Notification Channel](https://intl.cloud.tencent.com/document/product/1024/30715).
2. Configure RESTful API push.
Set the `oppo_ch_id` parameter in the Android structure of the RESTful API request parameters to implement delivery based on the notification channel. For more information, see [push API parameter description](https://intl.cloud.tencent.com/document/product/1024/33764).
>! Currently, notifications pushed through the OPPO private message channel can be delivered only through RESTful APIs but not the console.
>
Below is a sample push:
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

Mi push notification channels are classified into two types:

- General message channel (default): suitable for pushing universal content for users, for example, trending news, new product promotions, platform announcements, community topics, and lucky draws.
- Notification message channel: suitable for personal notification-related content such as chat messages, order status changes, package delivery notifications, transaction reminders, and IoT system notifications. The number of pushes for notification messages is unlimited.

The table below compares the general message channel and notification message channel.

| Type         | General Message Channel (Default)                                             | Notification Message Channel                                                     |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Push content     | Universal content for multiple users, for example, trending news, new product promotions, platform announcements, community topics, and lucky draws | Personal notification-related content such as chat messages, order status changes, package delivery notifications, transaction reminders, and IoT system notifications |
| Limit on the number of pushes | <li>If the number of daily connected MIUI devices is less than 10,000, the number of allowed pushes on the day will be 50,000. <li>If the number of daily connected MIUI devices is greater than or equal to 10,000, the number of allowed pushes on the day will be 5 times the number of daily connected MIUI devices. <li>Note: the number of messages arrived at devices is counted as the number of pushes.</li> | Unlimited |
| Configuration method     | Default                                                       | You need to apply to the Mi push team for a channel of the desired message type, which will be enabled after your application is approved (for more information on the application method, see the section below). |

### Applying for the Mi notification message channel

Log in to the Mi push operation platform and choose **Application Management** > **Notification Category** to apply for the Mi notification message channel. For more information, see [Mi Push Notification Message Channel](https://dev.mi.com/console/doc/detail?pId=2086#_0_1).

### Using the Mi notification message channel

Currently, Mi notification messages can be delivered only through RESTful APIs but not the console.
Set the `xm_ch_id` parameter in the Android structure of the RESTful API request parameters to implement delivery based on the Mi notification channel. For more information, see [push API parameter description](https://intl.cloud.tencent.com/document/product/1024/33764).
Below is a sample push:

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

| Message Category | Quota         | Supported Message Content |    How to Increase Quota | Notification Bar Message Display                   | Frequency Control Rule After June 1, 2020            |
| -------- | ------------ | ------------ | --------- | -------------------------------- | --------------------------------- |
| Operation message | Number of SDK subscriptions x 2 |  In addition to system messages, you can send notifications of content recommendations, event recommendations, social networking status updates, etc. For details, see [vivo message classification](https://dev.vivo.com.cn/documentCenter/doc/359). |  Contact vivo sales personnel. | Collapsed when the application is not active and displayed when the application is active | Up to 5 messages per application per user per day |
| System message | Number of SDK subscriptions x 2 |<li>Instant message</li><li>Email</li><li>Reminder set by user</li><li>Logistics</li><li>Order</li><li>To-do/To-read</li><li>Finance</li><li>Feature reminder</li>For details, see [message classification scenario description](https://dev.vivo.com.cn/documentCenter/doc/359). | Send an email to apply for quota increase. See below for the application template and requirements.   | Displayed regardless of whether the application is active           | No limit on the number of messages received by users                     |

> ?
>1. Before June 1, 2020, no matter whether the message classification feature is enabled, the frequency control rule remains the same: up to 5 **public messages (full push, group push, tag push)** per application per user per day, and no limit on the number of messages per push. From June 1, 2020 on, the frequency control rule specifies that the upper limit for **operation messages** per application per user is 5, and if any user experience-related complaint arises, the number will be adjusted.
>2. Funtouch OS 10 or above does not provide a message box, and messages are displayed on the narrow bar when the application is not active.
>3. Both the system message quota and operation message quota will automatically change with the number of SDK subscriptions. If special circumstances require an increase in the system message quota, please submit an application as instructed in the next section.
>4. If a vivo user receives more than 5 operational messages a day, the extra messages beyond the limit (5 messages) are delivered through the TPNS channel, instead of the vivo channel.
>5. If you have applied to vivo to increase the operating message limit, please contact us so that we can configure it on the backend; otherwise, the new limit will not take effect.
>


### Applying for vivo system messages
[](id:vivo_system)
1. System messages can be created only through vivo server APIs but not on the vivo web operation platform. The API has a new request field `classification`, where **0** indicates operation message and **1** indicates system message. If the field is left empty, **0** will be used by default. For more information, see the [vivo server API documentation](https://dev.vivo.com.cn/documentCenter/doc/362).
2. The system message quota is twice the number of SDK subscriptions by default. To increase the quota, send an application email based on the template below to push@vivo.com:
```plaintext
Subject: Application for Increasing the Quota of IM/System Messages for App XXX
Body: …
Application name: …
Package name: …
Application overview: …
IM/System message quota required (unit: 10,000): ...
Description of the specific push scenario: for example, personal user chat and merchant chat
```

### Using vivo system messages

Currently, vivo notification messages can be delivered only through RESTful APIs but not the console.
Set the `vivo_ch_id` parameter in the Android structure of the RESTful API request parameters to **1** to implement delivery of vivo system messages. For more information, see [push API parameter description](https://intl.cloud.tencent.com/document/product/1024/33764).
>?
>- The vivo push platform will conduct daily inspection of system messages according to the message classification criteria. It checks whether developers send operation messages through the system message channel, and imposes corresponding penalties (may disable the message push feature in worst cases) based on the degree and frequency of violations.
>- Please refer to the [message classification](https://dev.vivo.com.cn/documentCenter/doc/359) document to operate strictly in accordance with the platform message classification. For the penalty rules, see Message Classification Feature Description > V. Operation Supervision and Penalty > 3. Penalty Rules in this document.

Below is a sample push:

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

Starting from EMUI 10.0, Huawei's push service intelligently classifies notification messages into two levels: **service and communication** and **information and marketing**. Before EMUI 10.0, there is only one level and all messages are displayed through the **default notification** channel, equivalent to service and communication messages in EMUI 10.0.

The table below compares the display style of messages at different levels.

| Message Level | Displayed in the Notification Center | Displayed in the Status Bar | Notification for Screen Lock | Ringtone | Vibration |
| -------- | ---------------- | -------------- | -------- | ---- | ---- |
| Service and communication     | Normal         | Supported           | Supported     | Supported | Supported |
| Information and marketing     | Normal         | Not supported             | Not supported       | Not supported   | Not supported   |

Classification rules:

- Intelligent message classification
Intelligent classification algorithms will automatically categorize your messages according to classification criteria based on multiple dimensional factors such as the content you send.
- Self-help message classification
Starting from July 1, 2021, the Huawei Push service will begin to receive developers' applications for self-help message classification. After their applications are approved, developers can classify messages by themselves according to Huawei Push's classification specifications.

### Applying for self-help message classification permission
Currently, the self-help classification permission for Huawei notification messages can take effect only after you apply for it through email. For more information, please see [Message Classification Management Solution](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-management-solution-0000001149358835).

>!
> - If the application does not provide the self-help message classification feature, its push messages will be automatically classified by intelligent classification.
> - If the application provides the self-help message classification feature, the classification information provided by developers is trusted, and intelligent classification is not implemented for messages.
> 

### Using self-classified messages

Self-classified messages can be delivered only through APIs but not the console. After successfully obtaining the permission for self-help message classification, you can use the feature as follows:

Configure the `hw_importance` field in the `Android` request structure of the RESTful API to deliver self-classified messages. For more information, see the parameter description in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).

Below is a sample push:

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
        "title": "Account logged out:",
        "content": "Your account has been logged out due to login from an unusual login location.",
        "android": {
            "hw_importance":2
        }
    }
}
```

### Creating a Huawei notification channel

Huawei Push supports customizing notification channels for applications. To create a notification channel on the client, use either of the following methods:

1. Use the Android API to create a notification channel. For more information, see [Create and Manage Notification Channels](https://developer.android.google.cn/training/notify-user/channels).
2. Use the TPNS SDK (version 1.1.5.4 or later). For more information, see [Creating notification channel](https://intl.cloud.tencent.com/document/product/1024/30715) in the API documentation.

### Using a Huawei notification channel

Currently, notifications pushed through Huawe's custom channel can be delivered only through a RESTful API but not the console. After a notification channel is created, you can:

Configure the `hw_ch_id` field in the Android request structure of the RESTful API to push messages through the Huawei notification channel. For more information, see the parameter description in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).

>! A custom notification channel is applicable only for service and communication messages. Information and marketing messages are still displayed through the Huawei marketing notification channel.
>

Below is a sample push:

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
