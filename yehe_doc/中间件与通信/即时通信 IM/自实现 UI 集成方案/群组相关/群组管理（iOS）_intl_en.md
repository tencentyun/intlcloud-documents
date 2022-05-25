[](id:type)

## Group Types

Instant Messaging (IM) supports the following group types:

- **Work group (Work)**: After a work group is created, users can join the group only after being invited by group members. The invitation does not need to be accepted by the invitee or approved by the group owner. This group type is the same as private group (Private) in earlier versions. 
- **Public group (Public)**: After a public group is created, the group owner can designate group admins. To join the group, a user needs to search for the group ID and send a request, and the request needs to be approved by the group owner or an admin before the user can join the group.
- **Meeting group (Meeting)**: Allows users to join and leave freely and view historical messages sent before they join the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio/video conferencing and online education. This group type is the same as chat room (ChatRoom) in earlier versions.
- **Community group (Community)**: Allows users to join and exit freely and is ideal for ultra-large community group chat scenarios, such as knowledge sharing and game communication
- **Audio-video group (AVChatRoom)**: Allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Cloud Streaming Services (CSS) to support on-screen comment chat scenarios.


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
<td>Group owner and common member</td>
<td>Group owner, group admin, and common member</td>
<td>Group owner, group admin, and common member</td>
<td>Group owner, group admin, and common member</td>
<td>Group owner and common member</td>
</tr>
<tr>
<td>Requesting to join a group</td>
<td>Not supported</td>
<td>Supported with group owner or admin approval required</td>
<td>Supported, and no approval required</td>
<td>Supported, and no approval required</td>
<td>Supported, and no approval required</td>
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
<td>Group owner leaving group</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Who can modify group profile</td>
<td>Any group member</td>
<td>Group owner and admin</td>
<td>Group owner and admin</td>
<td>Group owner and admin</td>
<td>Group owner</td>
</tr>
<tr>
<td>Who can kick group members out of group</td>
<td>Group owner</td>
<td colspan="3">Group owner and admin. Group admin can only remove common group members.</td>
<td>Group members cannot be removed. The same effect can be achieved by muting members.</td>
</tr>
<tr>
<td>Who can mute members</td>
<td>Muting members is not supported</td>
<td colspan="3">Group owner and admin.
    Group admin can only mute common group members.</td>
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
<td colspan="4"><ul style="margin:0;padding-left:10px" ><li>Trial Edition: Seven days</li><li>Pro Edition: Seven days by default, which can be increased to up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: 30 days by default, which can be increased to up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
<td>Not supported</td>
</tr>
<tr>
<td>Number of groups</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: Up to 100 existing groups, and deleted groups do not count against the quota.</li><li>Pro Edition or Flagship Edition: Unlimited</li></ul></td>
<td><ul style="margin:0;padding-left:10px"><li>Trial Edition and Pro Edition: Not supported</li><li>Flagship Edition: 100,000</li></ul></td>
<td><ul style="margin:0;padding-left:10px"><li>Trial Edition: Up to 10 existing groups, and deleted groups do not count against the quota.</li><li>Pro Edition: Up to 50 existing groups, and deleted groups do not count against the quota.<br>You can upgrade to unlimited number of audio-video groups by purchasing the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a>.</li><li>Flagship Edition: Unlimited</li></ul></td>
</tr>
<tr>
<td>Number of group members</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: 20 per group</li><li>Pro Edition: 200 per group by default, which can be increased to up to 2,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Flagship Edition: 2,000 per group, which can be increased to up to 6,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
<td>100,000</td>
<td>Unlimited number of group members</td>
</tr>
</table>

>?
>
>- Group types are upgraded in the new SDK version and they are **work group (Work)**, **public group (Public)**, **meeting group (Meeting)**, **community group (Community)**, and **audio-video group (AVChatRoom)**. Private group (Private) and chat room (ChatRoom) in earlier versions (which have Public, Private, ChatRoom, and AVChatRoom groups) correspond to work group (Work) and meeting group (Meeting) in the new version respectively.
>- In the Pro Edition or Flagship Edition SDKAppID, the maximum net increase in group count per day is 10,000 for all group types. Free peak group count is 100,000 per month, and you will need to <a href="https://intl.cloud.tencent.com/document/product/1047/34350"> pay for usage not covered by the free quota</a>.
>- Community groups (Community) are supported only in native SDK 5.8.1668 Enhanced Edition or higher and web SDK 2.17.0 or later. To use the feature, you need to purchase the Flagship Edition package and [apply for activation](https://intl.cloud.tencent.com/document/product/1047/44322).
>- Work groups (Work) and public groups (Public) do not allow group members to view messages sent before they join the group. To enable the feature, submit a change request by referring to [Configuration Change Ticket](https://intl.cloud.tencent.com/document/product/1047/44322).


## Group Management

[](id:create)

### Creating a group

#### Simple API

You can quickly create a group by calling the [createGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4bada5d6a06fac04a1424ae2c597e389) API and specifying `groupType`, `groupID`, and `groupName`.

#### Advanced API

If you want to initialize group information (for example, group introduction, group profile photo, and initial group members) when creating a group, call the [createGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a10dc812487a4e9071d65a49df277f183) API in the `V2TIMManager+Group.h` management class.

```objectivec
// Sample code: Use the advanced `createGroup` API to create a work group 
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

- The value of `groupType` is a string and can be one `Work`, `Public`, `Meeting`, or `AVChatRoom`. For the differences between group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` in a SDKAppID. If you set `groupID` to `nil`, you will be assigned a group ID by default.
- `groupName` specifies the group description, which can have a maximum length of 30 bytes.

[](id:join)

### Joining a group

The group joining method varies according to the group type, as described below:

| Group Type | Work Group (Work) | Public Group (Public) | Meeting Group (Meeting) | Community Group (Community) | Audio-Video Group (AVChatRoom) |
| -------- | -------------------- | -------------------------- | --------------------- | ----------------- | -------------------- |
| Group Joining Method | Users must be invited by group member. | Users can join the group only after their requests are approved by group owner or admin. | Users can join the group freely. | Users can join the group freely. | Users can join the group freely. |

#### Scenario 1: Users can join the group freely

Meeting groups (Meeting) and audio-video groups (AVChatRoom) can be used for interactive scenarios where users join and leave groups frequently, such as online conferencing and show live streaming. The group joining procedure is therefore the simplest.

After a user successfully joins a group by calling [joinGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a9979ed856657724d317791c723bacef5), all group members (including the joined user) receive the [onMemberEnter](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#aa18644e5977300f3dcf29473e58be21c) callback. 

#### Scenario 2: Users must be invited to join the group

Resembling WeChat and WeCom groups, work groups (Work) are suitable for communication in work environments. The interaction pattern is designed to disable proactive group joining and only allow users to be invited to join the group by group members.

A group member calls [inviteUserToGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#af9d9a04bf3fe5a38346af842f7335f39) to invite a user to join the group, and then all group members (including the inviter) receive the [onMemberInvited](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a6664f9b1955f58f6445774f0247de5ed) callback.

#### Scenario 3: Users can join the group only after their requests are approved

Public groups (Public) are similar to the interest groups and tribes in QQ. Any user can request to join the group, but will not become a member of the group until the request is approved by the group owner or admin. While approval is required by default, the group owner or admin can call the [setGroupInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a13b25d1f491e18ab0ba953ffc2ca9e82) API to set the group joining option (`V2TIMGroupAddOpt`) to **forbid anyone to join** which is tighter, or to **disable the approval process**, which is more flexible.

- V2TIM_GROUP_ADD_FORBID: Forbid anyone to join the group.
- V2TIM_GROUP_ADD_AUTH (default): Group owner or admin approval is required for group joining.
- V2TIM_GROUP_ADD_ANY: Disable the approval process to allow any user to join the group.

The following diagram illustrates the process of group joining that requires approval:
![](https://main.qcloudimg.com/raw/9164de02268e14b178937bbd85465f4f.png)

1. **The user sends a request to join the group**
   The user calls [joinGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a9979ed856657724d317791c723bacef5) to join the group.
2. **The group owner or admin processes the group joining request**
   After receiving the [onReceiveJoinApplication](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a62e957192fd0ad88e79769a6266f5512) callback, the group owner or admin calls the [getGroupApplicationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ae761e7a0c5fd2ad55219bb732edae9cb) API to get the list of group joining requests, and accepts or rejects a request with [acceptGroupApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a72a9fc4dbb99d354121b944e98382e68) or [refuseGroupApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ad632874883b7b73e3fba773044bd8c1a).
3. **The user receives the result**
   The user receives the [onApplicationProcessed](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a440a39aad5fb7e342579d1ddf0eea8e5) callback in [V2TIMGroupListener](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html). If `isAgreeJoin` is `true`, the request is accepted. Otherwise, the request is rejected. If the request is accepted, all members (including the requester) receive the [onMemberEnter](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#aa18644e5977300f3dcf29473e58be21c) callback.

[](id:quit)

### Leaving a group

Call [quitGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a9979ed856657724d317791c723bacef5) to leave a group. The user who leaves the group then receives the [onQuitFromGroup](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a9d4a0c42366ea13f688a3c369f91e80f) callback and other group members receive the [onMemberLeave](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a70be19520a034b2f8fcba2428b6e4029) callback.

>!For a public group (Public), meeting group (Meeting), community group (Community), or audio-video group (AVChatRoom), the group owner is not allowed to leave the group but can [delete the group](#dismiss).

[](id:dismiss)

### Deleting a group

Call [dismissGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#af6605dd9624849843938573ef05b5463) to delete a group. Then all group members receive the [onGroupDismissed](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a2ba74c6627e1e77459bae84810af1d9d) callback.

>! 
>
>- For a public group (Public), meeting group (Meeting), community group (Community), or audio-video group (AVChatRoom), the group owner can delete the group at any time.
>- For a work group (Work), the group owner does not have the permission to delete the group. To delete the group, you must have your service server call the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34896).


### Getting the list of joined groups

Call [getJoinedGroupList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ae12e170ad585eaa8fb9f080bdc3bf8b8) to get a list of work groups (Work), public groups (Public), meeting groups (Meeting), and community groups (Community) the current user has joined. Audio-video groups (AVChatRoom) will not be included in this list.

## Group Profiles and Group Settings

[](id:getGroupsInfo)

### Getting group profiles

Call [getGroupsInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aeeffef844fd0948dda227620f0fac895) to get the group profile of one or more groups at a time. To get the group profiles of multiple groups by a single call, pass in multiple `groupID` values at a time.

### Modifying group profiles[](id:setGroupInfo)

Call [setGroupInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a13b25d1f491e18ab0ba953ffc2ca9e82) to modify the group profile. When the modification is complete, all group members receive the [onGroupInfoChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#ae07b62dc7f41e4c0fe74e515fd80f6ad) callback.

>!
>
>- For work groups (Work), all group members can modify the group profile.
>- For public groups (Public), meeting groups (Meeting), and community groups (Community), only the group owner and admin can modify the group profile.
>- For audio-video groups (AVChatRoom), only the group owner can modify the group profile.

```objectivec
// Sample code: Modify group profile
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"the ID of the group for which you want to modify the group profile";
info.faceURL = @"http://xxxx";
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // Group profile modified successfully
} fail:^(int code, NSString *msg) {
    // Failed to modify the group profile
}];
```

[](id:setGroupReceiveMessageOpt)

### Setting the group message receiving option

Any group member can call the [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a40f3e2ada605b73a39b05a3d3144636b) API to modify the group message receiving option. Available values are as follows:

- V2TIM_GROUP_RECEIVE_MESSAGE: Messages will be received when the user is online, and APNs push notifications will be received when the user is offline.
- V2TIM_GROUP_NOT_RECEIVE_MESSAGE: No group messages will be received.
- V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE: Messages will be received when the user is online, and no push notification will be received when the user is offline.

The group message receiving option allows you to mute group messages:

- **No group message will be received**
  With the group message receiving option set to `V2TIM_GROUP_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.
- **Group messages will be received but the user will not be notified. A badge without the unread count will be displayed on the conversation list interface.**

>?This mode requires the unread count feature and therefore it applies only to work groups (Work) and public groups (Public).
>
>With the group message receiving option set to `V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, when new group messages are received and the conversation list needs to be updated, you can get the unread count through [unreadCount](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6). Use [recvOpt](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a851651878491c64d73aa83131134e6cc) to verify that a red dot instead of the unread count is displayed when the group message receiving option is `V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`.

## Group Attributes (Custom Group Fields)

New custom group fields, also called group attributes, are designed based on API 2.0. They have the following features:

1. You can CRUD group attributes directly in the client without console configuration.
2. You can configure up to 16 group attributes. The size of each group attribute can be up to 4 KB, and the total size of all group attributes can be up to 16 KB.
3. Only audio-video groups (AVChatRoom) support group attributes.
4. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs each can be called by the SDK for up to 10 times per five seconds, and the error code 8511 will be called back if the limit is exceeded. The APIs each can be called by the backend for up to five times per second, and the error code 10049 will be called back if the limit is exceeded.
5. The `getGroupAttributes` API can be called by the SDK for up to 20 times per five seconds.

With group attributes, you can manage the seats of audio chat rooms. When a user mic on, you can set a group attribute to manage the information of the user. When the user mic off, you can delete the group attribute. Other members can get the list of group attributes to display the seat list.

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

[](id:getGroupMemberList)

### Getting the group member list

Call [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) to get the list of group members of a given group. The list contains profile information about individual members, such as user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining group (`joinTime`).
As a group might have a large number of members (for example, over 5,000), this API supports two advanced features: filter (`filter`) and pulling by page (`nextSeq`).

#### Filter (`filter`)

When calling the [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) API, you can specify `filter` to pull the information list of certain roles.

| Filter                           | Description                   |
| -------------------------------- | -------------------------- |
| V2TIM_GROUP_MEMBER_FILTER_ALL | Pull the information list of all group members |
| V2TIM_GROUP_MEMBER_FILTER_OWNER | Pull the information list of the group owner |
| V2TIM_GROUP_MEMBER_FILTER_ADMIN | Pull the information list of the group admin |
| V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of common group members |

```objectivec
// Sample code: Pull the profile of the group owner using the `filter` parameter
[[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_OWNER 
nextSeq:0 succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
    // Pulled successfully
} fail:^(int code, NSString *msg) {
    // Failed to pull
}];
```

#### Pulling by page (`nextSeq`)

In many cases, it makes more sense for the user interface to display the first page of the group member list instead of the complete list. More group members can be pulled when the user clicks **Next Page** or scroll down the list to refresh. For this scenario, you can apply the method of pulling by page.

The [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) API returns a maximum of 50 members at a time. You can use the pagination flag `nextSeq` to pull the paginated group member list. In the first attempt to pull the group member list, enter `0` for `nextSeq`. When the first pull succeeds, the `getGroupMemberList` callback result [V2TIMGroupMemberInfoResult](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a7f808c605381e518881db74a4a2dbaf5) contains the `nextSeq` field.

- If `nextSeq` is `0`, the complete group member list has been pulled.
- If `nextSeq` is greater than 0, there remains group member information to be pulled. You can then decide whether to make another call to pull group member information based on the user’s action on the UI. In the second pull, you need to pass the `nextSeq` in the `V2TIMGroupMemberInfoResult` returned from the previous pull as the input parameter of the [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ba27ad3077804addcfd92c3a45dd092) API.

```objectivec
// Sample code: Use `nextSeq` to pull the group member list by page
[[V2TIMManager sharedInstance] getGroupMemberList:@"testGroup" filter:V2TIM_GROUP_MEMBER_FILTER_ALL nextSeq:0 
succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberInfo *> *memberList) {
    // If `nextSeq` is greater than 0, make another pull
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

[](id:getGroupMembersInfo)

### Getting group member profiles

Call [getGroupMembersInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ab74754f326c661e94b4511a3b6d91f32) to get the profile of group members in batches. You can pass in multiple `userID` at a time to improve network transmission efficiency.

[](id:setGroupMemberInfo)

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

The group owner can call [setGroupMemberRole](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a548aef46b1ef435864678d56f0c0ce54) to change the role of a member of public group (Public) or meeting group (Meeting). Roles available for changing are common members and group admins.

- After a member is set as group admin, all group members (including the new admin) receive the [onGrantAdministrator](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a9e4f0397fa6ba7998ecf8b9c62312afe) callback.
- After the admin role is removed for a member, all group members (including the member with admin role removed) receive the [onRevokeAdministrator](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#ab0b95c7cdfad6c21a1af7154df9cc677) callback.

[](id:transfer)

### Transferring the ownership of a group

The group owner can call [transferGroupOwner](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a99e8c3488c6bbb553fc662804f7e2f02) to transfer the ownership of the group to other group members.
After the group ownership is transferred, all group members receive the [onGroupInfoChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#ae07b62dc7f41e4c0fe74e515fd80f6ad) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

## Community Group Topics

A community group is a large group of people brought together by common topics, and multiple topics can be created under the same community group based on different interests.
Community groups are used to manage group members. All topics under the same community group share community members, and can send and receive messages independently without interfering with each other.

>! Community group topics are supported only in 6.2.2363 and later versions.

### Community group management

#### Creating a community group

You need to perform two steps to create a community group that supports topics:

1. Create the [V2TIMGroupInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupInfo.html) object, and set `groupType` to `Community` and `isSupportTopic` to `true` in the object.
2. Call the [createGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c) API to create the group.

Sample code:

```objectivec
V2TIMGroupInfo *groupInfo = [[V2TIMGroupInfo alloc] init];;
groupInfo.groupName = @"This is a Community";
groupInfo.groupType = GroupType_Community;
groupInfo.isSupportTopic = YES;
[[V2TIMManager sharedInstance] createGroup:groupInfo memberList:nil succ:^(NSString *groupID) {
    // Community group created successfully
} fail:^(int code, NSString *desc) {
    // Creation failed
}];
```

#### Getting the list of community groups joined

Call the [getJoinedCommunityList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a17350dec83b7cd32d308a1f2b2827fdd) API to get the list of community groups the current user has joined.

Sample code:

```objectivec
[[V2TIMManager sharedInstance] getJoinedCommunityList:^(NSArray<V2TIMGroupInfo *> *groupList) {
    // Community group list got successfully
} fail:^(int code, NSString *desc) {
    // Failed to get the community group list
}];

```

#### Other management APIs

Other management APIs for the community groups and community group members are listed in the following table.

<table>
<tr>
<th width="15%">Category</th>
<th width="25%">Feature</th>
<th width="60%">API</th>
</tr>
<tr>
<td rowspan="5">Community group management</td>
<td><a href="#join">Joining a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a">joinGroup</a></td>
</tr>
<tr>
<td><a href="#quit">Leaving a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5">quitGroup</a></td>
</tr>
<tr>
<td><a href="#dismiss">Deleting a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e">dismissGroup</a></td>
</tr>
<tr>
<td><a href="#getGroupsInfo">Getting the profile of a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568">getGroupsInfo</a></td>
</tr>
<tr>
<td><a href="#setGroupInfo">Modifying the profile of a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144">setGroupInfo</a></td>
</tr>
<tr>
<td rowspan="4">Community group member management</td>
<td><a href="#getGroupMemberList">Getting the list of community group members</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a98681b9036e73acbe8f84737b5291326">getGroupMemberList</a></td>
</tr>
<tr>
<td><a href="#getGroupMembersInfo">Getting the profiles of specified group members</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04">getGroupMembersInfo</a></td>
</tr>
<tr>
<td><a href="#setGroupMemberInfo">Modifying the profiles of specified group members</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756">setGroupMemberInfo</a></td>
</tr>
<tr>
<td><a href="#kick">Removing a member from a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97">kickGroupMember</a></td>
</tr>
</table>


### Topic management

#### Creating a topic

You need to perform two steps to create a topic:

1. Create the [V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMTopicInfo.html) object.
2. Call the [createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a8cc04d04254867787060cf1cae0fc5b8) API to create the topic.

Sample code:

```objectivec
V2TIMTopicInfo *topicInfo = [[V2TIMTopicInfo alloc] init];
topicInfo.topicName = @"topicName";
topicInfo.topicFaceURL = @"topicFaceUrl";
topicInfo.introduction = @"topicIntroduction";
topicInfo.notification = @"topicNotification";
topicInfo.customString = @"topicCustomString";

// Set `groupID` to the ID of a community group that supports topics
[[V2TIMManager sharedInstance] createTopicInCommunity:@"groupID" topicInfo:topicInfo succ:^(NSString *topicID) {
    // Topic created successfully
} fail:^(int code, NSString *desc) {
    // Failed to create the topic
}];

```

#### Deleting a topic

Call the [deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a31b726136637a58b5bb246eaac41187c) API to delete a topic.
Sample code:

```objectivec
[[V2TIMManager sharedInstance] deleteTopicFromCommunity:@"groupID" topicIDList:@[@"topic1", @"topic2"] succ:^(NSMutableArray<V2TIMTopicOperationResult *> *resultList) {
    // Topic deleted successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete the topic
}];
```

#### Modifying topic information

You need to perform two steps to modify the information of a topic:

1. Create the [V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMTopicInfo.html) object and set the fields to be modified in the object.
2. Call the [setTopicInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a237e2fa6e16e55143c516c5428a23936) API to modify the topic information.

Sample code:

```objectivec
V2TIMTopicInfo *topicInfo = [[V2TIMTopicInfo alloc] init];
topicInfo.topicID = @"topicID";
topicInfo.topicName = @"topicName";
topicInfo.topicFaceURL = @"topicFaceUrl";
topicInfo.introduction = @"topicIntroduction";
topicInfo.notification = @"topicNotification";
topicInfo.customString = @"topicCustomString";
topicInfo.draftText =  @"topicDraft";
topicInfo.isAllMuted = NO;
[[V2TIMManager sharedInstance] setTopicInfo:topicInfo succ:^{
    // Topic information modified successfully
} fail:^(int code, NSString *desc) {
    // Failed to modify the topic information
}];

```

To modify other topic information, see [Muting members](#mute) and [Modifying the topic message receiving option](#setGroupReceiveMessageOpt).

#### Getting the topic list

Call the [getTopicInfoList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#af93ad10e0e2b21d6ae3c8ec45021b159) API to get the topic list.

- If `topicIDList` is empty, the list of all topics of the community group will be got.
- If `topicIDList` is the ID of specified topics, the list of the specified topics will be got.

Sample code:

```objectivec
[[V2TIMManager sharedInstance] getTopicInfoList:@"groupID" topicIDList:@[@"topic1", @"topic2"] succ:^(NSMutableArray<V2TIMTopicInfoResult *> *resultList) {
    // Topic list got successfully
} fail:^(int code, NSString *desc) {
    // Failed to get the topic list
}];
```

#### Listening for topic callbacks

In [V2TIMGroupListener](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html), topic related callback methods `onTopicCreated`, `onTopicDeleted`, and `onTopicInfoChanged` are added for topic event listening. 

Sample code:

```objectivec
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onTopicCreated:(NSString *)groupID topicID:(NSString *)topicID {
    // Listening for topic creation notifications
}
- (void)onTopicDeleted:(NSString *)groupID topicIDList:(NSArray<NSString *> *)topicIDList {
    // Listening for topic deletion notifications
}
- (void)onTopicChanged:(NSString *)groupID topicInfo:(V2TIMTopicInfo *)topicInfo {
    // Listening for topic information update notifications
}
```

### Topic messages

Messages can be sent and received within a topic, and messages between different topics are independent of each other.

Topic message APIs are in the core class `V2TIMManager(Message)` and are described in the following table.

<table>
<tr>
<th width="15%">Feature</th>
<th width="40%">API</th>
<th width="30%">Remarks</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36360">Sending messages</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21">sendMessage</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36360">Receiving messages</a></td>
<td>`onRecvNewMessage` method in <a href="https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html">V2TIMAdvancedMsgListener</a></td>
<td>Set `groupID` in the message to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36360">Marking messages as read</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc">markGroupMessageAsRead</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36360">Getting the message history</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0">getGroupHistoryMessageList</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36360">Recalling messages</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a">revokeMessage</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
</table>


## FAQs

### 1. Can an audio-video group (AVChatRoom) continue to receive messages after it was disconnected and then reconnected?

Yes, but since an audio-video group (AVChatRoom) does not support storing message history in the cloud, it cannot pull the messages that were sent when it was disconnected.

### 2. Why doesn't the group receive notifications when a user joins or leaves the group?

Verify the group type:

- A meeting group (Meeting) does not support member change notifications.
- An audio-video group (AVChatRoom) can receive up to 40 messages per second, and therefore it prioritizes the receiving and sending of high-priority messages and discards messages with the lowest priority first once the frequency limit is exceeded.

### 3. Why does the unread count of a meeting group (Meeting) remain at zero?

Meeting groups (Meeting) and audio-video groups (AVChatRoom) are designed for conference and live streaming scenarios respectively, and they do not support the unread count feature.
