### How do I mute or unmute group members in a group chat?
Muting is a way to control how group members send messages. The muted member cannot send messages during the muting period. For more information on how to mute members, see the following SDK documents:
- [Muting Group Members (Android)](https://intl.cloud.tencent.com/document/product/1047/36271)
- [Muting Group Members (iOS)](https://intl.cloud.tencent.com/document/product/1047/36257)
- [Muting Group Members (Web)](https://intl.cloud.tencent.com/document/product/1047/34330)


Additionally, app admins can mute any member in any group through a RESTful API. For more information, see the [RESTful API: Batch Muting and Unmuting](https://intl.cloud.tencent.com/document/product/1047/34951).


### How do I query muted members and their muting periods?
Group admins and the group owner can mute or unmute members through the API provided by the IM SDK. To unmute members, set the muting period to 0.
To query information about muted members, you need to query group member profiles. For more information, see the following SDK documents:
- [Obtaining One’s Own Profile in a Group (Android)](https://intl.cloud.tencent.com/document/product/1047/36271)
- [Obtaining One’s Own Profile in a Group (iOS)](https://intl.cloud.tencent.com/document/product/1047/36257)
- [Obtaining the Group Member List (Web)](https://intl.cloud.tencent.com/document/product/1047/34330)

Additionally, the app admin can query information about muted members through a RESTful API. For more information, see the [RESTful API: Obtaining the List of Muted Members](https://intl.cloud.tencent.com/document/product/1047/34964).

### How do I view group messages from before I joined the group?

To view historical group messages sent before you joined the group, historical messages for the type of this group must support cloud storage. Based on group types and set use cases, the following configurations apply:
- **Audio-and-video chat rooms (AVChatRoom)** and **broadcasting chat rooms (BChatRoom)** in early versions do not support historical message storage. Therefore, you cannot view messages from before you joined these two types of groups.
- For non-live streaming groups, **work groups (Work)** and **public groups (Public)** by default do not allow members to view historical messages from before they joined the groups, whereas **meeting groups (Meeting)** by default allow members to view historical messages from before they joined the groups. To modify the default configuration, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to apply for modification.

The default retention period of historical messages of non-live streaming groups is 7 days (30 days for Ultimate edition). To extend this period, log in to the [console](https://console.cloud.tencent.com/im) and choose **Feature Configuration**. Extending the message retention period is a paid value-added service. For more information on billing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

### What are the differences between AVChatRoom and Meeting (ChatRoom in early versions)?

These two types of groups are designed for different scenarios. Specifically, Meeting is suitable for medium-sized groups (with less than 6,000 members), whereas AVChatRoom is suitable for large-scale live-streaming scenarios with unlimited members. The following table lists the major differences between their features:

| Group Feature                                                | Meeting                                                      | AVChatRoom                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------ |
| Maximum group members                                        | 6,000                                                        | Unlimited                      |
| Group member information                                     | All group member information is saved                        | No member information is saved |
| Group owner can set group admins                             | Yes                                                          | No                             |
| Delete group members                                         | The group admin, group owner, and app admin can delete group members. | Not supported                  |
| Message roaming                                              | Supported                                                    | Not supported                  |
| Members can view historical messages from before they joined the group | Yes. Messages within the retention period of historical messages can be viewed by default. | No                             |
| Notification on member changes                               | Not supported                                                | Supported                      |
| App admin can import groups                                  | Yes                                                          | No                             |

### Why cannot I obtain the values of a group/group member custom field?

Try the following troubleshooting methods:
1. Check whether the custom field is correctly configured in the console.
2. Check the following in the query request: the requester has the read permission and the group type supports the custom field.
3. Check whether the configuration request of the custom field has succeeded.
4. For group custom fields:
   - iOS: Before logging in to the IM SDK, navigate to TIMManager > setUserConfig > TIMUserConfig > TIMGroupInfoOption > groupCustom to set the relevant configuration.
   - Android: Before logging in to the IM SDK, navigate to TIMManager > setUserConfig > TIMUserConfig > TIMGroupSettings > groupInfoOptions > setCustomTags to set the relevant configuration.
5. For group member custom fields:
   - iOS: Before logging in to the IM SDK, navigate to TIMManager > setUserConfig > TIMUserConfig > TIMGroupMemberInfoOption > memberCustom to set the relevant configuration.
   - Android: Before logging in to the IM SDK, navigate to TIMManager > setUserConfig > TIMUserConfig > TIMGroupSettings > memberInfoOptions > setCustomTags to set the relevant configuration.
