## Group System
The group system is an instant messaging system that allows multiple participants to communicate in one chat. The group system has the following basic capabilities:

- Comprehensive [group management](https://intl.cloud.tencent.com/document/product/1047/33530) capabilities: creating and disbanding a group, member management, group profile management, member profile management, and more.
- Stable and reliable messaging and a sophisticated [group messaging](https://intl.cloud.tencent.com/document/product/1047/33526) management mechanism: permission control, muting, bad language filtering, message callback, message roaming, and more.
- Built-in group types including private group (Private), public group (Public), chat room (ChatRoom), audio-video chat room (AVChatRoom), and broadcasting chat room (BChatRoom). You can also create [custom group types](https://intl.cloud.tencent.com/document/product/1047/33529) as needed.
- Different group sizes are supported:
 - The maximum number of members is 200 for a private group, 2,000 for a public group, and 6,000 for a chat room. Note that for these three group types, the actual maximum number of members is subject to the specific standard billing plan. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
 - Audio-video chat rooms and broadcasting chat rooms can support unlimited participants and they are not limited by standard billing plans. However, the number of audio-video chat rooms you can create is limited by the specific standard billing plan. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
- On the web, audio-video chat rooms and broadcasting chat rooms allow users to receive messages as guests without logging in.

>
>- While audio-video chat rooms (AVChatRoom) and broadcasting chat rooms (BChatRoom) support unlimited group members, if a spike in group members is expected within a short time (in scenarios such as large online events where members in a single group exceed 50,000), contact Tencent Cloud customer service or sales representatives in advance and report service resource usage by providing the SDKAppID and the scheduled event time.
>- Currently, message roaming is only available to private groups, public groups, and chat rooms, with messages stored for 7 days by default. If you need a longer storage period, change the message roaming period value in the [console](https://console.cloud.tencent.com/im). Increasing the message roaming period is a value-added service. For more information on pricing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

IM’s group system is also highly customizable, allowing you to use:

- [Custom message formats](https://intl.cloud.tencent.com/document/product/1047/33527)
- [Custom group IDs](https://intl.cloud.tencent.com/document/product/1047/33529)
- [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529)
- [Custom group types](https://intl.cloud.tencent.com/document/product/1047/33529)
- [Custom callbacks](https://intl.cloud.tencent.com/document/product/1047/33529)

## Group Member Roles

The following table lists various group member roles and their permissions:

| Group Member Role | Description | Management Permissions |
| ------------ | ------------------------------------------ | ---------------------------------------------- |
| Ordinary member | An ordinary group member has no management permissions. | None |
| Admin | Admins are appointed by the group owner to assist with managing group members and hold certain management permissions. | <br>1. Modify basic group information<br>2. Remove an ordinary member from the group<br>3. Mute an ordinary member, that is, prevent the ordinary member from speaking for a certain period of time<br>4. Approve or reject a membership application |
| Group owner | The group owner is the creator of a group and has the highest level of management permissions in the group. | The group owner has the following permissions in addition to all permissions held by the admins:<br>1. Appoint or cancel an admin<br>2. Remove an admin from the group<br>3. Mute an admin<br>4. Disband the group<br>5. Transfer the group |
| App admin | This special role has the authority to manage all group permissions in the app and more power than the group owner. | The app admin has the same permissions as the group owner, whether it is a member of the group or not. |

## Group Types

By default, the group system supports five group types:

| Group Type | Applicable Scenario |
|--------|---------|
| Private group (Private) | Suitable for more private chat scenarios, where the group profile is not made public and a user can join the group only by being invited by a group member. Private groups are similar to the groups in WeChat. |
| Public group (Public) | Suitable for public chat scenarios. Public groups have a strict management and admission mechanism. Public groups are similar to QQ groups. |
| Chat room (ChatRoom) | Has a less stringent management mechanism and allows room members to join and exit the room freely. |
| Audio-and-video chat room (AVChatRoom) | Suitable for interactive live broadcasting scenarios. Similar to an ordinary chat room, it allows room members to join and exit the room freely, but does not impose a limit on the number of room members. It also allows users to receive messages as guests without logging in. |
| Broadcasting chat room (BChatRoom) | Suitable for scenarios where messages are pushed to all online users, such as megaphone messages in a live broadcasting system. |

These group types are suitable for different scenarios, and therefore they support slightly different management methods, as described below:

### Differences in group operations

| Operation | Private Group | Public Group/Chat Room | Audio-and-Video Chat Room | Broadcasting Chat Room |
|--- |-- |-- |-- |-- |
| Fuzzy search | Not supported | Not supported | Not supported | Not supported |
| Exact search | Not supported | Supported | Supported | Not supported |
| Permission to modify basic group information | Ordinary member | Group admin<br>Group owner<br>App admin | Group owner<br>App admin | App admin |
| Obtain group member information | Information of all group members | Information of all group members | Information of up to 300 group members | None group member information |
| Disband a group | Only the app admin can disband a group | Group owner and app admins can disband the group | Group owner and app admins can disband the group | Only the app admin can disband the group |


>
>- Fuzzy search: search for a group by fields such as the group name. Exact Search: search for a group by group ID.
>- Ordinary members of a private group can modify only the group name, introduction, announcement, and group profile photo URL, but not other basic group information.
>- It is necessary to obtain the information of some members in scenarios where a broadcasting chat room displays a list of some of its members.


### Differences in group member operations

| Operation | Private Group | Public Group/Chat Room | Audio-and-Video Chat Room/Broadcasting Chat Room |
|--- |--- |--- |--- |
| Apply to join a group | Not allowed | For public groups, the application must be approved by the admin. For chat rooms, the applicant can join directly without admin approval. | The applicant can join directly without admin approval. |
| Invite non-members to a group | 1. Any group member can invite non-members and add them to the group without the prior confirmation of invitees.<br>2. Add new members when creating a group. |1. By default, only the app admin can invite non-members to the group.<br>2. Add new members when creating a group. | 1. No one is allowed to invite non-members to the group, including the app admin.<br>2. No one is allowed to add new members when creating the group. |
| Whether group owner can quit the group | Yes. After the group owner quits, the group has no group owner. | No, unless the group owner disbands the group. | No, unless the group owner disbands the group. |
| Whether group owner can set an admin | No | Yes | Yes |
| Remove a group member | The group owner and app admin can remove group members. | The group admin, group owner, and app admin can remove group members. | No one (including the app admin) is allowed to remove group members. |
| Periodically remove offline group members | Disabled by default | Disabled by default | Not supported |

> For audio-video chat rooms and broadcasting chat rooms, only the first 300 group members can be set as admins.



### Differences in group limits

| Item | Private Group | Public Group | Chat Room | Audio-and-Video Chat Room | Broadcasting Chat Room |
|--- |--- |--- |--- |--- |--- |
| Maximum number of members | 200 | 2,000 | 6,000 | Unlimited | Unlimited |
| Maximum daily net increase in group quantity | 10,000 | 10,000 | 10,000 | 10,000 | 5 |
| Accumulated number of groups per app | Unlimited | Unlimited | Unlimited | See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) | 5 |

>
>- For all group types, the total number of groups that can be created is unlimited. However, if you create more than 100,000 groups, you will need to pay certain fees. For more information, see [Fees for usage exceeding the free quota -> Peak group count](https://intl.cloud.tencent.com/document/product/1047/34350#.E5.A5.97.E9.A4.90.E5.A4.96.E8.B6.85.E9.87.8F.E8.B4.B9.E7.94.A8). We recommend that you disband the groups that are no longer needed in a timely manner.
>- For private groups, public groups, and chat rooms, the actual group member limit depends on purchased items. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). For example, if you purchased the Pro Edition, then any of all three group types can have up to 200 members. However, if you purchased an extra **increase member limit to 6,000** item, then the maximum numbers of members become 200, 2,000, and 6,000 respectively.
>- The net increase in group quantity is obtained by subtracting disbanded groups from created groups.
>- The maximum daily net increase in group quantity of 10,000 refers to the total net increase across all group types.



### Differences in message management

| Item | Private Group | Public Group | Chat Room | Audio-and-Video Chat Room | Broadcasting Chat Room |
|--- |--- |--- |--- |--- |--- |
| Who can send messages | App admin and all group members | App admin and all group members | App admin and all group members | Any account in the app that has been imported into IM | App admin |
| Group members can view messages from before they joined the group | No | No | Yes | No | No |
| Member change notifications are supported | Yes | Yes | No | Yes | No |
| A message must be sent to activate a new group | Yes | No | No | No | No |
| Admins can mute group members | No | Yes | Yes | Yes | No |
| Default message receiving option | Receive online and offline push messages | Receive online and offline push messages | Receive only online push messages | Receive only online push messages | Receive only online push messages |
| Unread message counting is supported | Yes | Yes | No | No | No |
| Users can receive group messages as guests without logging in | No | No | No | Yes | Yes |
| Message roaming is supported | Yes | Yes | Yes | No | No |

>
>- For a group that requires activation, before the group owner sends a message, the group is inactive and invisible to all group members except the group owner. A group that does not require activation is visible to all group members once it is created.
>- Muted group members cannot send group chat messages. In a broadcasting chat room, only the app admin is allowed to send messages, and therefore muting is not supported.
>- Currently, offline push is available only on Android (Android offline push) and iOS (APNs push) platforms.
>- Currently, message roaming is only available to private groups, public groups, and chat rooms, with messages stored for 7 days by default. If you need a longer storage period, change the message roaming period value in the [console](https://console.cloud.tencent.com/im). Increasing the message roaming period is a value-added service. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).


### Differences in batch import and automatic repossession

| Item | Private Group/Public Group/Chat Room | Audio-and-Video Chat Room/Broadcasting Chat Room |
|--- |--- |--- |
| Importing groups, group members, and group messages is allowed | Yes. It is allowed when historical groups are migrated from a third-party platform to IM. | No. Only existing groups, group members, and group messages can be used. |
| Time before a group is automatically repossessed (in seconds) | The backend does not repossess groups, unless the group owner disbands the group or all members quit the group. | The backend does not repossess groups, unless the group owner disbands the group or all members quit the group. |

> To enable group repossession, submit a ticket based on ticket templates. After configuration, inactive groups will be removed. An inactive group is one in which no message has been sent and no member change has occurred.

## Group Data Structure
### Basic group information

| Field Name | Type | Description | Notes |
|--- |--- |--- |--- |
| GroupId | String | Unique identifier of the group | Read-only<br>The ID of the group, which must be unique in the app. The prefix is @TGS#, and custom group IDs can also be used in the app. |
| Type | String | Group type | Read-only<br>Five group types are supported by default: private group, public group, chat room, audio-and-video chat room, and broadcasting chat room. For more information, see the preceding introduction to group types. |
| Name | String | Name of the group | This can be read and written with a length up to 30 bytes, but cannot be adjusted. |
| Introduction | String | Introduction of the group | This can be read and written with a length up to 240 bytes, but cannot be adjusted. |
| Notification | String | Group announcement | This can be read and written with a length up to 300 bytes, but cannot be adjusted. |
| FaceUrl | String | URL of the group’s profile photo | This can be read and written with a length up to 100 bytes, but cannot be adjusted. |
| Owner_Account | String | ID of the group owner | Read-only |
| CreateTime | Integer | Creation time of the group | Read-only |
| InfoSeq | Integer | This value increases every time the group information changes. | Read-only |
| LastInfoTime | Integer | Time of the last change to group information | Read-only |
| LastMsgTime | Integer | Time of the last message in the group chat | Read-only |
| NextMsgSeq | Integer | Seq of the next message in the group chat | Read-only.<br>Every message in the group chat has a unique message Seq. Seq values are continuous based on the sequence of sent messages. With every message sent in the group chat, NextMsgSeq (starting from 1) increments by 1. |
| MemberNum | Integer | Number of current members | Read-only |
| MaxMemberNum | Integer | Maximum number of members | - |
| ApplyJoinOption | String | Membership application option | Three options are available. DisableApply: disallow any application. NeedPermission: group owner or admin approval is required. FreeAccess: can join the group freely without prior approval. |

> The permissions to modify the group name, introduction, announcement, and profile photo URL are described as follows. In a private group, any member can modify them. In a public group or chat room, the group admins, group owner, and app admin are authorized to modify them. In a live broadcasting chat room, the group owner and app admin are authorized to modify them. In a broadcasting chat room, only the app admin is authorized to modify them.

### Group member profiles

| Field Name | Type | Description | Notes |
|--- |--- |--- |--- |
| Member_Account | String | Group member ID | Read-only |
| Role | String | Role in the group | A group has the following roles: Owner (group owner), Admin (group admin), and Member (group member). |
| JoinTime | Integer | Time of joining the group | Read-only |
| MsgSeq | Integer | Current read message Seq of the member | Read-only |
| MsgFlag | String | Message receiving option | Three options are available. AcceptAndNotify: receive and notify. AcceptNotNotify: receive without notifying (APNs remote push is not triggered). Discard: block group messages (messages are not pushed to clients.) |
| LastSendMsgTime | Integer | Time of sending the last message | Read-only |
| NameCard | String | Group name card | Readable and writable |

## Customizing Group Types

In practice, if you need more than the [five group types](https://intl.cloud.tencent.com/document/product/1047/33529) provided by IM, you can prepare related information based on ticket templates and [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to modify existing group types or create new group types.
For example, you can create a group that is used in an office environment. This group is similar to a public group, but every member has the highest level of management permissions and can view messages from before they joined the group. In this case, you can:
- Choose the public group type and [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to enable the **view historical messages before joining** and **allow ordinary members to remove members** options.
- [Submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for a new group type named OAGroup. Specify public group (Public) as the reference type and enable the **view historical messages before joining** and **allow ordinary members to remove members** options.  

> When creating a new group type, you must specify a default group type as a reference. Note that the broadcasting chat room (BChatRoom) type cannot be specified as the reference.
> After configuration, the new group type will have new features that are specified in the ticket, and the same features as the referenced group type.

## Customizing Group IDs

When a group is created in the app, IM assigns a default group ID to the new group by default. This default group ID starts with @TGS# and is unique in the app.
IM also allows you to customize group IDs that are simple and easy to remember and communicate. A custom group ID must be a string of ASCII characters (0x20-0x7e) with a length less than 48 bytes. Do not use @TGS# as the prefix to avoid confusion with assigned group IDs.

## Customizing Fields

IM allows you to configure up to 20 group-level custom fields and 5 member-level custom fields based on your business needs. With custom fields, apps can attach additional data to groups and read and write through existing APIs. Note that custom fields cannot be deleted once created and applied.

### Description

Custom fields have the following characteristics:

1. Their values are expressed in key-value format.
2. Key is a string with a length less than 16 bytes. Its name contains only uppercase and lowercase letters, numbers, and underscores.
3. Value is a buffer customized by the user, which can be binary data. Group-level values have a maximum length of 512 bytes, while member-level values have a maximum length of 64 bytes
4. You can configure the least read permission and the least write permission for each Key.

The read and write permissions of a custom field are listed as follows, from high to low:

1. Readable and writable by the app admin.
2. Readable and writable by the group owner.
3. Readable and writable by the group admin.
4. Readable and writable by group members.
5. Readable and writable by anyone, including non-members.

For example, assume that an app needs to extend the GroupLevel field for groups and the value of this field is a number representing the level of a group. If this level information is calculated by the app backend, then the least write permission should be **writable by the app admin**. If the field is part of the public profile of the group, its least read permission should be **readable by anyone, including non-members**.

If the value to be stored is a number, we recommend C and C++ developers to store it as a string instead of binary data. For example, when the number to be stored is 1, store it as string **1** instead of binary data **0x01**. In the future, IM will offer more operations for custom fields, such as specific mathematical operations, which will be performed on the basis of string-type numbers.

### Configuration method

Custom fields at these two levels can be configured in IM Console.
To configure member-level custom fields, you need to specify the group type based on which to add custom fields. However, AVChatRoom, BChatRoom, and custom group types that are configured based on them do not support custom fields at the group member level, because these types of groups do not store member profiles.
The **self read and write permissions** indicate whether members can read and write their own member-level custom fields. For example, assume that a member-level customer field named **MemberLevel** is present, which represents the level of a member level in a group. Generally, group members can read but not modify their own levels, and therefore their **self read and write permissions** are set to **readable but unwritable**.

## Customizing Callbacks

Third-party callback is an important method to meet the special needs of apps. It provides users with the capability to customize actions.
IM’s group system supports different callbacks. For more information, see [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354) and the [List of Callback Commands](https://intl.cloud.tencent.com/document/product/1047/34355).
