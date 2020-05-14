The Opush platform provides an unlimited "private message" channel for personalized push scenarios. You can apply for the beta eligibility of the OPPO public/private message service. After applying for and creating the private message channel, you can use the TPNS server API for message push to improve the arrival rate of personalized pushes.
>In this document, "tunnel" and "channel" are the same concept.

## Notification Channel
From Android 8.0 (API level 26 or higher) on, Android requires that developers assign channels for all notifications, and different types of messages are sent through different channels. Developers can set the notification behavior of each channel, and users can modify the settings of individual channels. This feature aims to solve the following problems:
- More and more unimportant application notifications that disturb users can be disabled.
- Users can block selected notifications and receive only the ones they consider as important.


## OPPO Private Message Channel Overview
The default channel on the Opush platform is the public message channel. Now, the "private message" channel is provided to push user-specific personalized messages, with no limit on the number of pushes. The comparison between "public message" and "private message" is as follows:

| Type | Public Message | Private Message |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Push content | Universal content for multiple users such as trending news, new product promotions, platform announcements, community topics, and lucky draws | Content closely related to individual users such as changes of orders, package delivery notifications, subscribed content updates, interactive comments, and loyalty program point updates |
| Push object | Multiple users (single user is also allowed) | Only single user |
| Maximum number of pushes | All public message channels share a total number of pushes; if the daily limit is reached, they will stop pushing messages on the day. The current maximum number of daily pushes is the total number of all registered users * 2 | Unlimited |
| Configuration method | Default | You need to register the channel with the Opush platform and set the corresponding channel attribute to "Private Message" |

>Official reminder from OPPO: you must not use the private message channel to push universal messages (such as trending news and new product promotions), as the backend will monitor the push content, and if you violate the operational rules, Opush has the right to disable your private channel access, and all consequences arising therefrom, such as exceptional API calls and delivery failures of messages sent through the private message channel shall be borne by you.

## Application for OPPO Private Message Channel
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


## Use of OPPO Private Message Channel

1. Create a notification channel for the client in either of the following ways:
(1). Use the corresponding Android API to create a notification channel. For more information, please see [Create and Manage Notification Channels](https://developer.android.google.cn/training/notify-user/channels).
(2). Use the TPNS SDK (v1.1.5.4 or above) to create a notification channel. For more information, please see [Creating Notification Channels](https://intl.cloud.tencent.com/document/product/1024/30715#.E5.88.9B.E5.BB.BA.E9.80.9A.E7.9F.A5.E6.B8.A0.E9.81.93).
2. Configure RESTful API push.
Set the `n_ch_id` and `n_ch_name` parameters in the Android structure of the RESTful API request parameters so as to implement delivery based on notification channel. For more information, please see [Push API Parameter Description](https://intl.cloud.tencent.com/document/product/1024/33764#.E8.AF.B7.E6.B1.82.E5.8F.82.E6.95.B0).
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
        "n_ch_id": "Private channel ID",
        "n_ch_name": "Private channel name"}
  }
}

```