## Group System
The group system is an instant messaging system that allows multiple participants to communicate in 1 chat. The group system has the following basic capabilities:

- Comprehensive [group management](https://intl.cloud.tencent.com/document/product/1047/33530) capabilities: creation and disbanding of a group, member management, group profile management, member profile management, and so on.
- Stable and reliable messaging and a sophisticated [group chat message](https://intl.cloud.tencent.com/document/product/1047/33526) management mechanism: permission control, muting, vulgar language filtering, message callback, message roaming, and so on.
- Based on common use cases, the following group types are configured by default: **work group (Work)**, **public group (Public)**, **meeting group (Meeting)**, and **audio-video chat room (AVChatRoom)**. You can create [custom group types](https://intl.cloud.tencent.com/document/product/1047/33529) based on business needs.
- Upper limit on the number of group members:
  - The number of members in a non-AVChatRoom group can be increased to a maximum of 6,000 if fees are paid. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
  - There is no upper limit on the number of members in an AVChatRoom.
- On the web or mini program end, AVChatRooms allow users to receive messages as guests without logging in.

>!
>- Although AVChatRooms support unlimited group members, if a spike in group members is expected within a short time (in scenarios such as large online events where members in a single group exceed 50,000), contact sales representatives in advance and report service resource usage by providing the SDKAppID and the scheduled event time.
>- Currently, historical message storage is available only for non-AVChatRoom groups, with messages stored for 7 days for billing plans of the Trial Edition and Pro Edition and 30 days for the Flagship Edition by default. If you require a longer storage period, change the storage period of historical messages in the [console](https://console.cloud.tencent.com/im). Increasing the storage period of historical messages is a value-added service. For more information on pricing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

IM's group system is highly customizable, allowing you to use:

- [Custom message formats](https://intl.cloud.tencent.com/document/product/1047/33527)
- [Custom group IDs](https://intl.cloud.tencent.com/document/product/1047/33529)
- [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529)
- [Custom group types](https://intl.cloud.tencent.com/document/product/1047/33529)
- [Custom callbacks](https://intl.cloud.tencent.com/document/product/1047/33529)

## Group Member Roles

The following table lists various group member roles and their permissions:

| Group Member Role | Description | Management Permissions |
| ------------ | -------------- | ------------ |
| Ordinary member | An ordinary member has no management permissions. | In a work group (Work), an ordinary member has the permission to modify the group profile. |
| Admin | An admin is appointed by the group owner to assist in managing group members and holds certain management permissions. | <ul style="margin:0;"><li>Modify basic group information</li><li>Remove an ordinary member from the group</li><li>Mute an ordinary member, that is, prevent the ordinary member from speaking for a certain period of time</li><li>Approve or reject a membership application</li></ul>Work groups do not support the setting of admins by default. |
| Group owner | A group owner is the creator of a group and has the highest level of management permissions in the group. | The group owner has the following permissions in addition to all permissions held by an admin:<ul style="margin:0;"><li>Appoint or cancel an admin</li><li>Remove an admin from the group</li><li>Mute an admin</li><li>Disband the group</li><li>Transfer the group</li></ul> |
| App admin | This special role has the authority to manage all group permissions in the app and has more power than the group owner. | The app admin has the same permissions as the group owner, whether it is a member of the group or not. |

<span id="GroupType"></span>
## Group Types

By default, the group system supports the following group types for common use cases:

| Group Type | Applicable Scenario |
|--------|---------|
| Work group (Work) | Similar to an ordinary WeChat group. After a work group is created, only a group member can invite other users to join this group, and the invitation does not need to be approved by the invited user or group owner. |
| Public group (Public) | Similar to a QQ group. After a public group is created, the group owner can specify a group admin. When a user searches for the group ID and initiates a request to join the group, the request must be approved by the group owner or admin before the user can join the group. |
| Meeting group (Meeting) | After a meeting group is created, a user can join and quit the group as desired, and view messages sent before the user joined the group. This group type is suitable for scenarios where real-time audio/video services are used, for example, audio and video conferencing and online education. |
| Audio-video chat room (AVChatRoom) | After an AVChatRoom is created, a user can join and quit the group as desired. This group type does not limit the number of members, but it does not support storage of historical messages. It can be used together with Live Video Broadcasting (LVB) to support on-screen comments. |


### Differences in basic group capabilities

| Item | Work Group | Public Group | Meeting Group | AVChatRoom |
|--- |-- |-- |-- |-- |
| Available member roles | Group owner<br>Ordinary member<br>App admin | Group owner<br>Admin<br>Ordinary member<br>App admin | Group owner<br>Admin<br>Ordinary member<br>App admin | Group owner<br>Ordinary member<br>App admin |
| Modify basic group information | Ordinary member | Group admin<br>Group owner<br>App admin | Group owner<br>App admin | App admin |
| Obtain group member information | Information of all group members  |Information of all group members|Information of the first 300 group members| None group member information |
| Disband a group | Only the app admin can disband a group. |The group owner and group admin can disband the group. | The group owner and group admin can disband the group. | The group owner and group admin can disband the group. |

>?
>- Ordinary members of a work group (Work) can modify only the group name, introduction, announcement, and group profile photo URL, but not other basic group information.
>- If the roles of a group type cannot meet your business needs, you can add roles by setting member-level [custom fields](https://intl.cloud.tencent.com/document/product/1047/33529).
>- It is necessary to obtain the information about some members in scenarios where an AVChatRoom displays a list of some of its members.

### Differences in joining a group

| Item | Work Group | Public Group | Meeting Group | AVChatRoom |
|--- |-- |-- |-- |-- |
| Perform an exact search for a group ID to join a group | Not supported | Supported | Supported | Supported |
| Perform a fuzzy search for group information to join a group | Not supported | Not supported | Not supported | Not supported |
| Apply to join a group | Not supported | Supported. Approval from the group owner or admin is needed. | Supported. No approval is needed. | Supported. No approval is needed. |
| Join a group after receiving an invitation from a group member | Supported | Not supported | Not supported | Not supported |

>?
>- Exact search: search for a group by group ID. Fuzzy search: search for a group by fields such as the group name.
>- Approval for joining a group: the group owner and admin can choose to approve or reject applications made by non-members to join the group. Only approved users can join the group.
>- For a group type that does not support the invitation of non-members to a group, group members can share the group ID with non-members in the app so that the non-members can join the group.

### Differences in member management capabilities

| Item | Work Group | Public Group | Meeting Group | AVChatRoom |
|--- |--- |--- |--- |--- |
|Set an admin | Not supported | Supported | Supported | Not supported |
| A group owner quits the group | Supported. After the group owner quits, the group has no group owner. | Not supported | Not supported | Not supported |
| Remove a group member | Supported. The group owner can remove group members. | Supported. The group owner and admin can remove group members, but the admin can remove only ordinary group members. | Supported. The group owner and admin can remove group members, but the admin can remove only ordinary group members. | Not supported. The muting feature can be used to achieve a similar effect. |
| Mute a group member | Not supported | Supported. The group owner and admin can mute group members, but the admin can mute only ordinary group members. | Supported. The group owner and admin can mute group members, but the admin can mute only ordinary group members. | Supported. The group owner can mute group members. |
| Periodically remove offline group members | Supported, but disabled by default | Supported, but disabled by default | Supported, but disabled by default | Not supported |

>!Muted group members cannot send group chat messages.


### Differences in group limits
| Item | Work Group/Public Group/Meeting Group | AVChatRoom |
|--- |--- |--- |
| Maximum number of members | <ul style="margin:0;"><li>Trial Edition: 20 per group</li><li>Pro Edition: 200 per group by default, can be increased to 2,000 per group through a [value-added service](https://intl.cloud.tencent.com/document/product/1047/34350#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B5.84.E8.B4.B9)</li><li>Flagship Edition: 2,000 per group by default, can be increased to 6,000 per group through a [value-added service](https://intl.cloud.tencent.com/document/product/1047/34350#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B5.84.E8.B4.B9).</li></ul> | Unlimited |
| Maximum number of groups | <ul style="margin:0;"><li>Trial Edition: up to 100 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition or Flagship Edition: unlimited</li></ul> | <ul style="margin:0;"><li>Trial Edition: up to 10 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition: up to 50 existing groups, and disbanded groups do not count against the quota. You can upgrade to an unlimited number of AVChatRooms by purchasing a [value-added service](https://intl.cloud.tencent.com/document/product/1047/34350#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B5.84.E8.B4.B9).</li><li>Flagship Edition: unlimited</li></ul> |

>!
>- For an SDKAppID of the Pro Edition or Flagship Edition, up to 10,000 groups regardless of the group type (the number of created groups minus the number of disbanded groups) can be added in a day.
>- For an SDKAppID of the Pro Edition or Flagship Edition, up to 100,000 groups can be added for free in a month. If this quota is exceeded, [fees for usage exceeding the free quota](https://intl.cloud.tencent.com/document/product/1047/34350#.E5.A5.97.E9.A4.90.E5.A4.96.E8.B6.85.E9.87.8F.E8.B4.B9.E7.94.A8) will be charged. It is recommend that you disband the groups that are no longer needed in a timely manner.


### Differences in message capabilities

| Item | Work Group | Public Group | Meeting Group | AVChatRoom |
|--- |--- |--- |--- |--- |
| Unread count is supported | Yes | Yes | No | No |
| Group members can view messages sent before they join the group | No | No | Yes | No |
| Historical message storage is supported | Yes | Yes | Yes | No |
| Member change notifications are supported | Yes | Yes | No | Yes |
| A message must be sent to activate a new group | Yes | No | No | No |
| Default message receiving option | Receive online and offline pushed messages | Receive online and offline pushed messages | Receive only online pushed messages | Receive only online pushed messages |
| Users can receive group messages as guests without logging in | No | No | No | Yes |

>!
>- A group that requires activation is inactive before the group owner sends a message and is invisible to all group members except the group owner. A group that does not require activation is visible to all group members once created.
>- Currently, offline push is available only on Android (Android offline push) and iOS (APNs push) platforms.
>- The work group, public group, and meeting group have the historical message storage capability, which allows historical messages to be stored for 7 days (30 days for the Flagship Edition) free of charge by default. If you need a longer storage period, change the storage period of historical messages in the [console](https://console.cloud.tencent.com/im). Increasing the storage period of historical messages is a value-added service. For more information on pricing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).


### Differences in batch import and automatic repossession

| Item | Work Group/Public Group/Meeting Group | AVChatRoom |
|--- |--- |--- |
| Importing groups, group members, and group messages is allowed | Yes. It is allowed when historical groups are migrated from a third-party platform to IM. | No. Only existing groups, group members, and group messages can be used. |
| Time before a group is automatically repossessed (in seconds) | The backend does not repossess a group, unless the group owner disbands the group or all members quit the group. | The backend does not repossess a group, unless the group owner disbands the group or all members quit the group. |

>!To enable group repossession, submit a ticket. After configuration, inactive groups will be cleaned up by group type. An inactive group is a group in which no messages are sent and no member changes occur.

## Group Data Structure
### Basic group information

| Field Name | Type | Description | Notes |
|--- |--- |--- |--- |
| GroupId | String | Unique identifier of the group | Read-only<br>The ID of the group, which must be unique in the app. The prefix is @TGS#, and custom group IDs can also be used in the app. |
| Type | String | Group type | Read-only<br>The following group types are supported by default: work group, public group, meeting group, and AVChatRoom. For more information, see [Group Types](#GroupType).<br>In the SDK of an earlier version, group types also include the private group, ChatRoom, and BChatRoom, which are not recommended. |
| Name | String | Name of the group | Readable and writable. The maximum length is 30 bytes and cannot be adjusted. |
| Introduction | String | Introduction to the group | Readable and writable. The maximum length is 240 bytes and cannot be adjusted. |
| Notification | String | Group announcement | Readable and writable. The maximum length is 300 bytes and cannot be adjusted. |
| FaceUrl | String | URL of the group's profile photo | Readable and writable. The maximum length is 100 bytes and cannot be adjusted. |
| Owner_Account | String | ID of the group owner | Read-only |
| CreateTime | Integer | Creation time of the group | Read-only |
| InfoSeq | Integer | This value increases every time the group information changes. | Read-only |
| LastInfoTime | Integer | Time of the last change to group information | Read-only |
| LastMsgTime | Integer | Time of the last message in the group chat | Read-only |
| NextMsgSeq | Integer | Seq of the next message in the group chat | Read-only<br>Every message in the group chat has a unique message Seq. Seq values are continuous based on the sequence of sent messages. With every message sent in the group chat, `NextMsgSeq` (starting from 1) increases by 1. |
| MemberNum | Integer | Number of current members | Read-only |
| MaxMemberNum | Integer | Maximum number of members | - |
| ApplyJoinOption | String | Membership application option | The following options are available:<ul style="margin:0;"><li>DisableApply: disallow any application.</li><li>NeedPermission: group owner or admin's approval is required.</li><li>FreeAccess: users can join the group freely without prior approval.</li></ul>|


>!The permissions to modify the group name, introduction, announcement, and profile photo URL are described as follows:
>- In a work group, any member can modify them.
>- For other group types, only **non-ordinary members** can modify them.

### Group member profiles

| Field Name | Type | Description | Notes |
|--- |--- |--- |--- |
| Member_Account | String | Group member ID | Read-only |
| Role | String | Role in the group | A group has the following roles: Owner (group owner), Admin (group admin), and Member (group member). |
| JoinTime | Integer | Time of joining the group | Read-only |
| MsgSeq | Integer | Current read message Seq of the member | Read-only |
| MsgFlag | String | Message receiving option | The following options are available:<ul style="margin:0;"><li>AcceptAndNotify: receive and notify.</li><li>AcceptNotNotify: receive without notifying (remote APNs push is not triggered).</li><li>Discard: block group messages (messages are not pushed to clients.)</li></ul>|
| LastSendMsgTime | Integer | Time of sending the last message | Read-only |
| NameCard | String | Group name card | Readable and writable |

## Custom Group Types

If the [group types](#GroupType) provided by IM cannot meet your needs, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to modify existing group types or add custom group types.
For example, you can create a group that is used in an office environment. This group is similar to a work group, but every member has the highest level of management permissions and can view messages sent before they join the group. In this case, you can:
- Choose the work group type and [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to enable the **view historical messages before joining** and **allow ordinary members to remove members** options.
- [Submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for a new group type named OAGroup. Specify work group as the reference type and enable the **view historical messages before joining** and **allow ordinary members to remove members** options.  

>!
>- When creating a group type, you must specify a group type as a **reference type**. Note that BChatRoom in SDK of earlier versions cannot be specified as a reference type.
>- After configuration, the new group type will have new features that are specified in the ticket, and the same features as the reference type.

## Custom Group IDs

When a group is created in the app, IM assigns a default group ID to the new group by default. This default group ID starts with @TGS# and is unique in the app.
IM also allows you to customize group IDs that are simple and easy to remember and communicate. A custom group ID must be a string of ASCII characters (0x20-0x7e) with a length less than 48 bytes. Do not use @TGS# as the prefix to avoid confusion with assigned group IDs.

## Custom Fields

IM allows you to configure up to 20 group-level custom fields and 5 member-level custom fields based on your business needs. With custom fields, apps can attach additional data to groups and read and write data through existing APIs. **Custom fields cannot be deleted once created and applied.**

### Description

Custom fields have the following characteristics:

- Their values are expressed in the key-value format.
- Key is a string with a maximum length of 16 bytes. Its name contains only uppercase and lowercase letters, digits, and underscores (_).
- Value is a buffer customized by the user, which can be binary data. Group-level values have a maximum length of 512 bytes, while member-level values have a maximum length of 64 bytes.
- You can configure the least read permission and the least write permission for each key.

The read and write permissions of a custom field are as follows, from high to low:

1. Readable and writable by the app admin.
2. Readable and writable by the group owner.
3. Readable and writable by the group admin.
4. Readable and writable by group members.
5. Readable and writable by anyone, including non-members.

For example, an app needs to extend the `GroupLevel` field for groups and the value of this field is a number representing the level of a group. If this level information is calculated by the app backend, then the least write permission should be **writable by the app admin**. If the field is part of the public profile of the group, its least read permission should be **readable by anyone, including non-members**.

If the value to be stored is a number, we recommend that C and C++ developers store it as a string instead of binary data. For example, when the number to be stored is 1, store it as string **1** instead of binary data **0x01**. In the future, IM will offer more operations for custom fields, such as specific mathematical operations on values, which will be performed on the basis of string-type numbers.

### Configuration method

Custom fields at these 2 levels can be configured in IM Console.
To configure member-level custom fields, you need to specify the group type first. AVChatRoom and custom group types that are configured based on it do not support custom fields at the group member level, because these types of groups do not store member profiles.
The **self read and write permissions** indicate whether members can read and write their own member-level custom fields. For example, a member-level custom field named `MemberLevel` represents the level of a member in a group. Group members can read but not modify their own levels, and therefore **self read and write permissions** are set to **readable/unwritable** for this field.

## Custom Callbacks

Third-party callback is an important means to meet the special requirements of apps. It provides users with the capability to customize actions.
IM's group system supports different callbacks. For more information, see [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354) and [List of Callback Commands](https://intl.cloud.tencent.com/document/product/1047/34355).
