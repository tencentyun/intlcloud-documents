### How do I mute or unmute group members in a group chat?
Muting is one of the methods to control how group members send messages. Muted member cannot send messages during the muting period. For more information on how to set muting, see the following SDK documents:
- [Android - Muting Members](https://cloud.tencent.com/document/product/269/9236#.E5.AF.B9.E7.BE.A4.E6.88.90.E5.91.98.E8.BF.9B.E8.A1.8C.E7.A6.81.E8.A8.80)
- [iOS - Muting Members](https://cloud.tencent.com/document/product/269/9152#.E5.AF.B9.E7.BE.A4.E6.88.90.E5.91.98.E8.BF.9B.E8.A1.8C.E7.A6.81.E8.A8.80)
- [Web - Muting Members](https://cloud.tencent.com/document/product/269/1602#.E8.8E.B7.E5.8F.96.E7.BE.A4.E6.88.90.E5.91.98.E5.88.97.E8.A1.A8)


Additionally, the app admin can mute any member in any group through a RESTful API. For more information, see [RESTful APIs: Batch Muting and Unmuting](https://cloud.tencent.com/document/product/269/1627).


### How do I view muted members and their muting periods?
The admin and group owner can mute or unmute members through the API provided by the IM SDK. To unmute members, simply set the muting period to 0.
To query information about muted members, you need to query group member information. For more information, see the following SDK documents:
- [Android - Obtaining Your Own Information in a Group](https://cloud.tencent.com/document/product/269/9236#.E8.8E.B7.E5.8F.96.E6.9C.AC.E4.BA.BA.E5.9C.A8.E7.BE.A4.E9.87.8C.E7.9A.84.E8.B5.84.E6.96.99)
- [iOS - Obtaining Your Own Information in a Group](https://cloud.tencent.com/document/product/269/9152#.E8.8E.B7.E5.8F.96.E6.9C.AC.E4.BA.BA.E5.9C.A8.E7.BE.A4.E9.87.8C.E7.9A.84.E8.B5.84.E6.96.99)
- [Web - Obtaining a List of Group Members](https://cloud.tencent.com/document/product/269/1602)

Additionally, the app admin can query information about muted members through a RESTful API. For more information, see [RESTful APIs: Obtaining the List of Muted Members](https://cloud.tencent.com/document/product/269/2925).

### How do I view group messages from the time before I joined the group? 

To view group messages from the time before you join the group, the group must support message roaming.
As AVChatRoom and BChatRoom groups currently do not support message roaming, you cannot view messages from the time before you join both types of groups.
By default, Private and Public groups do not allow members to view messages from the time before they joined the group. To enable this feature, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1). By default, ChatRoom groups allow members to view historical messages from the time before they joined the group.
By default, Private, Public, and ChatRoom groups support 7-day message roaming. To increase the message roaming period, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1). For more information, see [Pricing](https://cloud.tencent.com/document/product/269/11673).

### What are the differences between AVChatRoom and ChatRoom?

Both types of groups are designed for different scenarios: ChatRoom is suitable for medium-size groups (with less than 10,000 members), whereas AVChatRoom is suitable for large-scale live-streaming scenarios with unlimited members. The following table lists their major differences:

| Group Feature | ChatRoom | AVChatRoom |
| ------------------------- | --------------------------------------- | --------------------- |
| Maximum group members | 6,000 | Unlimited |
| Group member information | All group member information is stored | Only the information of 300 group members is stored |
| Group owner can set group admins | Yes | No |
| Deleting group members | Group admin, group owner, and app admin can delete group members | Unsupported |
| Support message roaming | Yes | No |
| Members can view historical messages from the time before they joined the group | Yes, and messages within the roaming period can be viewed by default | No |
| Supports notifications on member changes | No | Yes |
| App admin can import groups | Yes | No |

### Why cannot I obtain the values of a group custom field or group member custom field?

Troubleshoot this issue as follows:
1. Check whether the custom field is correctly configured in the console.
2. Verify the following in the query request: the requester has the read permission, and the group type supports the custom field.
3. Verify that the configuration request of the custom field has succeeded.
4. For group custom fields:
   - iOS: before logging in to the IM SDK, configure by navigating to TIMManager > setUserConfig > TIMUserConfig > TIMGroupInfoOption > groupCustom.
   - Android: before logging in to the IM SDK, configure by navigating to TIMManager > setUserConfig > TIMUserConfig > TIMGroupSettings > groupInfoOptions > setCustomTags.
5. For group member custom fields:
   - iOS: before logging in to the IM SDK, configure by navigating to TIMManager > setUserConfig > TIMUserConfig > TIMGroupMemberInfoOption > memberCustom.
   - Android: before logging in to the IM SDK, configure by navigating to TIMManager > setUserConfig > TIMUserConfig > TIMGroupSettings > memberInfoOptions > setCustomTags.
