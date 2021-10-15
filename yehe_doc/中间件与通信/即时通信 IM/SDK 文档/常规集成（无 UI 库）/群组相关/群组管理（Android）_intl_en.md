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
You can quickly create a group by calling the [createGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) API and specifying `groupType`, `groupID`, and `groupName`.

#### Advanced API
If you want to initialize group information (for example, group introduction, group profile photo, and initial group members) when creating a group, call the [createGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) API in the `V2TIMGroupManager` management class. The `V2TIMGroupManager` management class can be obtained via `V2TIMManager.getGroupManager`.

```
// Sample code: create a work group using the advanced createGroup API 
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupName("testWork");
v2TIMGroupInfo.setGroupType("Work");
v2TIMGroupInfo.setIntroduction("this is a test Work group");

List<V2TIMCreateGroupMemberInfo> memberInfoList = new ArrayList<>();
V2TIMCreateGroupMemberInfo memberA = new V2TIMCreateGroupMemberInfo();
memberA.setUserID("vinson");
V2TIMCreateGroupMemberInfo memberB = new V2TIMCreateGroupMemberInfo();
memberB.setUserID("park");
memberInfoList.add(memberA);
memberInfoList.add(memberB);

V2TIMManager.getGroupManager().createGroup(
    v2TIMGroupInfo, memberInfoList, new V2TIMValueCallback<String>() {
	@Override
	public void onError(int code, String desc) {
		// Failed to create
	}
	@Override
	public void onSuccess(String groupID) {
		// Created successfully
	}
});
```

- The value of `groupType` is a string. Valid values: “Work”, “Public”, “Meeting”, and “AVChatRoom”. For more information on the differences among group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` in a single SDKAppID. If you set `groupID` to null, an ID is assigned for your group by default.
- `groupName` specifies the group description, which has a maximum length of 30 bytes.

<span id="join"> </span>
### Joining a group
The group joining processes for different group types are described below:

| Type | Work Group (Work) | Social Networking Group (Public) | Temporary Meeting Group (Meeting) | Live Streaming Group (AVChatRoom) |
|---------|---------|---------|---------|---------|
| How to join the group | Must be invited by a group member | User joins the group after request is approved by group owner or admin | User can join freely | User can join freely |

#### Scenario 1: users can join and quit the group freely
Temporary meeting groups (Meeting) and live streaming groups (AVChatRoom) can be used for interactive scenarios where users join and exit the group frequently, such as online conferences and fashion show live streams. These groups have the simplest join procedure.

After a user successfully joins a group by calling [joinGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564), all group members (including the joining user) receive the [onMemberEnter](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) callback. 

#### Scenario 2: users must be invited to the group
Similar to WeChat and WeChat Work groups, work groups (Work) are suitable for communication in a work environment. The interaction pattern is designed to disable proactive group joining and only allows users to be invited to the group by group members.

A group member calls [inviteUserToGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92) to invite a user to the group, and then all group members (including the inviter) receive the [onMemberInvited](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#af6119ca3c6eabcc63acbf012f508b1b1) callback.

#### Scenario 3: users join the group after their requests are approved
Social networking groups (Public) are similar to the interest groups and tribes in QQ. Any user can request to join the group, but will not become a member of the group until the request is approved by the group owner or admin. While approval is required by default, the group owner or admin can call the [setGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) API to set the group joining option (`V2TIMGroupAddOpt`) to “forbid anyone to join” or “disable the approval process”.
- V2TIM_GROUP_ADD_FORBID: forbid anyone to join the group.
- V2TIM_GROUP_ADD_AUTH: (default) group owner or admin approval is required to join the group.
- V2TIM_GROUP_ADD_ANY: disable the approval process to allow any user to join the group.

The following diagram illustrates the process of group joining that requires approval:
![](https://main.qcloudimg.com/raw/9164de02268e14b178937bbd85465f4f.png)

1. **The user sends a request to join the group**
The user calls [joinGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) to request to join the group.
2. **The group owner or admin processes the group joining application**
After the [onReceiveJoinApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#adf0b34684efd46d6e31d31e7bc3643f9) callback is received, the group owner or admin calls [getGroupApplicationList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4) to get the list of group joining requests, and approves or rejects a request with [acceptGroupApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07) or [refuseGroupApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd).
3. **The user receives the result**
 The user receives the [onApplicationProcessed](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac833c624e33036ec0454fe5444b8f00a) callback in [V2TIMGroupListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html). If `isAgreeJoin` is `true`, the request is approved. Otherwise, the request is rejected. If the request is approved, all members (including the requestor) receive the [onMemberEnter](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) callback.



<span id="quit"> </span>
### Quitting a group
Call [quitGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919) to quit a group. The user who quits the group then receives the [onQuitFromGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a489004526f1bd8daba7ac63fb0ad965f) callback and other group members receive the [onMemberLeave](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2169676423875e4c9c376796245ca8d5) callback.
>! The group owners of social networking groups (Public), temporary meeting groups (Meeting), and live streaming groups (AVChatRoom) are not allowed to quit the group. Instead, the group owner can [disband the group](#dismiss).

<span id="dismiss"> </span>
### Disbanding a group
Call [dismissGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb) to disband a group. Then all group members receive the [onGroupDismissed](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a6e89728e160e126460a6b8eeddf00ad5) callback.

>! 
>- For social networking groups (Public), temporary meeting groups (Meeting), and live streaming groups (AVChatRoom), the group owner can disband the group at any time.
>- For work groups (Work), the group owner does not have the permission to disband the group. To disband the group, you must have your business server call the [RESTful API for disbanding groups](https://intl.cloud.tencent.com/document/product/1047/34896).


### Getting the list of joined groups
Call [getJoinedGroupList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a05bfd8f7df6bfba718abc96fdad49791) to get a list of work groups (Work), social networking groups (Public), and temporary meeting groups (Meeting) the current user has joined. Live streaming groups (AVChatRoom) will not be included in this list.

## Group Profiles and Group Settings
### Getting group profiles
Call [getGroupsInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154) to get the group profile of one or more groups at a time. To get the group profiles of multiple groups with a single call, pass in multiple `groupIDs` at one time.

### Modifying group profiles
Call [setGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) to modify the group profile. When the modification is complete, all group members receive the [onGroupInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad5968cdb7ca01e2f7a702e2ca2f648fb) callback.
>!
> - For work groups (Work), all group members can modify the basic group profile.
> - For social networking groups (Public) and temporary meeting groups (Meeting), only the group owner and admin can modify the basic group profile.
> - For live streaming groups (AVChatRoom), only the group owner can modify the group profile.

```
// Sample code: modify the group profile
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupID("the ID of the group for which you want to modify the group profile");
v2TIMGroupInfo.setFaceUrl("http://xxxx");
V2TIMManager.getGroupManager().setGroupInfo(v2TIMGroupInfo, new V2TIMCallback() {
		@Override
		public void onError(int code, String desc) {
			// Failed
		}
		@Override
		public void onSuccess() {
			// Successful
		}
});
```

### Setting the group message receiving option
Any group member can call the [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e) API to modify the group message receiving option. Available values are as follows:
- V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_MESSAGE: messages will be received when the user is online and push notifications will be received when the user is offline.
- V2TIMGroupInfo.V2TIM_GROUP_NOT_RECEIVE_MESSAGE: no group messages will be received.
- V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE: messages will be received when the user is online and no push notification will be received when the user is offline.

The group message receiving option allows you to mute group messages:
- **No group message will be received**
With the group message receiving option set to `V2TIMGroupInfo.V2TIM_GROUP_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.
- **Group messages will be received but the user will not be notified. A badge without the unread count will be displayed on the conversation list interface**
>? The unread count feature needs to be enabled for this to work. Therefore it only applies to work groups (Work) and social networking groups (Public).
>
With the group message receiving option set to `V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, when new group messages are received and the conversation list needs to update, get the unread count through [getUnreadCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e). Use [getRecvOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) to verify that the group message receiving option is `V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE` and then display a badge without the unread count.

## Group Attributes (Custom Group Fields)
Based on API 2.0, we designed new custom group fields called "group attributes". Their features are as follows:
1. Clients can directly add, delete, modify, and query group attributes without the need for console configuration.
2. A maximum of 16 group attributes is supported. The maximum size supported for each group attribute is 4 KB, and the maximum size supported for all group attributes is 16 KB.
3. Currently, only AVChatRooms are supported.
4. The SDK can call initGroupAttributes, setGroupAttributes, and deleteGroupAttributes simultaneously up to 10 times every 5 seconds. If this limit is exceeded, the 8511 error code is returned via callback. The backend can call these APIs simultaneously up to 5 times per second. If this limit is exceeded, the 10049 error code is returned.
5. The SDK can call getGroupAttributes up to 20 times every 5 seconds.

Based on group attributes, we can manage the mic for voice chat rooms. When a member turns the mic on, you can set a group attribute to manage the information of the mic-on member. When the member turns the mic off, you can delete the corresponding group attribute. Other members can obtain the group attribute list to show the mic position list.

### Initializing group attributes
Call [initGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a17569b57abc77adb6be9356b9eb70182) to initialize group attributes. The original group attributes, if any, will be cleared.

### Setting group attributes

Call [setGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3ec31101e4763dab7a1c99a71bc3da08) to set group attributes. If a set group attribute does not exist, it will be automatically added.

### Deleting group attributes
Call [deleteGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a45f211bafddc58bf5e199e18a6814578) to delete the specified group attribute. If the `keys` field is set to `null`, all group attributes will be cleared.

### Obtaining group attributes
Call [getGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ade2155fb24ed1c0b8eb976e146c14e3d) to obtain the specified group attribute. If the `keys` field is set to `null`, all group attributes will be obtained.

### Updating group attributes
If any group attribute is updated, all group attributes will be updated via the [onGroupAttributeChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#aa390fa93bc73a0262bdddb540227dc45) callback.

### Managing group members
### Getting group member list
Call [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) to get the list of members of a specified group. The list contains profile information about individual members, such as user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining the group (`joinTime`).
As a group may have a large number of members (even over 5,000), so this API supports two advanced properties: `filter` and `nextSeq`.

#### Filters (filter)
When calling [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be), you can specify `filter` to pull the information list of certain group roles.

| Filter | Description |
|---------|---------|
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ALL | Pull the information list of all group members |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER | Pull the information list of the group owner |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ADMIN | Pull the information list of the group admin |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of ordinary group members |

```java
// Sample code: pull the profile of the group owner using the filter parameter
int role = V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER;
V2TIMManager.getGroupManager().getGroupMemberList("testGroup", role, 0, 
    new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
	@Override
	public void onError(int code, String desc) {
		// Failed to pull
	}

	@Override
	public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
		// Pulled successfully
	}
});
```

#### Pulling paginated results with nextSeq
In many cases, it makes more sense for the user interface to display the first page of the group member list instead of the complete list. More group members can be pulled when the user clicks "Next Page" or pull the list to refresh. For this scenario, you can apply the method of pulling paginated results.

The [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API returns a maximum of 50 members at a time. You can use the pagination flag `nextSeq` to pull a paginated group member list. In the first attempt to pull the group member list, enter 0 for `nextSeq`. When the first pull succeeds, `getGroupMemberList`’s callback result [V2TIMGroupMemberInfoResult](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html) contains the [getNextSeq()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) API.
- If [getNextSeq()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) returns 0, the complete group member list has been pulled.
- If [getNextSeq()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) returns a value greater than 0, there remains group member information to be pulled. You can then decide whether to make another call to pull group member information based on the user’s action on the UI. In the second pull, you need to pass the [getNextSeq()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) in the `V2TIMGroupMemberInfoResult` returned from the previous pull as parameter to the [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API.

```java
// Sample code: pull paginated group member list using nextSeq
{
	...
	long nextSeq = 0;
	getGroupMemberList(nextSeq);
	...
}
public void getGroupMemberList(long nextSeq) {
	int filterRole = V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ALL;
	V2TIMManager.getGroupManager().getGroupMemberList("testGroup", filterRole, nextSeq, 
	    new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
		@Override
		public void onError(int code, String desc) {
			// Failed to pull
		}

		@Override
		public void onSuccess(V2TIMGroupMemberInfoResult groupMemberInfoResult) {
			if (groupMemberInfoResult.getNextSeq() != 0) {
				// Make another pull
				getGroupMemberList(groupMemberInfoResult.getNextSeq());
				...
			} else {
				// Pull ends
			}
		}
	});
}
```


### Getting the profiles of group members
To obtain the profile of a group member, call the [getGroupMembersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5) API. You can pass in multiple `userID` values at one time to obtain profiles of groups, which improves network transmission efficiency.

### Modifying group member profiles
The group owner or admin can call the [setGroupMemberInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b) API to modify group-related information of members, including group name card (`nameCard`), group member role (`role`), and muting duration (`muteUntil`).



<span id="mute"> </span>
### Muting
The group owner or admin can mute a group member and set a muting duration (in seconds) via [muteGroupMember](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5). Muting information is stored in the [muteUtil](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberFullInfo.html#a2caecbec07bdd4fa8e6b8072bc39be58) field of the group member. After the group member is muted, all group members (including the muted member) receive the [onGroupMemberInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a6d8bdea63f14a03faffeb21a274a1e12) callback.
The group owner or admin can mute the entire group via the [setGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) API by setting [allMuted](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#a6faf73364372206bfee9c2b99ed5807e) to `true`. There is no time limit for muting the group. The group can be unmuted through `setAllMuted(false)` in the group profile.


<span id="kick"> </span>
### Removing group members
The group owner or admin can call the [kickGroupMember](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a2e4816131f15187ccfcee8fe30e69cda) API to remove a group member. As a live streaming group (AVChatRoom) can have unlimited members, it does not support this API. You can use [muteGroupMember](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5) to achieve the same effect instead.
After the member is removed, all group members (including the removed member) receive the [onMemberKicked](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2874b768866c2d255144c128a766c7fe) callback.

### Changing group member roles
The group owner can call [setGroupMemberRole](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8) to change the role of a member of a social networking group (Public) or temporary meeting group (Meeting). Roles available for changing are ordinary member and group admin.
- After a member is set as group admin, all group members (including the new admin) receive the [onGrantAdministrator](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ae4e23c72489eafc882a40a24f36f1ae9) callback.
- After the admin role is removed for a member, all group members (including the member with admin role removed) receive the [onRevokeAdministrator](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a089480ee71485b5842c75b8c1985f72f) callback.

<span id="transfer"> </span>
### Transferring a group
The group owner can call [transferGroupOwner](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4) to transfer the ownership of the group to another group member.
After the group ownership is transferred, all group members receive the [onGroupInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad5968cdb7ca01e2f7a702e2ca2f648fb) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

## FAQs

### 1. Can a live streaming group (AVChatRoom) continue to receive messages after it is disconnected and then reconnected?
Yes, but since live streaming groups (AVChatRoom) do not support storing message history in the cloud, it cannot pull the messages that were sent when it was disconnected.

### 2. Why doesn’t the group receive notifications when a user joins or quits the group?
Verify the group type:
- Temporary meeting groups (Meeting) do not support member change notifications.
- Live streaming groups (AVChatRoom) can receive up to 40 messages per second, and it prioritizes the receiving and sending of high-priority messages and discards messages with the lowest priority first once the frequency limit is exceeded.

### 3. Why does the unread count of temporary meeting groups (Meeting) remain at 0?
Temporary meeting groups (Meeting) and live streaming groups (AVChatRoom) are designed for conference and live streaming scenarios respectively, and they do not support the unread count feature.


