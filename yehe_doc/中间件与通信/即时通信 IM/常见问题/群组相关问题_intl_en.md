### How do I mute or unmute group members in a group chat?
Muting is one way to control how group members send messages. The muted member cannot send messages during the muting duration. For more information on how to set muting, see the following SDK documentation:
- [Muting group members (Android)](https://intl.cloud.tencent.com/document/product/1047/48466)
- [Muting group members (iOS)](https://intl.cloud.tencent.com/document/product/1047/48181)
- [Muting group members (Web)](https://intl.cloud.tencent.com/document/product/1047/48180)


Additionally, the app admins can mute any member in any group through a RESTful API. For more information, see [RESTful API: Batch Muting and Unmuting](https://intl.cloud.tencent.com/document/product/1047/34951).


### How can I view muted members and their muting periods?
Admins and group owners can mute or unmute members through the API provided by the IM SDK. To unmute members, set the muting period to `0`.
The muting information of members can be queried by querying the group member profiles. For detailed settings, see the following SDK documents:
- [Getting Group Member Profile (Android)](https://intl.cloud.tencent.com/document/product/1047/48178)
- [Getting Group Member Profile (iOS)](https://intl.cloud.tencent.com/document/product/1047/48178)
- [Getting group member list (Web)](https://intl.cloud.tencent.com/document/product/1047/48180)

Additionally, the app admin can query information about muted members through a RESTful API. For more information, see [RESTful API: Getting the List of Muted Members](https://intl.cloud.tencent.com/document/product/1047/34964).

### How can I view roaming messages from before I join the group?

You can view only cloud roaming messages from before joining the group. The following configurations are performed based on the group types and use cases:
- **Audio-video groups** and **broadcasting chat rooms** on earlier versions do not support historical message storage. Therefore, you cannot view roaming messages from before joining them.
- Among non-audio-video groups, **work groups** and **public groups** do not allow viewing roaming messages from before group join by default; **meeting groups** and **communities** allow viewing roaming messages from before group join by default. To modify the configuration, select **Feature Configuration** > **Group configuration** > **Group message configuration** in the [**console**](https://console.cloud.tencent.com/im).

The default message history storage period of non-audio-video groups is 7 days (30 days for the Ultimate edition). To extend this period, select **Feature Configuration** in the [console](https://console.cloud.tencent.com/im). An extended message history storage period is a value-added service. For its billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

### What is the difference between audio-video groups (AVChatRoom) and meeting groups (Meeting or ChatRoom on earlier versions)?

These two types of groups are designed for different scenarios: a meeting group is suitable for medium-sized groups (less than 6,000 members), while an audio-video group is suitable for large-scale live-streaming scenarios with unlimited members. Their differences are as described below:

| Group Feature                  | Meeting Groups                               | Audio-Video Groups            |
| ------------------------- | --------------------------------------- | --------------------- |
| Maximum number of group members                | 6,000                                 | Unlimited                |
| Group member information                | Information of all the group members is stored.                      | Member information is not stored. |
| Setting the group admin by the group owner  | Supported                                    | Not supported                |
| Deleting group members                | The group admin, group owner, and application admin can delete group members. | Not supported                |
| Message roaming          | Supported                                    | Not supported                |
| Viewing historical messages before group join    | Historical messages can be viewed within the storage period by default.          | Not supported                |
| Member change notification      | Not supported                                  | Supported                  |
| Importing group data by the application admin | Supported                                    | Not supported                |

### Why can't I obtain the values of custom group/member fields?

You can troubleshoot the issue in the following steps:
1. Check whether the custom field is correctly configured in the console.
2. Check whether users have the read permission and whether the custom field is supported by the group type in the query requests.
3. Check whether the request to set the custom field is sent successfully.
4. For custom group fields:
   - iOS: before logging in to the IM SDK, go to TIMManager -> setUserConfig -> TIMUserConfig -> TIMGroupInfoOption -> groupCustom to set the relevant configuration.
   - Android: before logging in to the IM SDK, go to TIMManager -> setUserConfig -> TIMUserConfig -> TIMGroupSettings -> groupInfoOptions -> setCustomTags to set the relevant configuration.
5. For custom group member fields:
   - iOS: before logging in to the IM SDK, go to TIMManager -> setUserConfig -> TIMUserConfig -> TIMGroupMemberInfoOption -> memberCustom to set the relevant configuration.
   - Android: before logging in to the IM SDK, go to TIMManager -> setUserConfig -> TIMUserConfig -> TIMGroupSettings -> memberInfoOptions -> setCustomTags to set the relevant configuration.
   
   
 ### How can I get the number of online members in an audio-video group?
You can get the number of online members in an audio-video group by calling the SDK API ([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce), [iOS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae), [web](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupOnlineMemberCount), or [Flutter](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupOnlineMemberCount.html)) or [RESTful API](https://intl.cloud.tencent.com/document/product/1047/38521).
)、[iOS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae)、[Web](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupOnlineMemberCount)、[Flutter](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupOnlineMemberCount.html)）或者 [REST API](https://intl.cloud.tencent.com/document/product/1047/38521) 接口获取。

### How can I determine whether the group message limit of 40 messages per second is exceeded when there is no prompt?
After the limit is exceeded, no error code will be returned to the caller by default. To have the error code ([10023](https://intl.cloud.tencent.com/document/product/1047/34348)) returned to the caller, [submit a ticket](https://intl.cloud.tencent.com/document/product/1047/44322) for application.
