[](id:type)
## Group Types
Instant Messaging (IM) supports the following group types:
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
>- Group types are **work group (Work)**, **public group (Public)**, **meeting group (Meeting)**, **Community group (Community)**, and **audio-video group (AVChatRoom)**. Private group (Private) and chat room (ChatRoom) in earlier versions (which have Public, Private, ChatRoom, and AVChatRoom groups) correspond to work group (Work) and meeting group (Meeting) in the new version respectively.
>- In the Pro Edition or Flagship Edition SDKAppID, the maximum net increase in group count per day is 10,000 for all group types. Free peak group count is 100,000 per month, and you will need to <a href="https://intl.cloud.tencent.com/document/product/1047/34350"> pay for usage not covered by the free quota</a>.
>- The community group (Community) feature is supported only in SDK 5.8.1668 enhanced edition or higher. To use the feature, you need to purchase the Flagship Edition package and [apply for activation](https://intl.cloud.tencent.com/document/product/1047/44322).
>- Work groups (Work) and public groups (Public) do not allows group members to view messages sent before they join the group. To enable the feature, submit a change request by referring to [Configuration Change Ticket](https://intl.cloud.tencent.com/document/product/1047/44322).


## Group Management
[](id:create)
### Creating a group
#### Simple API (disused after v3.6.0)
 The simple API [createGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/createGroup.html) for group creation is disused after v3.6.0. Please use the advanced API for group creation in `groupManager` instead.

#### Advanced API
If you want to initialize group information (for example, group introduction, group profile photo, and initial group members) when creating a group, call the [createGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/createGroup.html) API in the `V2TIMGroupManager` management class. The `V2TIMGroupManager` management class can be obtain via `TencentImSDKPlugin.v2TIMManager.getGroupManager()`.


```dart
// Sample code: create a work group using the advanced createGroup API 
   List<V2TimGroupMember> list = [];
    for (String userID in memberList) {
      list.add(V2TimGroupMember(userID: userID, role: 200));
    }
    V2TimValueCallback<String> res =
        await TencentImSDKPlugin.v2TIMManager.getGroupManager().createGroup(
              groupType: "Work", // Work group
              groupName: "groupName",
              groupID: groupID, 
              notification: "notification", // Group notification
              introduction: introduction, // Group introduction
              isAllMuted: false, // Whether to mute all group members
              faceUrl: "...",
              addOpt: GroupAddOptTypeEnum.V2TIM_GROUP_ADD_ANY, // Permission to add a group
              memberList: list, // Members added during group creation
            );
```


- The value of `groupType` is a string and can be one of `Work`, `Public`, `Meeting`, `Community`, and `AVChatRoom`. To learn about the differences among group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` in a SDKAppID. If you set `groupID` to null, you will be assigned a group ID by default.
- `groupName` specifies the group description, which has a maximum length of 30 bytes.

[](id:join)
### Joining a group
The processes for joining groups of different types are described as follows:

| Type              | Work Group (Work)                        | Public Group (Public)                                                     | Meeting Group (Meeting)                   | Community Group (Community)               | Audio-Video Group (AVChatRoom)            |
| ----------------- | ---------------------------------------- | ------------------------------------------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| How to join group | Users must be invited to join the group. | users join the group after requests are approved by group owner or admin. | Users can join and quit the group freely. | Users can join and quit the group freely. | Users can join and quit the group freely. |

#### Scenario 1: users can join and quit the group freely
Meeting groups (Meeting) and audio-video groups (AVChatRoom) can be used for interactive scenarios where users join and exit groups frequently, such as online conferencing and show live streaming. The group joining procedure is therefore the simplest.

After a user successfully joins a group by calling [joinGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/joinGroup.html), all group members (including the joined user) receive the [onMemberEnter](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberEnterCallback.html) callback. 

#### Scenario 2: users must be invited to join the group
Resembling WeChat and WeCom groups, work groups (Work) are suitable for communication in work environments. The interaction pattern is designed to disable proactive group joining and only allows users to be invited to join the group by group members.

A group member calls [inviteUserToGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/inviteUserToGroup.html) to invite a user to group, then all group members (including the inviter) receive the [onMemberInvited](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberInvitedCallback.html) callback.

#### Scenario 3: users join the group after requests are approved
Public groups (Public) are similar to the interest groups and tribes in QQ. Any user can request to join the group, but will not become a member of the group until the request is approved by the group owner or admin. While approval is required by default, the group owner or admin can call the [setGroupInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html) API to set the group joining option (`GroupAddOptType`) to **forbid anyone to join**, which is tighter, or to **disable the approval process**, which is more flexible.
- GroupAddOptTypeEnum.V2TIM_GROUP_ADD_FORBID: forbid anyone to join the group.
- GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH (default): group owner or admin approval is required for group joining.
- GroupAddOptTypeEnum.V2TIM_GROUP_ADD_ANY: disable the approval process to allow any user to join the group.

The following diagram illustrates the process of group joining that requires approval:
![](https://main.qcloudimg.com/raw/9164de02268e14b178937bbd85465f4f.png)

1. **The user sends a request to join the group**
The user calls [joinGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/joinGroup.html) to request to join the group.
2. **The group owner or admin processes the group joining request**
After receiving the [onReceiveJoinApplication](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveJoinApplicationCallback.html) callback, the group owner or admin calls the [getGroupApplicationList](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupApplicationList.html) API to get the list of group joining requests, and accepts or rejects a request with [acceptGroupApplication](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/acceptGroupApplication.html) or [refuseGroupApplication](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/refuseGroupApplication.html).
3. **The user receives the result**
 The user receives the [onApplicationProcessed](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnApplicationProcessedCallback.html) callback in [V2TimGroupListener](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Listener/V2TimGroupListener.html). If `isAgreeJoin` is `true`, the request is accepted. Otherwise, the request is rejected. If the request is accepted, all members (including the requester) receive the [onMemberEnter](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberEnterCallback.html) callback.



[](id:quit)
### Quitting a group
Call [quitGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/quitGroup.html) to quit a group. The user who quits the group then receives the [onQuitFromGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnQuitFromGroupCallback.html) callback and other group members receive the [onMemberLeave](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberLeaveCallback.html) callback.
>?For a public group (Public), meeting group (Meeting), community group (Community), or audio-video group (AVChatRoom), the group owner is not allowed to quit the group but can [delete the group](#dismiss).

[](id:dismiss)
### Deleting a group
Call [dismissGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/dismissGroup.html) to delete a group. Then all group members receive the [onGroupDismissed](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGroupDismissedCallback.html) callback.

>?
>- For a public group (Public), meeting group (Meeting), community group (Community), or audio-video group (AVChatRoom), the group owner can delete the group at any time.
>- For a work group (Work), the group owner does not have the permission to delete the group. To delete the group, you must have your service server call the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34896).


### Getting the list of joined groups
Call [getJoinedGroupList](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getJoinedGroupList.html) to get a list of work groups (Work), public groups (Public), meeting groups (Meeting), and community group (Community) the current user has joined. Audio-video groups (AVChatRoom) will not be included in this list.

## Group Profiles and Group Settings
### Getting group profiles
Call [getGroupsInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getJoinedGroupList.html) to get the group profile of one or more groups at a time. To get the group profiles of multiple groups by a single call, pass in multiple `groupID` at a time.

### Modifying group profiles
Call [setGroupInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html) to modify the group profile. When the modification is complete, all group members receive the [onGroupInfoChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGroupInfoChangedCallback.html) callback.
>?
> - For work groups (Work), all group members can modify the basic group profile.
> - For public groups (Public), meeting groups (Meeting), and community groups (Community), only the group owner and admin can modify the group profile.
> - For audio-video groups (AVChatRoom), only the group owner can modify the group profile.

```dart
// Sample code: modify group profile
 V2TimCallback res =
        await TencentImSDKPlugin.v2TIMManager.getGroupManager().setGroupInfo(
              info: V2TimGroupInfo.fromJson(  // Pass in the V2TimGroupInfo type
                {
                  "groupID": : "ID of the group for which you want to modify the group profile",
                  "groupName": "Name of the group for which you want to modify the group profile",
                  "groupType": "Work",
                  "notification": "notification",
                  "introduction": "introduction",
                  "faceUrl": faceUrl,
                  "isAllMuted": false,
                  "addOpt": GroupAddOptType.V2TIM_GROUP_ADD_ANY,
                  "customInfo": Map(),
                },
              ),
            );
```

### Setting the group message receiving option
Any group member can call the [setGroupReceiveMessageOpt](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/setGroupReceiveMessageOpt.html) API to modify the group message receiving option. Available group message receiving options are as follows:
- ReceiveMsgOptEnum.V2TIM_RECEIVE_MESSAGE: messages will be received when the user is online, and push notifications will be received when the user is offline.
- ReceiveMsgOptEnum.V2TIM_NOT_RECEIVE_MESSAGE: no group messages will be received.
- ReceiveMsgOptEnum.V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE: messages will be received when the user is online, and no push notification will be received when the user is offline.

The group message receiving option allows you to mute group messages:
- **No group message will be received**
With the group message receiving option set to `ReceiveMsgOptEnum.V2TIM_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.
- **Group messages will be received but the user will not be notified. A badge without the unread count will be displayed on the conversation list interface**
>?This mode requires the unread count feature and therefore it applies only to work groups (Work) and public groups (Public).
>
With the group message receiving option set to `ReceiveMsgOptEnum.V2TIM_RECEIVE_MESSAGE`, when new group messages are received and the conversation list needs to be updated, you can get the unread count through [unreadCount](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#unreadcount). Use [recvOpt](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html#recvopt) to verify that a red dot instead of the unread count is displayed when the group message receiving option is `ReceiveMsgOptEnum.V2TIM_RECEIVE_MESSAGE`.

## Group Attributes (Custom Group Fields)
New custom group fields, also called group attributes, are designed. They have the following features:
1. You can CRUD group attributes in the client instead of console.
2. You can configure up to 16 group attributes. The size of each group attribute can be up to 4 KB, and the total size of all group attributes can be up to 16 KB.
3. Only audio-video groups (AVChatRoom) support group attributes.
4. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs each can be called by the SDK for up to 10 times per 5 seconds, and the 8511 error code will be called back if the limit is exceeded. The APIs each can be called by the backend for up to 5 times per second, and the 10049 error code will be called back if the limit is exceeded.
5. The `getGroupAttributes` API can be called by the SDK for up to 20 times per 5 seconds.

With group attributes, you can manage the seats of audio chat rooms. When a user mics on, you can set a group attribute to manage the information of the user. When the user mics off, you can delete the group attribute. Other members can get the list of group attributes to display the seat list.

### Initializing group attributes
Call the [initGroupAttributes](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/initGroupAttributes.html) API to initialize group attributes. If the group has existing group attributes, they will be deleted first.

### Setting group attributes

Call the [setGroupAttributes](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupAttributes.html) API to set group attributes. If the group attributes to set do not exist, they will be automatically added.

### Deleting group attributes
Call the [deleteGroupAttributes](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/deleteGroupAttributes.html) API to delete specified group attributes. If you set the `keys` field to `null`, all group attributes will be deleted.

### Getting group attributes
Call the [getGroupAttributes](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupAttributes.html) API to get specified group attributes. If you set the `keys` field to `null`, all group attributes will be returned.

### Updating group attributes
If any group attribute is updated, all group attribute fields will be called back via [onGroupAttributeChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGroupAttributeChangedCallback.html).

## Group Member Management
### Getting the group member list
Call [getGroupMemberList](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html) to get the list of group members of a given group. The list contains profile information about individual members, such as user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining group (`joinTime`).
As a group might have a large number of members (for example, 5,000+), this API supports two advanced attributes: `filter` and `nextSeq`.

#### Filters
When calling the [getGroupMemberList](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html) API, you can specify `filter` to pull the information of certain roles.

| Filter                                                     | Description                                         |
| ---------------------------------------------------------- | --------------------------------------------------- |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ALL    | Pull the information list of all group members      |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_OWNER  | Pull the information list of the group owner        |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN  | Pull the information list of the group admin        |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of ordinary group members |

```dart
// Sample code: pull the profile of the group owner using the filter parameter
 await TencentImSDKPlugin.v2TIMManager
            .getGroupManager()
            .getGroupMemberList(
              groupID: "Your groupId",
              filter: GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_OWNER,
              nextSeq: "0",
            );
```

#### Pulling paginated results with nextSeq
In many cases, it makes more sense for the user interface to display the first page of the group member list instead of the complete list. More group members can be pulled when the user clicks **Next Page** or pull the list to refresh. For this scenario, you can apply the method of pulling paginated results.

The [getGroupMemberList](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html) API returns a maximum of 50 members at a time. You can use the pagination flag `nextSeq` to pull the paginated group member list. In the first attempt to pull the group member list, enter 0 for `nextSeq`. When the first pull succeeds, `getGroupMemberList`'s callback result [V2TIMGroupMemberInfoResult](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberInfoResult.html) contains the [nextSeq](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberInfoResult.html#nextseq) field.
- If [nextSeq](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberInfoResult.html#nextseq) returns 0, the complete group member list has been pulled.
- If [nextSeq](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberInfoResult.html#nextseq) returns a value greater than 0, there remains group member information to be pulled. You can then decide whether to make another call to pull group member information based on the user's action on the UI. In the second pull, you need to pass the [nextSeq](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberInfoResult.html) in `V2TIMGroupMemberInfoResult` returned from the previous pull as parameter to the [getGroupMemberList](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html) API.

```dart
// Sample code: pull the paginated group member list using nextSeq
  String nextSeq = "0";
  getGroupMemberList(String nextSeq) async {
    V2TimValueCallback<V2TimGroupMemberInfoResult> res =
        await TencentImSDKPlugin.v2TIMManager
            .getGroupManager()
            .getGroupMemberList(
              groupID: "Your groupId",
              filter: GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ALL,
              nextSeq: nextSeq,
            );
    setState(() {
      resData = res.toJson();
      if (res.data != null) {
        nextSeq = res.data!.nextSeq!;
		// ...
      }
    });
  }
```


### Getting group member profiles
Call [getGroupMembersInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMembersInfo.html) to get the profile of group members in batches. You can pass in multiple `userID` at a time to improve network transmission efficiency.

### Modifying group member profiles
The group owner or admin can call the [setGroupMemberInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupMemberInfo.html) API to modify the group-related information of members, including the group name card (`nameCard`), group member role (`role`), muting duration (`muteUntil`), and custom fields.

[](id:mute)
### Muting group members
The group owner or admin can mute a group member and set muting duration (in seconds) via [muteGroupMember](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html). Muting information is stored in the [muteUtil](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberFullInfo.html#muteuntil) attribute field of the group member. After the group member is muted, all group members (including the muted member) receive the [onMemberInfoChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberInfoChangedCallback.html) event callback.
The group owner or admin can mute the entire group via the [setGroupInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html) API by setting the [isAllMuted](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html#isallmuted) attribute field to `true`. There is no time limit for group muting. The group can be unmuted through `setAllMuted(false)` in the group profile.


[](id:kick)
### Removing group members
The group owner or admin can call the [kickGroupMember](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/kickGroupMember.html) API to remove a group member. As an audio-video group (AVChatRoom) can have unlimited members, it does not support the API. You can use [muteGroupMember](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html) to achieve the same effect instead.
After the member is removed, all group members (including the kicked member) receive the [onMemberKicked](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberKickedCallback.html) callback.

### Changing group member roles
The group owner can call [setGroupMemberRole](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupMemberRole.html) to change the role of a member of a public group (Public) or meeting group (Meeting). Roles available for changing are ordinary member and group admin.
- After a member is set as group admin, all group members (including the new admin) receive the [onGrantAdministrator](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGrantAdministratorCallback.html) callback.
- After the admin role is removed for a member, all group members (including the member with admin role removed) receive the [onRevokeAdministrator](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnRevokeAdministratorCallback.html) callback.

[](id:transfer)
### Transferring a group
The group owner can call [transferGroupOwner](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/transferGroupOwner.html) to transfer the ownership of group to other group members.
After the group ownership is transferred, all group members receive the [onGroupInfoChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGroupInfoChangedCallback.html) callback, where the type of `V2TIMGroupChangeInfo` is `GroupChangeInfoType.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

## FAQs

### 1. Can an audio-video group (AVChatRoom) continue to receive messages after it was disconnected and then reconnected?
Yes, but since an audio-video group (AVChatRoom) does not support storing message history in the cloud, it cannot pull the messages that were sent when it was disconnected.

### 2. Why doesn’t the group receive notifications when a user joins or quits the group?
Verify the group type:
- Meeting group (Meeting) does not support member change notifications.
- An audio-video group (AVChatRoom) can receive up to 40 messages per second, therefore it prioritizes the receiving and sending of high-priority messages and discards messages with the lowest priority first once the frequency limit is exceeded.

### 3. Why does the unread count of a meeting group (Meeting) remain at 0?
Meeting groups (Meeting) and audio-video groups (AVChatRoom) are designed for conference and live streaming scenarios respectively, and they do not support the unread count feature.
