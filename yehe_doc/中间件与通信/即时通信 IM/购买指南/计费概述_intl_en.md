> !
>- The original billing mode of Chat was disused on December 26, 2022.
>- Customers who created Chat applications before December 26, 2022 use the original billing mode ([details](https://www.tencentcloud.com/document/product/1047/52474)) by default. If you want to migrate to the current billing mode, [contact sales](https://www.tencentcloud.com/contact-us) or [submit a ticket](https://console.tencentcloud.com/workorder). Once migrated, the billing mode cannot be restored.

## Billing Overview
Chat is billed on a monthly billing cycle:
- Fees are billed by calendar month. Fees incurred in a calendar month will be deducted within the first 3 days of the next month.


## Basic Services
The basic service fee covers two parts: the **resource plan** fee and **out-of-plan resource usage** fee.
- Resource plan fee: Chat offers the Developer, Standard, and Premium editions. The edition for a created application defaults to the Developer edition (free). You can choose a plan based on your needs. For resource plan comparison, see [Comparison of billing plans](#tc).
- Out-of-plan resource usage fee: The fee charged for resource usage that exceeds the free quota of the Standard or Premium edition plan.


<dx-alert infotype="explain" title="Notes:">
- The feature of pushing to all users is available only to users with Developer and Premium edition accounts. You can apply for this feature as instructed in [Configuration Change Ticket](https://www.tencentcloud.com/document/product/1047/44322). The feature will be enabled **48 hours** after your application is approved.
- Community group (Community) is supported only in native SDK 5.8.1668 enhanced edition or later and web SDK 2.17.0 or later and is available only to Developer and Premium edition users. The feature is temporarily unavailable in IDCs in Germany and South Korea. Please stay tuned.
- The feature of read receipts for group messages is available in native SDK 6.1.2155 or later and only to Developer and Premium edition users. It is applicable to work groups (Work), public groups (Public), and meeting groups (Meeting) that support up to 200 members per group.
</dx-alert>

[](id:tc)
The following table compares the features of different plans:

| Feature       | Developer Edition      | Standard Edition    | Premium Edition           |
| ----------------- |---------- |----------------- | ------------------- |
| Global coverage | Supported | Supported | Supported |
| Maximum users | 100 | Unlimited | Unlimited |
| Maximum friends for a single user | 20 | 3,000 | 3,000 |
| Maximum groups a single user can join | 50 | 500 | 1,000 |
| Maximum members per group (non-audio-video group) | 20 | 200 |  2,000 |
| Maximum non-audio-video groups (excluding disbanded ones) | 100 | Unlimited | Unlimited |
| Maximum audio-video groups that can be created    | 10        | 50          | Unlimited             |
| Maximum net increase in group quantity per day | 100 | 10,000 | 10,000 |
| Free retention period of historical messages | 7 days | 7 days | 30 days |
| Quota of free monthly active users (MAU) | 100/month | 10,000/month | 10,000/month |
| [Pushing to all users](https://intl.cloud.tencent.com/document/product/1047/37165) | Supported | Not supported |Supported. You need to apply for it as instructed [here](https://intl.cloud.tencent.com/document/product/1047/44322) |
| Concurrent logins on multiple devices on the same platform | Supported | Not supported |Supported |
| Local message search (Android and iOS) | Supported | Not supported | Supported |
| Message history for new members in audio-video groups | Supported | Not supported |Supported |
| [Creating a community group](https://intl.cloud.tencent.com/document/product/1047/33529)   | Supported | Not supported | Supported |
| Read receipts for group messages  | Supported | Not supported | Supported |
|Targeted group messages | Supported | Not supported| Supported|
| List of online audio-video group members | Supported | Not supported | Supported |
| Broadcast messaging of audio-video group   | Supported | Not supported| Supported |
| User status      | Supported | Not supported | Supported |
| Conversation mark  | Supported | Not supported | Supported |
| Conversation group | Supported | Not supported | Supported |
|Audio-video group member banning | Supported | Not supported | Supported |



- **Maximum audio-video groups that can be created**: The total number of audio-video groups that can be created by all users under an application (SDKAppID). Audio-video groups support only text, image, short audio, and custom messages. Services such as [Cloud Streaming Services](https://intl.cloud.tencent.com/document/product/267) and [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647) need to be activated separately.
- **Maximum net increase in group quantity per day**: The net total number of groups (of all types) that can be created by all users under an application (SDKAppID) in a calendar day. Its value is 10,000, and up to 5 online broadcasting chat rooms can be created. If the quantity of groups created reaches the threshold of the day, but you need to create more groups, delete the groups that are no longer needed. For more information, see [Groups](https://intl.cloud.tencent.com/document/product/1047/33529).
- **MAU**: The number of unique users that log in to Chat app in a given month. A user that logs in repeatedly in the same month counts as only one MAU.
- **Community**: A community allows users to join and leave freely. It is suitable for chat scenarios with a super large number of community members, such as knowledge sharing and game discussion. For more information, see [Groups](https://intl.cloud.tencent.com/document/product/1047/33529).


## Value-Added Services
- The audio/video call feature is currently in beta, with a 60-day free trial provided. It applies to an individual application (SDKAppID) and supports status display, multi-client login, and cutting in a group call. The free edition of the audio/video call feature provides all feature items. For more details, see [Audio/video call feature details](#trtc).
- More value-added services are under development. If you have additional value-added service requirements when using Chat, [contact us](https://www.tencentcloud.com/document/product/1047/41676).


[](id:trtc)Audio/video call feature version details

| Feature                  | Free Edition            |
| :---------------------- | :---------------- |
| Audio/video call          | Supported              |
| Complete chat UI         | Supported              |
| Call status display        | Supported              |
| Calling notification        | Supported             |
| Floating window for call   | Supported              |
| Custom calling ringtone          | Supported              |
| Call launching/answering/rejecting/hanging up | Supported              |
| Group call                | Supported              |
| Launching/Cutting in a group call   | Supported              |
| Switch from video call to audio call    | Supported              |
| AI-based noise reduction                | Supported              |
| Outdoor calls optimization         | Supported              |
| Platform                | iOS, Android, Web |

<dx-alert infotype="explain" title="Notes:">
- **Audio/video call feature**:
  - **This feature is currently in beta. ​Each SDKAppID can be tried twice for free with a 60-day validity period for each trial, and up to 10 SDKAppIDs can be tried under one account.**
  - It is implemented based on Chat and TRTC services. Therefore, the TRTC service will be activated and applications created for you by default if you enable this feature.
  - Its free edition **only grants you the right to use the free edition free of charge. Your calls launched via this feature will be charged as stated in [Billing of TRTC Basic Services](https://www.tencentcloud.com/zh/document/product/647/42734), and relevant Chat services will be charged as stated in [Billing Overview](https://www.tencentcloud.com/zh/document/product/1047/34349) of Chat**.
    </dx-alert>

## References
- [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350)
- [Purchase Guide](https://www.tencentcloud.com/document/product/1047/36021)		
