<span id="type"> </span>
## Group Types
Instant Messaging (IM) supports the following group types:
- A **work group for friends (Work)** is like an ordinary WeChat group. After a work group is created, a user can only join the group by being invited by a friend who is a member of the group. The invitation does not need to be accepted by the invitee or approved by the group owner. 
- A **public group (Public)** is like a QQ group. After a public group is created, the group owner can specify group admins. When a user searches the group ID and initiates a request to join the group, the request must be approved by the group owner or admin before the user can join the group.
- A **temporary meeting group (Meeting)** allows users to join and exit freely and supports viewing historical messages from before the user joined the group. Meeting groups can integrate Tencent Real-Time Communication (TRTC), such as in audio and video conference and online education scenarios.
- A **live streaming group (AVChatRoom)** allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Live streaming groups can be used with Live Video Broadcasting (LVB) to support the on-screen comments.


The following table describes the features and limitations of each group type:

<table>
<tr>
<th width="20%">Feature Item</th>
<th width="16%">Work</th>
<th width="16%">Public</th>
<th width="16%">Meeting</th>
<th>AVChatRoom</th>
</tr>
<tr>
<td>Available member roles</td>
<td>Group owner and ordinary member</td>
<td>Group owner, group admin, and ordinary member</td>
<td>Group owner, group admin, and ordinary member</td>
<td>Group owner and ordinary member</td>
</tr>
<tr>
<td>Requesting to join a group</td>
<td>Unsupported</td>
<td>Supported with group owner or group admin approval required</td>
<td>Supported with no approval required</td>
<td>Supported with no approval required</td>
</tr>
<tr>
<td>Joining the group via invitation by a member</td>
<td>Supported</td>
<td>Unsupported</td>
<td>Unsupported</td>
<td>Unsupported</td>
</tr>
<tr>
<td>Group owner can quit the group</td>
<td>Supported</td>
<td>Unsupported</td>
<td>Unsupported</td>
<td>Unsupported</td>
</tr>
<tr>
<td>Who can modify the group profile</td>
<td>Any group member</td>
<td>Group owner and group admin</td>
<td>Group owner and group admin</td>
<td>Group owner</td>
</tr>
<tr>
<td>Who can kick group members out of the group</td>
<td>Group owner</td>
<td colspan="2">Group owner and group admin, but group admins can only kick ordinary group members out of the group</td>
<td>Group members cannot be removed. The same effect can be achieved by muting members.</td>
</tr>
<tr>
<td>Who can mute members</td>
<td>Muting members is not supported</td>
<td colspan="2">Group owner and group admin,
	but group admin can only mute ordinary group members</td>
<td>Group owner</td>
</tr>
<tr>
<td>Unread message count</td>
<td>Supported</td>
<td>Supported</td>
<td>Unsupported</td>
<td>Unsupported</td>
</tr>
<tr>
<td>Viewing historical messages from before a user joined</td>
<td>Unsupported</td>
<td>Unsupported</td>
<td>Supported</td>
<td>Unsupported</td>
</tr>
<tr>
<td>Storage of historical messages on the cloud</td>
<td colspan="3"><ul style="margin:0;padding-left:10px" ><li>Trial Edition: 7 days</li><li>Pro Edition: 7 days by default, up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: 30 days by default, up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
<td>Unsupported</td>
</tr>
<tr>
<td>Number of groups</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: up to 100 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition or Flagship Edition: unlimited</li></ul></td>
<td><ul style="margin:0;padding-left:10px"><li>Trial Edition: up to 10 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition: up to 50 existing groups, and disbanded groups do not count against the quota<br>You can upgrade to an unlimited number of live streaming groups by purchasing <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: unlimited</li></ul></td>
</tr>
<tr>
<td>Number of group members</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: 20 per group</li><li>Pro Edition: 200 per group by default, which can be increased to 2,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: 2,000 per group by default, which can be increased to 6,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a></li></ul></td>
<td>Unlimited number of group members</td>
</tr>
</table>

>? In the Pro Edition or Flagship Edition SDKAppID, the maximum net increase in group quantity per day is 10,000 for all group types by default. The maximum number of free groups is 100,000 per month, and you will need to <a href="https://intl.cloud.tencent.com/document/product/1047/34350">pay for groups exceeding the free quota</a>.


## Group Management
<span id="create"> </span>
### Creating a group
#### Simple API
You can quickly create a group by calling the [createGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989) API and specifying `groupType`, `groupID`, and `groupName`.

#### Advanced API
If you want to initialize group information (for example, group introduction, group profile photo, and initial group members) when creating a group, call the [createGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c) API in the `V2TIMManager+Group.h` management class.

```
// Sample code: create a work group using the advanced createGroup API 
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupName = @"testWork";
info.groupType = @"Work";
NSMutableArray *memberList = [NSMutableArray array];
V2TIMCreateGroupMemberInfo *memberInfo = [[V2TIMCreateGroupMemberInfo alloc] init];
memberInfo.userID = @"vinson";
[memberList addObject:memberInfo];
[[V2TIMManager sharedInstance] createGroup:info memberList:memberList succ:^(NSString *groupID) {
    // Group created successfully
} fail:^(int code, NSString *msg) {
    // Failed to create the group
}];
```

- The value of `groupType` is a string. Valid values: “Work”, “Public”, “Meeting”, and “AVChatRoom”. For more information on the differences among group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` in a single SDKAppID. If you set `groupID` to nil, an ID is assigned for your group by default.
- `groupName` specifies the group description, which has a maximum length of 30 bytes.

<span id="join"> </span>
### Joining a group
The group joining processes for different group types are described below:

| Type | Work Group (Work) | Social Networking Group (Public) | Temporary Meeting Group (Meeting) | Live Streaming Group (AVChatRoom) |
|---------|---------|---------|---------|---------|
| How to join the group | Must be invited by a group member | User joins the group after request is approved by group owner or admin | User can join freely | User can join freely |

#### Scenario 1: users can join and quit the group freely
Temporary meeting groups (Meeting) and live streaming groups (AVChatRoom) can be used for interactive scenarios where users join and exit the group frequently, such as online conferences and fashion show live streams. These groups have the simplest join procedure.

After a user successfully joins a group by calling [joinGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a), all group members (including the joining user) receive the [onMemberEnter](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#aed6a96e6b304863586a107c45ba33f11) callback. 

#### Scenario 2: users must be invited to the group
Similar to WeChat and WeChat Work groups, work groups (Work) are suitable for communication in a work environment. The interaction pattern is designed to disable proactive group joining and only allows users to be invited to the group by group members.

A group member calls [inviteUserToGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a942d75fdea66e22cdbd8c131cf18e1ea) to invite a user to the group, and then all group members (including the inviter) receive the [onMemberInvited](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a6bff27f9f6859caefcaaf361b9c6fe68) callback.

#### Scenario 3: users join the group after their requests are approved
Social networking groups (Public) are similar to the interest groups and tribes in QQ. Any user can request to join the group, but will not become a member of the group until the request is approved by the group owner or admin. While approval is required by default, the group owner or admin can call the [setGroupInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) API to set the group joining option (`V2TIMGroupAddOpt`) to “forbid anyone to join” or “disable the approval process”.
- V2TIM_GROUP_ADD_FORBID: forbid anyone to join the group.
- V2TIM_GROUP_ADD_AUTH: (default) group owner or admin approval is required to join the group.
- V2TIM_GROUP_ADD_ANY: disable the approval process to allow any user to join the group.

The following diagram illustrates the process of group joining that requires approval:
![](https://main.qcloudimg.com/raw/9164de02268e14b178937bbd85465f4f.png)

1. **The user sends a request to join the group**
    The user calls [joinGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a) to apply to join the group.
2. **The group owner or admin processes the group joining application**
 After the [onReceiveJoinApplication](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a481ab06916795cc9445fa3fc465c69ab) callback is received, the group owner or admin calls [getGroupApplicationList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a29c36ad685159850a30d61a6b9c637e8) to get the list of group joining applications, and approves or rejects an application with [acceptGroupApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a51bb9b4f965cb3d01546fef348ac75e4) or [refuseGroupApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a46aa78c54986b2c0b7cc0012a3dc94ef).
3. **The user receives the result**
The user receives the [onApplicationProcessed](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a850a50e7ea6b86a2d28afa1a569245ca) callback in [V2TIMGroupListener](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html). If `isAgreeJoin` is `true`, the application is approved. Otherwise, the application is rejected. If the application is approved, all members (including the requestor) receive the [onMemberEnter](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#aed6a96e6b304863586a107c45ba33f11) callback.

<span id="quit"> </span>
### Quitting a group
Call [quitGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5) to quit a group. The user who quits the group then receives the [onQuitFromGroup](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a9d4a0c42366ea13f688a3c369f91e80f) callback and other group members receive the [onMemberLeave](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a27ca737d915d21810b7f54e8677922e0) callback.
>! The group owners of social networking groups (Public), temporary meeting groups (Meeting), and live streaming groups (AVChatRoom) are not allowed to quit the group. Instead, the group owner can [disband the group](#dismiss).

<span id="dismiss"> </span>
### Disbanding a group
Call [dismissGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e) to disband a group. Then all group members receive the [onGroupDismissed](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a9063ce1847731024581f2b1ad6b9ed0a) callback.

>! 
>- For social networking groups (Public), temporary meeting groups (Meeting), and live streaming groups (AVChatRoom), the group owner can disband the group at any time.
>- For work groups (Work), the group owner does not have the permission to disband the group. To disband the group, you must have your business server call the [RESTful API for disbanding groups](https://intl.cloud.tencent.com/document/product/1047/34896).


### Getting the list of joined groups
Call [getJoinedGroupList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4599e99791c150cc9f3e2492e8b4ce04) to get a list of work groups (Work), social networking groups (Public), and temporary meeting groups (Meeting) the current user has joined. Live streaming groups (AVChatRoom) will not be included in this list.

## Group Profiles and Group Settings
### Getting group profiles
Call [getGroupsInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568) to get the group profile of one or more groups at a time. To get the group profiles of multiple groups by a single call, pass in multiple `groupID` at a time.

### Modifying group profiles
Call [setGroupInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) to modify the group profile. When the modification is complete, all group members receive the [onGroupInfoChanged](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a695c8e4a2360d400c9a781be74530db5) callback.
>!
> - For work groups (Work), all group members can modify the basic group profile.
> - For social networking groups (Public) and temporary meeting groups (Meeting), only the group owner and admin can modify the basic group profile.
> - For live streaming groups (AVChatRoom), only the group owner can modify the group profile.

```
// Sample code: modify the group profile
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"the ID of the group for which you want to modify the group profile";
info.faceURL = @"http://xxxx";
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // Group profile modified successfully
} fail:^(int code, NSString *msg) {
    // Failed to modify the group profile
}];
```

### Setting the group message receiving option
Any group member can call the [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4974b44d56778b1d5a3df613bee09c87) API to modify the group message receiving option. Available values are as follows:
- V2TIM_GROUP_RECEIVE_MESSAGE: messages will be received when the user is online and APNs push notifications will be received when the user is offline.
- V2TIM_GROUP_NOT_RECEIVE_MESSAGE: no group messages will be received.
- V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE: messages will be received when the user is online and no push notification will be received when the user is offline.

The group message receiving option allows you to mute group messages:
- **No group message will be received**
With the group message receiving option set to `V2TIM_GROUP_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.
- **Group messages will be received but the user will not be notified. A badge without the unread count will be displayed on the conversation list interface**
>? The unread count feature needs to be enabled for this to work. Therefore it only applies to work groups (Work) and social networking groups (Public).
>
With the group message receiving option set to `V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, when new group messages are received and the conversation list needs to update, get the unread count through [unreadCount](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6). Use [recvOpt](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#ae40fd527e110178e73b34fe72fcfd778) to verify that the group message receiving option is `V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE` and then display a badge without the unread count.

## Group Attributes (Custom Group Fields)
Based on API 2.0, we designed new custom group fields called "group attributes". Their features are as follows:
1. Clients can directly add, delete, modify, and query group attributes without the need for console configuration.
2. A maximum of 16 group attributes is supported. The maximum size supported for each group attribute is 4 KB, and the maximum size supported for all group attributes is 16 KB.
3. Currently, only AVChatRooms are supported.
4. The SDK can call initGroupAttributes, setGroupAttributes, and deleteGroupAttributes simultaneously up to 10 times every 5 seconds. If this limit is exceeded, the 8511 error code is returned via callback. The backend can call these APIs simultaneously up to 5 times per second. If this limit is exceeded, the 10049 error code is returned.
5. The SDK can call getGroupAttributes up to 20 times every 5 seconds.

Based on group attributes, we can manage the mic for voice chat rooms. When a member turns the mic on, you can set a group attribute to manage the information of the mic-on member. When the member turns the mic off, you can delete the corresponding group attribute. Other members can obtain the group attribute list to show the mic position list.

### Initializing group attributes
Call [initGroupAttributes](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a1b3a56dfc345f1ef2a575cb36156e745) to initialize group attributes. If the group originally has group attributes, the original group attributes will be cleared.

### Setting group attributes

Call [setGroupAttributes](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a134342ddb51d1ee83f3981ed91d26885) to set group attributes. If a set group attribute does not exist, it will be automatically added.

### Deleting group attributes
Call [deleteGroupAttributes](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa504ffca9492580ca27a45f78a87e2cb) to delete the specified group attribute. If the `keys` field is set to `nil`, all group attributes will be cleared.

### Obtaining group attributes
Call [getGroupAttributes](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#ac8a74db230669d1b49da47bb0895cbf9) to obtain the specified group attribute. If the `keys` field is set to `nil`, all group attributes will be obtained.

### Updating group attributes
If any group attribute is updated, all group attributes will be updated via the [onGroupAttributeChanged](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a7b76343c7ef46af4a2cd09db6d51db13) callback.

### Managing group members
### Getting group member list
Call [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe) to get the list of group members of a given group. The list contains profile information about individual members, such as user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining the group (`joinTime`).
As a group may have a large number of members (even over 5,000), so this API supports two advanced properties: `filter` and `nextSeq`.

#### Filters (filter)
When calling [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe), you can specify `filter` to pull the information list of certain group roles.

| Filter | Description |
|---------|---------|
| V2TIM_GROUP_MEMBER_FILTER_ALL | Pull the information list of all group members |
| V2TIM_GROUP_MEMBER_FILTER_OWNER | Pull the information list of the group owner |
| V2TIM_GROUP_MEMBER_FILTER_ADMIN | Pull the information list of the group admin |
| V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of ordinary group members |

```
// Sample code: pull the profile of the group owner using the filter parameter
[[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_OWNER 
nextSeq:0 succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
    // Pulled successfully
} fail:^(int code, NSString *msg) {
    // Failed to pull
}];
```

#### Pulling paginated results with nextSeq
In many cases, it makes more sense for the user interface to display the first page of the group member list instead of the complete list. More group members can be pulled when the user clicks "Next Page" or pull the list to refresh. For this scenario, you can apply the method of pulling paginated results.

The [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe) API returns a maximum of 50 members at a time. You can use the pagination flag `nextSeq` to pull a paginated group member list. In the first attempt to pull the group member list, enter 0 for `nextSeq`. When the first pull succeeds, `getGroupMemberList`’s callback result [V2TIMGroupMemberInfoResult](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a7f808c605381e518881db74a4a2dbaf5) contains the `nextSeq` field.
- If `nextSeq` is 0, the complete group member list has been pulled.
- If `nextSeq` is greater than 0, there remains group member information to be pulled. You can then decide whether to make another call to pull group member information based on the user’s action on the UI. In the second pull, you need to pass the `nextSeq` in the `V2TIMGroupMemberInfoResult` returned from the previous pull as a parameter to the [getGroupMemberList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a148bb44bf0189a4e61a294a495a43dbe) API.

```
// Sample code: pull paginated group member list using nextSeq
[[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_ALL nextSeq:0 
succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
    // If nextSeq is greater than 0, make another pull
    if (nextSeq > 0) {
        [[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_ALL 
				nextSeq:nextSeq succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
            // The second pull succeeded
        } fail:^(int code, NSString *msg) {
            // The second pull failed
        }];
    }
    // The first pull succeeded
} fail:^(int code, NSString *msg) {
    // The first pull failed
}];
```


### Getting the profiles of group members
Call [getGroupMembersInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04) to get the profiles of group members in batches. You can pass in multiple `userID` at a time to improve network transmission efficiency.

### Modifying group member profiles
The group owner or admin can call the [setGroupMemberInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756) API to modify group-related information of members, including group name card (`nameCard`), group member role (`role`), and muting duration (`muteUntil`).



<span id="mute"> </span>
### Muting
The group owner or admin can mute a group member and set the muting duration (in seconds) via [muteGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee). Muting information is stored in the [muteUntil](http://doc.qcloudtrtc.com/im/interfaceV2TIMGroupMemberFullInfo.html#a953345fe02297a7192b727abe4b772c6) field of the group member. After the group member is muted, all group members (including the muted member) receive the [onGroupMemberInfoChanged](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a40481b176d3a7827ffa20a328ad61099) callback.
The group owner or admin can mute the entire group via the [setGroupInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) API by setting [allMuted](http://doc.qcloudtrtc.com/im/interfaceV2TIMGroupInfo.html#aff22b39b539249ee6d84aa136ca36573) to `true`. There is no time limit for muting the group. The group can be unmuted by setting `allMuted` to `NO`.


<span id="kick"> </span>
### Removing group members
The group owner or admin can call the [kickGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97) API to remove a group member. As a live streaming group (AVChatRoom) can have unlimited members, it does not support the API. You can use [muteGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee) to achieve the same effect instead.
After the member is removed, all group members (including the removed member) receive the [onMemberKicked](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a85e7f32f403d876018a26a1b37607edc) callback.

### Changing group member roles
The group owner can call [setGroupMemberRole](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#af7ce533e514adfab766b1ee726d9ffce) to change the role of a member of a social networking group (Public) or temporary meeting group (Meeting). Roles available for changing are ordinary member and group admin.
- After a member is set as group admin, all group members (including the new admin) receive the [onGrantAdministrator](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#af9148b7c76b1ecc89f52be0ffc8316d2) callback.
- After the admin role is removed for a member，all group members (including the member with admin role removed) receive the [onRevokeAdministrator](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#ad82c255d1cbff590fa580f4b746e0f3e) callback.

<span id="transfer"> </span>
### Transferring a group
The group owner can call [transferGroupOwner](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a58a2ffae60505a43984fe21bf0bc1101) to transfer the ownership of the group to another group member.
After the group ownership is transferred, all group members receive the [onGroupInfoChanged](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html#a695c8e4a2360d400c9a781be74530db5) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

## FAQs

### 1. Can a live streaming group (AVChatRoom) continue to receive messages after it is disconnected and then reconnected?
Yes, but since live streaming groups (AVChatRoom) do not support storing message history in the cloud, it cannot pull the messages that were sent when it was disconnected.

### 2. Why doesn’t the group receive notifications when a user joins or quits the group?
Verify the group type:
- Temporary meeting groups (Meeting) do not support member change notifications.
- Live streaming groups (AVChatRoom) can receive up to 40 messages per second, and it prioritizes the receiving and sending of high-priority messages and discards messages with the lowest priority first once the frequency limit is exceeded.

### 3. Why does the unread count of temporary meeting groups (Meeting) remain at 0?
Temporary meeting groups (Meeting) and live streaming groups (AVChatRoom) are designed for conference and live streaming scenarios respectively, and they do not support the unread count feature.


