[](id:type)
## Group Types
Instant Messaging (IM) supports the following group types:
- A **work group (Work)** is like a WeChat group. After a work group is created, users can join the group only after being invited by group members. The invitation does not need to be accepted by the invitee or approved by the group owner. This group type is the same as private group (Private) in earlier versions. 
- A **public group (Public)** is like a QQ group. After a public group is created, the group owner can designate group admins. To join the group, a user needs to search for the group ID and send a request, and the request needs to be approved by the group owner or an admin before the user can join the group.
- A **meeting group (Meeting)** allows users to join and leave freely and view historical messages sent before they join the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio/video conferencing and online education. This group type is the same as chat room (ChatRoom) in earlier versions.
- An **audio-video group (AVChatRoom)** allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Cloud Streaming Services (CSS) to support on-screen comment chat scenarios.


The following table describes the features and limitations of each group type:

<table>
<tr>
<th width="20%">Feature</th>
<th width="16%">Work Group (Work)</th>
<th width="16%">Public Group (Public)</th>
<th width="16%">Meeting Group (Meeting)</th>
<th>Audio-Video Group (AVChatRoom)</th>
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
<td>Not supported</td>
<td>Supported with group owner or group admin approval required</td>
<td>Supported with no approval required</td>
<td>Supported with no approval required</td>
</tr>
<tr>
<td>Joining group via invitation by a member</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Group owner quitting group</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Who can modify group profile</td>
<td>Any group member</td>
<td>Group owner and group admin</td>
<td>Group owner and group admin</td>
<td>Group owner</td>
</tr>
<tr>
<td>Who can kick group members out of group</td>
<td>Group owner</td>
<td colspan="2">Group owner and group admin. Group admin can only remove ordinary group members.</td>
<td>Group members cannot be removed. The same effect can be achieved by muting members.</td>
</tr>
<tr>
<td>Who can mute members</td>
<td>Muting members is not supported</td>
<td colspan="2">Group owner and group admin.
    Group admin can only mute ordinary group members.</td>
<td>Group owner</td>
</tr>
<tr>
<td>Unread count</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Viewing message history earlier than user's entry time</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Retaining message history in the cloud</td>
<td colspan="3"><ul style="margin:0;padding-left:10px" ><li>Trial Edition: 7 days</li><li>Pro Edition: 7 days by default, up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: 30 days by default, up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
<td>Not supported</td>
</tr>
<tr>
<td>Number of groups</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: up to 100 existing groups, and deleted groups do not count against the quota.</li><li>Pro Edition or Flagship Edition: unlimited</li></ul></td>
<td><ul style="margin:0;padding-left:10px"><li>Trial Edition: up to 10 existing groups, and deleted groups do not count against the quota.</li><li>Pro Edition: up to 50 existing groups, and deleted groups do not count against the quota.<br>You can upgrade to unlimited number of audio-video groups by purchasing the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a>.</li><li>Flagship Edition: unlimited</li></ul></td>
</tr>
<tr>
<td>Number of group members</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: 20 per group</li><li>Pro Edition: 200 per group by default, can be increased to 2,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: 2,000 per group, can be increased to 6,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
<td>Unlimited number of group members</td>
</tr>
</table>

>?
>- Group types are upgraded in the new SDK version and they are **work group (Work)**, **public group (Public)**, **meeting group (Meeting)**, and **audio-video group (AVChatRoom)**. Private group (Private) and chat room (ChatRoom) in earlier versions (which have Public, Private, ChatRoom, and AVChatRoom groups) correspond to work group (Work) and meeting group (Meeting) in the new version respectively.
>- In the Pro Edition or Flagship Edition SDKAppID, the maximum net increase in group count per day is 10,000 for all group types. Free peak group count is 100,000 per month, and you will need to <a href="https://intl.cloud.tencent.com/document/product/1047/34350"> pay for usage not covered by the free quota</a>.


## Group Management
[](id:create)
### Creating a group
#### Simple API
You can quickly create a group by calling the [createGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4bada5d6a06fac04a1424ae2c597e389) API and specifying `groupType`, `groupID`, and `groupName`.

#### Advanced API
If you want to initialize group information (for example, group introduction, group profile photo, and initial group members) when creating a group, call the [createGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a10dc812487a4e9071d65a49df277f183) API in the `V2TIMManager+Group.h` management class.

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

- The value of `groupType` is a string and can be one of “Work”, “Public”, “Meeting”, and “AVChatRoom”. To learn about the differences among group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` in a SDKAppID. If you set `groupID` to nil, you will be assigned a group ID by default.
- `groupName` specifies the group description, which has a maximum length of 30 bytes.

[](id:join)
### Joining a group
The processes for joining groups of different types are described as follows:

| Type | Work Group (Work) | Public Group (Public) | Meeting Group (Meeting) | Audio-Video Group (AVChatRoom) |
|---------|---------|---------|---------|---------|
| How to join group | Must be invited by group member | User joins group after request is approved by group owner or admin | User can join freely | User can join freely |

#### Scenario 1: users can join and quit the group freely
Meeting groups (Meeting) and audio-video groups (AVChatRoom) can be used for interactive scenarios where users join and exit groups frequently, such as online conferencing and show live streaming. The group joining procedure is therefore the simplest.

After a user successfully joins a group by calling [joinGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a9979ed856657724d317791c723bacef5), all group members (including the joined user) receive the [onMemberEnter](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#aa18644e5977300f3dcf29473e58be21c) callback. 

#### Scenario 2: users must be invited to join the group
Resembling WeChat and WeCom groups, work groups (Work) are suitable for communication in work environments. The interaction pattern is designed to disable proactive group joining and only allows users to be invited to join the group by group members.

A group member calls [inviteUserToGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#af9d9a04bf3fe5a38346af842f7335f39) to invite a user to group, then all group members (including the inviter) receive the [onMemberInvited](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a6664f9b1955f58f6445774f0247de5ed) callback.

#### Scenario 3: users join the group after requests are approved
Public groups (Public) are similar to the interest groups and tribes in QQ. Any user can request to join the group, but will not become a member of the group until the request is approved by the group owner or admin. While approval is required by default, the group owner or admin can call the [setGroupInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a13b25d1f491e18ab0ba953ffc2ca9e82) API to set the group joining option (`V2TIMGroupAddOpt`) to **forbid anyone to join** which is tighter, or to **disable the approval process**, which is more flexible.
- V2TIM_GROUP_ADD_FORBID: forbid anyone to join the group
- V2TIM_GROUP_ADD_AUTH: (default) group owner or admin approval is required for group joining.
- V2TIM_GROUP_ADD_ANY: disable the approval process to allow any user to join the group.

The following diagram illustrates the process of group joining that requires approval:
![](https://main.qcloudimg.com/raw/8b0de43bea607a6a75571c1885ca75aa.svg)

1. **The user sends a request to join the group**
    The user calls [joinGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a9979ed856657724d317791c723bacef5) to join the group.
2. **The group owner or admin processes the group joining request**
 After receiving the [onReceiveJoinApplication](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a62e957192fd0ad88e79769a6266f5512) callback, the group owner or admin calls the [getGroupApplicationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ae761e7a0c5fd2ad55219bb732edae9cb) API to get the list of group joining requests, and accepts or rejects a request with [acceptGroupApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a72a9fc4dbb99d354121b944e98382e68) or [refuseGroupApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ad632874883b7b73e3fba773044bd8c1a).
3. **The user receives the result**
The user receives the [onApplicationProcessed](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a440a39aad5fb7e342579d1ddf0eea8e5) callback in [V2TIMGroupListener](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html). If `isAgreeJoin` is `true`, the request is accepted. Otherwise, the request is rejected. If the request is accepted, all members (including the requester) receive the [onMemberEnter](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#aa18644e5977300f3dcf29473e58be21c) callback.

[](id:quit)
### Quitting a group
Call [quitGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a9979ed856657724d317791c723bacef5) to quit a group. The user who quits the group then receives the [onQuitFromGroup](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a9d4a0c42366ea13f688a3c369f91e80f) callback and other group members receive the [onMemberLeave](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a70be19520a034b2f8fcba2428b6e4029) callback.
>!For a public group (Public), meeting group (Meeting), or audio-video group (AVChatRoom), the group owner is not allowed to quit the group but can [delete the group](#dismiss).

[](id:dismiss)
### Deleting groups
Call [dismissGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#af6605dd9624849843938573ef05b5463) to delete a group. Then all group members receive the [onGroupDismissed](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a2ba74c6627e1e77459bae84810af1d9d) callback.

>! 
>- For a public group (Public), meeting group (Meeting), or audio-video group (AVChatRoom), the group owner can delete the group at any time.
>- For a work group (Work), the group owner does not have the permission to delete the group. To delete the group, you must have your service server call the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34896).


### Getting the list of joined groups
Call [getJoinedGroupList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ae12e170ad585eaa8fb9f080bdc3bf8b8) to get a list of work groups (Work), public groups (Public), and meeting groups (Meeting) the current user has joined. Audio-video groups (AVChatRoom) will not be included in this list.

## Group Profiles and Group Settings
### Getting group profiles
Call [getGroupsInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aeeffef844fd0948dda227620f0fac895) to get the group profile of one or more groups at a time. To get the group profiles of multiple groups by a single call, pass in multiple `groupID` at a time.

### Modifying group profiles
Call [setGroupInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a13b25d1f491e18ab0ba953ffc2ca9e82) to modify the group profile. When the modification is complete, all group members receive the [onGroupInfoChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#ae07b62dc7f41e4c0fe74e515fd80f6ad) callback.
>!
> - For work groups (Work), all group members can modify the basic group profile.
> - For public groups (Public) and meeting groups (Meeting), only the group owner and admin can modify the group profile.
> - For audio-video groups (AVChatRoom), only the group owner can modify the group profile.

```
// Sample code: modify group profile
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
Any group member can call the [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a40f3e2ada605b73a39b05a3d3144636b) API to modify the group message receiving option. Available values are as follows:
- V2TIM_GROUP_RECEIVE_MESSAGE: messages will be received when the user is online and APNs push notifications will be received when the user is offline.
- V2TIM_GROUP_NOT_RECEIVE_MESSAGE: no group messages will be received.
- V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE: messages will be received when the user is online and no push notification will be received when the user is offline.

The group message receiving option allows you to mute group messages:
- **No group message will be received**
With the group message receiving option set to `V2TIM_GROUP_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.
- **Group messages will be received but the user will not be notified. A badge without the unread count will be displayed on the conversation list interface**
>?This mode requires the unread count feature and therefore it applies only to work groups (Work) and public groups (Public).
>
With the group message receiving option set to `V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, when new group messages are received and the conversation list needs to be updated, you can get the unread count through [unreadCount](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6). Use [recvOpt](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a851651878491c64d73aa83131134e6cc) to verify that a red dot instead of the unread count is displayed when the group message receiving option is `V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`.

## Group Attributes (Custom Group Fields)
New custom group fields, also called group attributes, are designed based on API 2.0. They have the following features:
1. You can CRUD group attributes in the client instead of console.
2. You can configure up to 16 group attributes. The size of each group attribute can be up to 4 KB, and the total size of all group attributes can be up to 16 KB.
3. Only audio-video groups (AVChatRoom) support group attributes.
4. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs each can be called by the SDK for up to 10 times per 5 seconds, and the 8511 error code will be called back if the limit is exceeded. The APIs each can be called by the backend for up to 5 times per second, and the 10049 error code will be called back if the limit is exceeded.
5. The `getGroupAttributes` API can be called by the SDK for up to 20 times per 5 seconds.

With group attributes, you can manage the seats of audio chat rooms. When a user mics on, you can set a group attribute to manage the information of the user. When the user mics off, you can delete the group attribute. Other members can get the list of group attributes to display the seat list.

### Initializing group attributes
Call the [initGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a6d34074aa8ce1e8a6dc41ee53ff5963a) API to initialize group attributes. If the group already has group attributes, the existing group attributes will be cleared.

### Setting group attributes

Call the [setGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a60bbd75b35c42e823c9538b4be44e3ea) API to set group attributes. If the group attributes to set do not exist, they will be automatically added.

### Deleting group attributes
Call the [deleteGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac26f5b3da40dae914ce08b795d2a5218) API to delete specified group attributes. If the `keys` field is set to `nil`, all group attributes will be cleared.

### Getting group attributes
Call the [getGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#af3e1eb1c23996f2beab55670be96fb2d) API to get specified group attributes. If the `keys` field is set to `nil`, all group attributes will be got.

### Updating group attributes
If group attributes have any updates, all group attribute fields will be called back via the [onGroupAttributeChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#ac709b0e0bf75c59e164bd596f6551bbc) API.

## Group Member Management
### Getting the group member list
Call [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) to get the list of group members of a given group. The list contains profile information about individual members, such as user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining group (`joinTime`).
As a group might have a large number of members (for example, 5,000+), this API supports two advanced attributes: `filter` and `nextSeq`.

#### Filters
When calling the [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) API, you can specify `filter` to pull the information list of certain roles.

| Filter | Description |
|---------|---------|
| V2TIM_GROUP_MEMBER_FILTER_ALL | Pull the information list of all group members |
| V2TIM_GROUP_MEMBER_FILTER_OWNER | Pull the information list of the group owner |
| V2TIM_GROUP_MEMBER_FILTER_ADMIN | Pull the information list of the group admin |
| V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of all group members |

```
// Sample code: pull the profile of the group owner using the filter parameter
[[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_OWNER 
nextSeq:0 succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
    // Pulled successfully
} fail:^(int code, NSString *msg) {
    // Message pulling failed
}];
```

#### Pulling paginated results with nextSeq
In many cases, it makes more sense for the user interface to display the first page of the group member list instead of the complete list. More group members can be pulled when the user clicks **Next Page** or pull the list to refresh. For this scenario, you can apply the method of pulling paginated results.

The [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) API returns a maximum of 50 members at a time. You can use the pagination flag `nextSeq` to pull the paginated group member list. In the first attempt to pull the group member list, enter 0 for `nextSeq`. When the first pull succeeds, the `getGroupMemberList` callback result [V2TIMGroupMemberInfoResult](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a7f808c605381e518881db74a4a2dbaf5) contains the `nextSeq` field.
- If `nextSeq` is 0, the complete group member list has been pulled.
- If `nextSeq` is greater than 0, there remains group member information to be pulled. You can then decide whether to make another call to pull group member information based on the user’s action on the UI. In the second pull, you need to pass the `nextSeq` in the `V2TIMGroupMemberInfoResult` returned from the previous pull as parameter to the [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) API.

```
// Sample code: pull the paginated group member list using nextSeq
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


### Getting group member profiles
Call [getGroupMembersInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ab74754f326c661e94b4511a3b6d91f32) to get the profile of group members in batches. You can pass in multiple `userID` at a time to improve network transmission efficiency.

### Modifying group member profiles
The group owner or admin can call the [setGroupMemberInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a32caf9bf614778c291194fb5cf3ca3b0) API to modify information of group members, including group name card (`nameCard`), group member role (`role`), and muting duration (`muteUntil`).

[](id:mute)
### Muting group members
The group owner or admin can mute a group member and set muting duration (in seconds) via [muteGroupMember](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee). Muting information is stored in the [muteUntil](http://doc.qcloudtrtc.com/im/interfaceV2TIMGroupMemberFullInfo.html#a953345fe02297a7192b727abe4b772c6) field of the group member. After the group member is muted, all group members (including the muted member) receive the [onMemberInfoChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a65d39c082ade86ae9c909464160bd1d9) callback.
The group owner or admin can mute the entire group via the [setGroupInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a13b25d1f491e18ab0ba953ffc2ca9e82) API by setting [allMuted](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupInfo.html#aff22b39b539249ee6d84aa136ca36573) to `true`. There is no time limit for muting a group. To unmute a group, set `allMuted` to `NO`.


[](id:kick)
### Removing group members
The group owner or admin can call the [kickGroupMember](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a21d4d4d5b5291d8eda74b3359d857714) API to remove a group member. As an audio-video group (AVChatRoom) can have unlimited members, it does not support the API. You can use [muteGroupMember](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0ee1017ecded651208261ac7d1013ad0) to achieve the same effect instead.
After the member is removed, all group members (including the removed member) receive the [onMemberKicked](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#afac4f4644954bf86a10d937c1a3499cf) callback.

### Changing group member roles
The group owner can call [setGroupMemberRole](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a548aef46b1ef435864678d56f0c0ce54) to change the role of a member of public group (Public) or meeting group (Meeting). Roles available for changing are ordinary members and group admins.
- After a member is set as group admin, all group members (including the new admin) receive the [onGrantAdministrator](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a9e4f0397fa6ba7998ecf8b9c62312afe) callback.
- After the admin role is removed for a member, all group members (including the member with admin role removed) receive the [onRevokeAdministrator](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#ab0b95c7cdfad6c21a1af7154df9cc677) callback.

[](id:transfer)
### Transferring a group
The group owner can call [transferGroupOwner](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a99e8c3488c6bbb553fc662804f7e2f02) to transfer the ownership of the group to other group members.
After the group ownership is transferred, all group members receive the [onGroupInfoChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#ae07b62dc7f41e4c0fe74e515fd80f6ad) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

## FAQs

### 1. Can an audio-video group (AVChatRoom) continue to receive messages after it was disconnected and then reconnected?
Yes, but since an audio-video group (AVChatRoom) does not support storing message history in the cloud, it cannot pull the messages that were sent when it was disconnected.

### 2. Why doesn’t the group receive notifications when a user joins or quits the group?
Verify the group type:
- Meeting group (Meeting) does not support member change notifications.
- Audio-video group (AVChatRoom) can receive up to 40 messages per second, therefore it prioritizes the receiving and sending of high-priority messages and discards messages with the lowest priority first once the frequency limit is exceeded.

### 3. Why does the unread count of meeting group (Meeting) remain at 0?
Meeting group (Meeting) and audio-video group (AVChatRoom) are designed for conference and live streaming scenarios respectively, and they do not support the unread count feature.


