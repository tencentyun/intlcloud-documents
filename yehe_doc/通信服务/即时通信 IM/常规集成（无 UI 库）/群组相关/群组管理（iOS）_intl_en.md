<span id="type"> </span>
## Group Types
Instant Messaging (IM) supports four group types. The following table describes the general characteristics and limitations of each group type:

| Type | Work Group (Work) | Social Networking Group (Public) | Temporary Meeting Group (Meeting) | Live Streaming Group (AVChatRoom) |
|---------|---------|---------|---------|---------|
| Scenario | Similar to an ordinary WeChat group. After a Work group is created, a user can only join the group by being invited by a friend who is a member of the group. The invitation does not need to be accepted by the invitee or approved by the group owner. | Similar to a QQ group. After a Public group is created, a user can join the group by sending an application or being invited by a group member. The invitation needs to be both accepted by the invitee and approved by the group owner or group admin. | Allows users to join and leave freely and allows members to view messages from before they joined the group. Meeting groups are ideal for scenarios that use Tencent Real-Time Communication (TRTC), such as audio-and-video conferencing and online education. | Allows users to join and leave freely, supports an unlimited number of members, and does not store the message history. AVChatRoom groups can be used with Live Video Broadcasting (LVB) to support on-screen comments. (Note: the number of AVChatRoom groups that can be created is limited. For details, see your [standard billing plan](https://intl.cloud.tencent.com/document/product/1047/34350).) | Subject to the standard billing plan that you purchased. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). |
| Max number of group members | Subject to the standard billing plan that you purchased. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) | Subject to the standard billing plan that you purchased. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) | Subject to the standard billing plan that you purchased. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). | Unlimited |
| Group member roles | Group owner and ordinary member | Group owner, group admin, and ordinary member | Group owner, group admin, and ordinary member | Group owner and ordinary member |
| How to join the group | Must be invited by a group member | User joins the group after the application is approved by the group owner or group admin | User can join freely | User can join freely |
| Can members invite users to the group | Any member can initiate an invitation | No | No | No |
| Can the group owner exit the group | Yes | No | No | No |
| Who can modify basic group information | Any group member | Only the group owner and group admins | Only the group owner and group admins | Only the group owner |
| Who can remove members from the group | Only the group owner | Only the group owner and group admins | Only the group owner and group admins | Removal is not supported (use muting instead) |
| Who can mute members | Only the group owner | Only the group owner and group admins | Only the group owner and group admins | Only the group owner |
| Unread counting is supported | Yes | Yes | No | No |
| Message roaming is supported | Yes | Yes | Yes | No |
| Can members view messages from before they joined the group | No | No | Yes | No |

## Group Management
<span id="create"> </span>
### Creating a group
#### Simple API
You can quickly create a group by calling the [createGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989) API and specifying `groupType`, `groupID`, and `groupName`.

#### Advanced API
To initialize group information, such as the group introduction, group profile photo, and initial group members, when creating a group, call the [createGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c) API in the `V2TIMManager+Group.h` management class.

```
// Sample code for creating a Work group through the advanced createGroup API 
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupName = @"testWork";
info.groupType = @"Work";
NSMutableArray *memberList = [NSMutableArray array];
V2TIMCreateGroupMemberInfo *memberInfo = [[V2TIMCreateGroupMemberInfo alloc] init];
memberInfo.userID = @"vinson";
[memberList addObject:memberInfo];
[[V2TIMManager sharedInstance] createGroup:info memberList:memberList succ:^(NSString *groupID) {
    // Created the group successfully
} fail:^(int code, NSString *msg) {
    // Failed to create the group
}];
```

- The value of `groupType` is a string and can be "Work", "Public", "Meeting", or "AVChatRoom". To learn about the differences among group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` under the same SDKAppID. If you set `groupID` to nil, you will be assigned a group ID by default.
- `groupName` specifies the group description, whose maximum length is 30 bytes.

<span id="join"> </span>
### Joining a group
The group joining processes for different group types are described as follows:

| Type | Work Group (Work) | Social Networking Group (Public) | Temporary Meeting Group (Meeting) | Live Streaming Group (AVChatRoom) |
|---------|---------|---------|---------|---------|
| How to join the group | Must be invited by a group member | User joins the group after the application is approved by the group owner or group admin | User can join freely | User can join freely |

#### Scenario 1: users can join and exit the group freely
Meeting groups and AVChatRoom groups can be used for interactive scenarios where users join and exit the group frequently, such as online conferences and runway live streaming. Therefore, the joining procedure is very simple for these groups.

After a user successfully joins a group by calling [joinGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a), all group members (including the joined user) receive the [onMemberEnter](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#aed6a96e6b304863586a107c45ba33f11) callback. 

#### Scenario 2: users must be invited to the group
Similar to WeChat and WeChat Work groups, Work groups are suitable for communication in work environments. The interaction pattern is designed to deny active group joining and only allows users to be invited to a group by existing group members.

When a group member calls [inviteUserToGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a942d75fdea66e22cdbd8c131cf18e1ea) to invite a user to the group, all group members (including the inviter) receive the [onMemberInvited](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a6bff27f9f6859caefcaaf361b9c6fe68) callback.

#### Scenario 3: users join the group after applications are approved
Public groups are similar to the interest groups and tribes in QQ. Any user can apply to join the group, but will not become a member of the group until the application is approved by the group owner or group admin. While approval is required by default, the group owner or group admin can call the [setGroupInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) API to set the group joining option (`V2TIMGroupAddOpt`) to "forbid anyone to join" (which imposes stricter restrictions) or to "disable the approval process" (which loosens the restrictions).
- V2TIM_GROUP_ADD_FORBID: forbid anyone to join the group.
- V2TIM_GROUP_ADD_AUTH: (default) group owner or group admin approval is required for group joining.
- V2TIM_GROUP_ADD_ANY: disable the approval process to allow any user to join the group.

1. **The user sends an application to join the group.**
    The user calls [joinGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a) to apply to join the group.
2. **The group owner or group admin handles the group joining application.**
 After the [onReceiveJoinApplication](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a481ab06916795cc9445fa3fc465c69ab) callback is received, the group owner or group admin calls [getGroupApplicationList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a29c36ad685159850a30d61a6b9c637e8) to obtain the list of group joining applications and approves or rejects applications through [acceptGroupApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a51bb9b4f965cb3d01546fef348ac75e4) or [refuseGroupApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a46aa78c54986b2c0b7cc0012a3dc94ef).
3. **The applicant receives the application result.**
The user receives the [onApplicationProcessed](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a850a50e7ea6b86a2d28afa1a569245ca) callback in [V2TIMGroupListener](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html). If `isAgreeJoin` is `true`, the application was approved, otherwise the application was rejected. If the application was approved, all members (including the applicant) receive the [onMemberEnter](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#aed6a96e6b304863586a107c45ba33f11) callback.

<span id="quit"> </span>
### Exiting a group
Call [quitGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5) to exit a group. The user who exits the group then receives the [onQuitFromGroup](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a9d4a0c42366ea13f688a3c369f91e80f) callback, and other group members receive the [onMemberLeave](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a27ca737d915d21810b7f54e8677922e0) callback.
>The group owner of a Public group, Meeting group, or AVChatRoom group is not allowed to exit the group. Instead, the group owner can [disband the group](#dismiss).

<span id="dismiss"> </span>
### Disbanding a group
Call [dismissGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e) to disband a group. Then, all group members receive the [onGroupDismissed](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a9063ce1847731024581f2b1ad6b9ed0a) callback.

> 
>- The group owner can disband a Public group, Meeting group, or AVChatRoom group at any time.
>- For a Work group, the group owner does not have the privilege to disband the group. To disband the group, you must have your business server call the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34896).


### Obtaining the list of joined groups
Call [getJoinedGroupList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4599e99791c150cc9f3e2492e8b4ce04) to obtain a list of Work groups, Public groups, and Meeting groups the current user has joined. AVChatRooms are excluded from this list.

## Group Profiles and Group Settings
### Obtaining group profiles
Call [getGroupsInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568) to obtain the group profile of one or more groups at a time. To obtain the group profiles of multiple groups with a single call, pass in multiple `groupID` values at a time.

### Modifying group profiles
Call [setGroupInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) to modify the group profile. When the modification is completed, all group members receive the [onGroupInfoChanged](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a695c8e4a2360d400c9a781be74530db5) callback.
>
> - For Work groups, all group members can modify the basic group profile.
> - For Public groups and Meeting groups, only the group owner and group admin can modify the basic group profile.
> - For AVChatRoom groups, only the group owner can modify the basic group profile.

```
// Sample code for modifying the group profile
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"<ID of the group whose group profile needs to be modified";
info.faceURL = @"http://xxxx";
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // Modified the group profile successfully
} fail:^(int code, NSString *msg) {
    // Failed to modify the group profile
}];
```

### Setting the group message receiving option
Any group member can call the [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4974b44d56778b1d5a3df613bee09c87) API to modify the group message receiving option. Possible values are as follows:
- V2TIM_GROUP_RECEIVE_MESSAGE: messages will be received when the user is online, and APNs push notifications will be received when the user is offline.
- V2TIM_GROUP_NOT_RECEIVE_MESSAGE: no group messages will be received.
- V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE: messages will be received when the user is online, and no push notifications will be received when the user is offline.

The group message receiving option enables you to mute group messages:
- **No group messages will be received**
With the group message receiving option set to `V2TIM_GROUP_NOT_RECEIVE_MESSAGE`, no group messages will be received, and the conversation list will not be updated.
- **Group messages will be received but the user will not be notified, and a badge without the unread count will be displayed on the conversation list interface**
>Unread counting needs to be enabled for this to work. Therefore, it only applies to Work groups and Public groups.
>
With the group message receiving option set to `V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, when new group messages are received and the conversation list needs to be updated, you can obtain the unread count through [unreadCount](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6). Use [recvOpt](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#ae40fd527e110178e73b34fe72fcfd778) to verify that the group message receiving option is set to `V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE` and then display a badge without the unread count.

## Group Member Management
### Obtaing the group member list
Call [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe) to obtain the list of group members of a given group. The list contains profile information of individual members, such as their user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining the group (`joinTime`).
As a group might have a large number of members (even over 5,000), this API supports two advanced properties: `filter` and `nextSeq`.

#### Filter
When calling [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe), you can specify `filter` to pull the information list of certain group members.

| Filter | Description |
|---------|---------|
| V2TIM_GROUP_MEMBER_FILTER_ALL | Pull the information list of all group members |
| V2TIM_GROUP_MEMBER_FILTER_OWNER | Pull the information list of the group owner |
| V2TIM_GROUP_MEMBER_FILTER_ADMIN | Pull the information list of group admins |
| V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of all group members |

```
// Sample code for pulling the profile of the group owner by using the filter parameter
[[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_OWNER 
nextSeq:0 succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
    // Pulled the profile successfully
} fail:^(int code, NSString *msg) {
    // Failed to pull the profile
}];
```

#### Pulling paginated results with nextSeq
In many cases, it makes more sense for the user interface to display the first page of the group member list instead of the full list. More group members can be pulled when the user clicks "Next Page" or slides down on the list to refresh. In this scenario, you can apply the method for pulling paginated results.

The [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe) API returns a maximum of 50 members at a time. You can use the `nextSeq` pagination flag to pull the paginated group member list. In the first attempt to pull the group member list, enter 0 for `nextSeq`. When the first pull succeeds, the `getGroupMemberList` callback result [V2TIMGroupMemberInfoResult](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a7f808c605381e518881db74a4a2dbaf5) contains the `nextSeq` field.
- If `nextSeq` is 0, the full group member list has been pulled.
- If `nextSeq` is greater than 0, it indicates that additional group member information can be pulled. In this case, you can decide whether to make another call to pull additional group member information based on the user’s action on the UI. In the second pull, you need to pass in the `nextSeq` in the `V2TIMGroupMemberInfoResult` returned from the previous pull as a parameter to the [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe) API.

```
// Sample code for pulling the paginated group member list by using nextSeq
[[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_ALL nextSeq:0 
succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
    // If the nextSeq value is greater than 0, continue to pull the list.
    if (nextSeq > 0) {
        [[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_ALL 
				nextSeq:nextSeq succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
            // The second pull succeeded.
        } fail:^(int code, NSString *msg) {
            // The second pull failed.
        }];
    }
    // The first pull succeeded.
} fail:^(int code, NSString *msg) {
    // The first pull failed.
}];
```


### Obtaining the profiles of group members
Call [getGroupMembersInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04) to obtain the profiles of group members in batches. You can pass in multiple `userID` values at a time to improve network transmission efficiency.

### Modifying group name cards for members
The group owner or group admin can call the [setGroupMemberInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756) API to modify group-related information for members, including their group name card (`nameCard`), group member role (`role`), and muting duration (`muteUntil`).

```
// Sample code for changing the group name card of group member denny to denny-tencent 
V2TIMGroupMemberFullInfo *memberInfo = [[V2TIMGroupMemberFullInfo alloc] init];
memberInfo.userID = @"denny";
memberInfo.nameCard = @"denny-tencent";
[[V2TIMManager sharedInstance] setGroupMemberInfo:groupID info:memberInfo succ:^{
    // Configured successfully
} fail:^(int code, NSString *msg) {
    // Failed to configure
}];
```

<span id="mute"> </span>
### Muting
The group owner or group admin can mute a group member and set the muting duration (in seconds) through [muteGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee). Muting information is stored in the [muteUntil](http://doc.qcloudtrtc.com/im/interfaceV2TIMGroupMemberFullInfo.html#a953345fe02297a7192b727abe4b772c6) field of the group member. After the group member is muted, all group members (including the muted member) receive the [onGroupMemberInfoChanged](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a40481b176d3a7827ffa20a328ad61099) callback.
The group owner or group admin can mute all group members through the [setGroupInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) API by setting [allMuted](http://doc.qcloudtrtc.com/im/interfaceV2TIMGroupInfo.html#aff22b39b539249ee6d84aa136ca36573) to `true`. There is no time limit for group muting. The group can be unmuted by setting `allMuted` to `NO`.


<span id="kick"> </span>
### Removing group members
The group owner or group admin can call the [kickGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97) API to remove a group member. As AVChatRoom groups can have unlimited members, they do not support this API. Instead, you can use [muteGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee) for the same purpose.
After the member is removed, all group members (including the removed member) receive the [onMemberKicked](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a85e7f32f403d876018a26a1b37607edc) callback.

### Changing group member roles
The group owner can call [setGroupMemberRole](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#af7ce533e514adfab766b1ee726d9ffce) to change the role of a member of a Public group or Meeting group. You can change the role to ordinary member or group admin.
- After a member is set as a group admin, all group members (including the new admin) receive the [onGrantAdministrator](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#af9148b7c76b1ecc89f52be0ffc8316d2) callback.
- After the admin role is removed for a member, all group members (including the member whose admin role was removed) receive the [onRevokeAdministrator](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#ad82c255d1cbff590fa580f4b746e0f3e) callback.

<span id="transfer"> </span>
### Transferring a group
The group owner can call [transferGroupOwner](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a58a2ffae60505a43984fe21bf0bc1101) to transfer the ownership of the group to another group member.
After the group ownership is transferred, all group members receive the [onGroupInfoChanged](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a695c8e4a2360d400c9a781be74530db5) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

## FAQs

### 1. Can an AVChatRoom group continue to receive messages after it was disconnected and then reconnected?
Yes. However, AVChatRoom groups do not support storing the message history in the cloud, and they cannot pull the messages that were sent when it was disconnected.

### 2. Why no notifications are received when users join or exit the group?
Check the following reasons for different group types:
- Meeting groups do not support member change notifications.
- An AVChatRoom group can receive up to 40 messages per second, and therefore it prioritizes the sending and receiving of high-priority messages and discards messages with the lowest priority once the frequency limit is exceeded.

### 3. Why does the unread count of a Meeting group remain at 0?
Meeting groups and AVChatRoom groups are designed for conferencing and livestreaming scenarios respectively, so they do not support unread counting.


