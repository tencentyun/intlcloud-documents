## Group Types

- **Work group (Work)**: after a work group is created, users can join the group only after being invited by group members. The invitation does not need to be accepted by the invitee or approved by the group owner. This group type is the same as private group (Private) in earlier versions.
- **Public group (Public)**: after a public group is created, the group owner can designate group admins. To join the group, a user needs to search for the group ID and send a request, and the request needs to be approved by the group owner or an admin before the user can join the group.
- **Meeting group (Meeting)**: allows users to join and leave freely and view historical messages sent before they join the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio/video conferencing and online education. This group type is the same as chat room (ChatRoom) in earlier versions.
- **Community group (Community)**: allows users to join and exit freely and is ideal for ultra-large community group chat scenarios, such as knowledge sharing and game communication
- **Audio-video group (AVChatRoom)**: allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Cloud Streaming Services (CSS) to support on-screen comment chat scenarios.



The following table describes the features and limitations of each group type:

<table>
  <tr>
    <th width="20%">Feature</th>
    <th width="16%">Work Group (Work)</th>
    <th width="16%">Public Group (Public)</th>
    <th width="16%">Meeting Group (Meeting)</th>
    <th width="16%">Community Group (Community)</th>
    <th>Audio-Video Group (AVChatRoom)</th>
  </tr>
  <tr>
    <td>Available member roles</td>
    <td>Group owner and ordinary member</td>
    <td>Group owner, group admin, and ordinary member</td>
    <td>Group owner, group admin, and ordinary member</td>
    <td>Group owner, group admin, and ordinary member</td>
    <td>Group owner and ordinary member</td>
  </tr>
  <tr>
    <td>Requesting to join a group</td>
    <td>Not supported</td>
    <td>Supported with group owner or group admin approval required</td>
    <td>Supported with no approval required</td>
    <td>Supported with no approval required</td>
    <td>Supported with no approval required</td>
  </tr>
  <tr>
    <td>Joining group via invitation by a member</td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td>Group owner quitting group</td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td>Who can modify group profile</td>
    <td>Any group member</td>
    <td>Group owner and group admin</td>
    <td>Group owner and group admin</td>
    <td>Group owner and group admin</td>
    <td>Group owner</td>
  </tr>
  <tr>
    <td>Who can kick group members out of group</td>
    <td>Group owner</td>
    <td colspan="3">Group owner and group admin. Group admin can only remove ordinary group members.</td>
    <td>Group members cannot be removed. The same effect can be achieved by muting members.</td>
  </tr>
  <tr>
    <td>Who can mute members</td>
    <td>Muting members is not supported</td>
    <td colspan="3">Group owner and group admin.
      Group admin can only mute ordinary group members.</td>
    <td>Group owner</td>
  </tr>
  <tr>
    <td>Unread count</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td>Viewing message history earlier than user's entry time</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
  	<td>Retaining message history in the cloud</td>
  	<td colspan="4"><ul style="margin:0;padding-left:10px" ><li>Trial Edition: 7 days</li><li>Pro Edition: 7 days by default, up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: 30 days by default, up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
  <td>Not supported</td>
  </tr>
  <tr>
  <td>Number of groups</td>
  <td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: up to 100 existing groups, and deleted groups do not count against the quota.</li><li>Pro Edition or Flagship Edition: unlimited</li></ul></td>
  <td><ul style="margin:0;padding-left:10px"><li>Trial Edition and Pro Edition: not supported</li><li>Flagship Edition: 100,000</li></ul></td>
  <td><ul style="margin:0;padding-left:10px"><li>Trial Edition: up to 10 existing groups, and deleted groups do not count against the quota.</li><li>Pro Edition: up to 50 existing groups, and deleted groups do not count against the quota.<br>You can upgrade to unlimited number of audio-video groups by purchasing the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a>.</li><li>Flagship Edition: unlimited</li></ul></td>
  </tr>
  <tr>
  <td>Number of group members</td>
  <td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: 20 per group</li><li>Pro Edition: 200 per group by default, can be increased to 2,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: 2,000 per group, can be increased to 6,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
  <td>100,000</td>
  <td>Unlimited number of group members</td>
  </tr>
</table>

>?
>- Group types are upgraded in the new SDK version and they are **work group (Work)**, **public group (Public)**, **meeting group (Meeting)**, **community group (Community)**, and **audio-video group (AVChatRoom)**. Private group (Private) and chat room (ChatRoom) in earlier versions (which have Public, Private, ChatRoom, and AVChatRoom groups) correspond to work group (Work) and meeting group (Meeting) in the new version respectively.
>- In the Pro Edition or Flagship Edition SDKAppID, the maximum net increase in group count per day is 10,000 for all group types. Free peak group count is 100,000 per month, and you will need to pay for [usage not covered by the free quota](https://intl.cloud.tencent.com/document/product/1047/34350).
>- The community group (Community) feature is supported only in SDK 5.8.1668 enhanced edition or higher. To use the feature, you need to purchase the Flagship Edition package and [apply for activation](https://intl.cloud.tencent.com/document/product/1047/44322).
>- Work groups (Work) and public groups (Public) do not allows group members to view messages sent before they join the group. To enable the feature, submit a change request by referring to [Configuration Change Ticket](https://intl.cloud.tencent.com/document/product/1047/44322).

## Creating a Group

If you want to initialize group information (for example, group introduction, group profile photo, and initial group members) when creating a group, call the [GroupCreate](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupCreate.html) API. For parameter details, see [CreateGroupParam](https://comm.qq.com/im/doc/unity/en/types/GroupsAttributes/CreateGroupParam.html).

```c#
TencentIMSDK.GroupCreate(CreateGroupParam,(int code, string desc, string json_param, string user_data)=>{

})
```

## Joining a Group

The processes for joining groups of different types are described as follows:

| Type              | Work Group (Work)                        | Public Group (Public)                                                     | Meeting Group (Meeting)                   | Community Group (Community)               | Audio-Video Group (AVChatRoom)            |
| :---------------- | :--------------------------------------- | :------------------------------------------------------------------------ | :---------------------------------------- | :---------------------------------------- | :---------------------------------------- |
| How to join group | Users must be invited to join the group. | users join the group after requests are approved by group owner or admin. | Users can join and quit the group freely. | Users can join and quit the group freely. | Users can join and quit the group freely. |

### Scenario 1: users can join and quit the group freely

Meeting groups (Meeting) and audio-video groups (AVChatRoom) can be used for interactive scenarios where users join and exit groups frequently, such as online conferencing and show live streaming. The group joining procedure is therefore the simplest.

After a user successfully joins a group by calling [GroupJoin](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupJoin.html), all group members (including the joined user) receive the [GroupTipsEventCallback](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html) callback.

### Scenario 2: users must be invited to join the group

Resembling WeChat and WeCom groups, work groups (Work) are suitable for communication in work environments. The interaction pattern is designed to disable proactive group joining and only allows users to be invited to join the group by group members.

A group member calls [GroupInviteMember](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupInviteMember.html) to invite a user to join the group, then all group members (including the inviter) receive the [GroupTipsEventCallback](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html) callback.

### Scenario 3: users join the group after requests are approved

Public groups (Public) are similar to the interest groups and tribes in QQ. Any user can request to join the group, but will not become a member of the group until the request is approved by the group owner or admin. While approval is required by default, the group owner or admin can call the [GroupModifyGroupInfo](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyGroupInfo.html) API to set the group joining option ([TIMGroupAddOption](https://comm.qq.com/im/doc/unity/en/enums/TIMGroupAddOption.html)) to **forbid anyone to join**, which is tighter, or to **disable the approval process**, which is more flexible.

- kTIMGroupAddOpt_Forbid: forbid anyone to join the group.
- kTIMGroupAddOpt_Auth (default): group owner or admin approval is required for group joining.
- kTIMGroupAddOpt_Any: disable the approval process to allow any user to join the group.

## Quitting a group

Call [GroupQuit](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupQuit.html) to quit a group. Then all group members receive the [GroupTipsEventCallback](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html) callback.

>!For a public group (Public), meeting group (Meeting), community group (Community), or audio-video group (AVChatRoom), the group owner is not allowed to quit the group but can delete the group.

## Deleting Groups

Call [GroupDelete](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupDelete.html) to delete a group. Then all group members receive the [GroupTipsEventCallback](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html) callback.

>!
>- For a public group (Public), meeting group (Meeting), community group (Community), or audio-video group (AVChatRoom), the group owner can delete the group at any time.
>- For a work group (Work), the group owner does not have the permission to delete the group. To delete the group, you must have your service server call the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34896).

## Getting the List of Joined Groups

Call [GroupGetJoinedGroupList](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupGetJoinedGroupList.html) to get a list of work groups (Work), public groups (Public), meeting groups (Meeting), and community groups (Community) the current user has joined. Audio-video groups (AVChatRoom) will not be included in this list.

## Group Profiles and Group Settings

### Getting group profiles

Call [GroupGetGroupInfoList](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupGetGroupInfoList.html) to get the group profile of one or more groups at a time. To get the group profiles of multiple groups by a single call, pass in multiple `groupID` at a time.

### Modifying group profiles

Call [GroupModifyGroupInfo](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyGroupInfo.html) to modify the group profile. When the modification is completed, all group members receive the [GroupTipsEventCallback](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html) callback.

>?
>- For work groups (Work), all group members can modify the basic group profile.
>- For public groups (Public), meeting groups (Meeting), and community groups (Community), only the group owner and admin can modify the group profile.
>- For audio-video groups (AVChatRoom), only the group owner can modify the group profile.

## Setting the Group Message Receiving Option

Any group member can call the [MsgSetGroupReceiveMessageOpt](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSetGroupReceiveMessageOpt.html) API to modify the group message receiving option. Available group message receiving options are as follows:

- TIMReceiveMessageOpt.kTIMRecvMsgOpt_Receive: messages will be received when the user is online, and push notifications will be received when the user is offline.
- TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive: no group messages will be received.
- TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Notify: messages will be received when the user is online, and no push notification will be received when the user is offline.

## FAQs

### 1. Can an audio-video group (AVChatRoom) continue to receive messages after it was disconnected and then reconnected?

Yes, but since an audio-video group (AVChatRoom) does not support storing message history in the cloud, it cannot pull the messages that were sent when it was disconnected.

### 2. Why doesn’t the group receive notifications when a user joins or quits the group?

Verify the group type:
- Meeting group (Meeting) does not support member change notifications.
- An audio-video group (AVChatRoom) can receive up to 40 messages per second, therefore it prioritizes the receiving and sending of high-priority messages and discards messages with the lowest priority first once the frequency limit is exceeded.

### 3. Why does the unread count of a meeting group (Meeting) remain at 0?

Meeting groups (Meeting) and audio-video groups (AVChatRoom) are designed for conference and live streaming scenarios respectively, and they do not support the unread count feature.
