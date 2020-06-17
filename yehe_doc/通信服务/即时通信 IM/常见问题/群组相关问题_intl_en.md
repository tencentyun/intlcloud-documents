### How do I mute or unmute group members in a group chat?
Muting is one way to control how group members send messages. The muted member cannot send messages during the muting duration. For more information on how to set muting, see the following SDK documentation:
- [Muting group members (Android)](https://intl.cloud.tencent.com/document/product/1047/34328)
- [Muting group members (iOS)](https://intl.cloud.tencent.com/document/product/1047/34329)
- [Muting group members (Web)](https://intl.cloud.tencent.com/document/product/1047/34330)


Additionally, the app admins can mute any member in any group through a RESTful API. For more information, please see [RESTful API: Batch Muting and Unmuting](https://intl.cloud.tencent.com/document/product/1047/34951).


### How do I check muted members and their muting duration?
The admin and group owner can mute or unmute members through the API provided by the IM SDK. To unmute members, set the muting duration to 0.
To query information about muted members, you need to query group member profiles. For more information, see the following SDK documentation:
- [Getting one’s own profile in a group (Android)](https://intl.cloud.tencent.com/document/product/1047/34328)
- [Getting one’s own profile in a group (iOS)](https://intl.cloud.tencent.com/document/product/1047/34329)
- [Getting group member list (Web)](https://intl.cloud.tencent.com/document/product/1047/34330)

Additionally, the app admin can query information about muted members through a RESTful API. For more information, please see [RESTful API: Getting the List of Muted Members](https://intl.cloud.tencent.com/document/product/1047/34964).

### How do I view group messages from before I joined the group?

To view group messages from before joining the group, the group must support message roaming.
As audio-video chat rooms and broadcasting chat rooms currently do not support message roaming, you cannot view messages from before joining these two types of groups.
By default, private groups and public groups do not allow members to view messages from before they joined the group. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to enable this feature. Chat rooms allow members to view the message history from before they joined the group by default.
The default message history storage period of private groups, public groups, and chat rooms is 7 days. To extend message history storage period, go to [console](https://console.cloud.tencent.com/im) ->**Feature Configuration**. Extending the message roaming period is a value-added service, see [Price Specification](https://intl.cloud.tencent.com/document/product/1047/34350) for more information on billing.

### What are the differences between AVChatRoom and ChatRoom?

These two types of groups are designed for different scenarios: ChatRoom is suitable for medium-sized groups (less than 10,000 members), while AVChatRoom is suitable for large-scale live-streaming scenarios with unlimited members. The following table lists the major differences:

| Group Feature | ChatRoom | AVChatRoom |
| ------------------------- | --------------------------------------- | --------------------- |
| Maximum group members | 6,000 | Unlimited |
| Group member information | All group member information is saved | Only the information of 300 group members is saved |
| Can the group owner sets group admins? | Yes | No |
| Deleting group members | The group admin, group owner, and app admin can delete group members | Unsupported |
| Message roaming | Supported | Unsupported |
| Can members view message history from before they joined the group? | Messages within the roaming period can be viewed by default | No |
| Notification on member modifications | Unsupported | Supported |
| Can the app admin import groups? | Yes | No |

### Why can’t I get the values of a group/group member custom field?

Try the following troubleshooting methods:
1. Check whether the custom field is correctly configured in the console.
2. Verify the following in the query request: the requester has read access, and the group type supports the custom field.
3. Verify that the configuration request of the custom field has succeeded.
4. For group custom fields:
   - iOS: before logging in to the IM SDK, go to TIMManager -> setUserConfig -> TIMUserConfig -> TIMGroupInfoOption -> groupCustom to set the relevant configuration.
   - Android: before logging in to the IM SDK, go to TIMManager -> setUserConfig -> TIMUserConfig -> TIMGroupSettings -> groupInfoOptions -> setCustomTags to set the relevant configuration.
5. For group member custom fields:
   - iOS: before logging in to the IM SDK, go to TIMManager -> setUserConfig -> TIMUserConfig -> TIMGroupMemberInfoOption -> memberCustom to set the relevant configuration.
   - Android: before logging in to the IM SDK, go to TIMManager -> setUserConfig -> TIMUserConfig -> TIMGroupSettings -> memberInfoOptions -> setCustomTags to set the relevant configuration.
