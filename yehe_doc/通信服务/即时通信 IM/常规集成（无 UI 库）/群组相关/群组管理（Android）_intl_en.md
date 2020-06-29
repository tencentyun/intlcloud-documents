<span id="type"> </span>
## Group Types
Instant Messaging (IM) supports the following group types:
- *Work group**: similar to an ordinary WeChat group. After a work group is created, only a group member can invite other users to join this group, and the invitation does not need to be approved by the invited user or group owner. 
- **Public group**: similar to a QQ group. After a public group is created, the group owner can specify a group admin. When a user searches for the group ID and initiates a request to join the group, the request must be approved by the group owner or admin before the user can join the group.
- **Meeting group**: after a meeting group is created, users can join and quit the group as they please and view messages from before they joined the group. This group type is suitable for scenarios where Tencent Real-Time Communication (TRTC) is used, for example, audio and video conferencing and online education.
- **Livestreaming group (AVChatRoom)**: after an AVChatRoom is created, users can join and quit the group as they please. This group type does not limit the number of members, but it does not support the storage of historical messages. It can be used together with Live Video Broadcasting (LVB) to support on-screen comments.


The following table describes the features and limitations of each group type:

<table>
<tr>
<th width="20%">Feature</th>
<th width="16%">Work group</th>
<th width="16%">Public group</th>
<th width="16%">Meeting group</th>
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
<td>Applying to join a group</td>
<td>Not supported</td>
<td>Supported. An approval from the group owner or group admin is needed.</td>
<td>Supported. No approval is needed.</td>
<td>Supported. No approval is needed.</td>
</tr>
<tr>
<td>Joining group after receiving an invitation from a group member</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Allowing the group owner to quit the group</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Having permission to modify the group profile</td>
<td>Any group member</td>
<td>Group owner and group admin</td>
<td>Group owner and group admin</td>
<td>Group owner</td>
</tr>
<tr>
<td>Having permission to remove members from the group</td>
<td>Group owner</td>
<td colspan="2">Group owner and group admin. The group admin can only remove ordinary group members.</td>
<td>Group members cannot be removed. A member can be muted to achieve the same effect as removing a member.</td>
</tr>
<tr>
<td>Having the permission to mute members</td>
<td>Not supported</td>
<td colspan="2">Group owner and group admin.
	The group admin can only mute ordinary group members.</td>
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
<td>Viewing historical messages from before the user joined the group</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Storing historical messages in the cloud</td>
<td colspan="3"><ul style="margin:0;padding-left:10px" ><li>Trial Edition: 7 days</li><li>Pro Edition: 7 days by default; up to 360 days if the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service is purchased</a></li><li>Flagship Edition: 30 days by default; up to 360 days if the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service is purchased</a></li></ul></td>
<td>Not supported</td>
</tr>
<tr>
<td>Number of groups</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: up to 100 existing groups, excluding disbanded groups</li><li>Pro Edition or Flagship Edition: unlimited</li></ul></td>
<td><ul style="margin:0;padding-left:10px"><li>Trial Edition: up to 10 existing groups, excluding disbanded groups</li><li>Pro Edition: up to 50 existing groups, excluding disbanded groups<br>The number of groups is unlimited if the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> is purchased</li><li>Flagship Edition: unlimited</li></ul></td>
</tr>
<tr>
<td>Number of group members</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Trial Edition: 20 members per group</li><li>Pro Edition: 200 members per group by default; up to 2,000 members per group if the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> is purchased</li><li>Flagship Edition: 2,000 per group; up to 6,000 members per group if the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> is purchased</li></ul></td>
<td>Unlimited</td>
</tr>
</table>

> For an SDKAppID of Pro Edition or Flagship Edition, a net increase of up to 10,000 groups, regardless of the group type, is allowed in a single day. Up to 100,000 groups can be added for free in a month. If this quota is exceeded, <a href="https://intl.cloud.tencent.com/document/product/1047/34350">fees for usage exceeding the free quota</a> will be charged.


## Group Management
<span id="create"> </span>
### Creating a group
#### Simplified API
You can quickly create a group by calling the [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) API and specifying `groupType`, `groupID`, and `groupName`.

#### Advanced API
When creating a group, if you also want to initialize group information, such as the group introduction, group profile photo, and initial group members, call the [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) API in the `V2TIMGroupManager` management class. To obtain this management class, call `V2TIMManager.getGroupManager`.

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
		// Creation failed
	}
	@Override
	public void onSuccess(String groupID) {
		// Created successfully
	}
});
```

- `groupType` is a string-type parameter. Valid values include “Work”, “Public”, “Meeting”, and “AVChatRoom”. To learn about the differences among group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` within the same SDKAppID. If you set `groupID` to null, a group ID is assigned by default.
- `groupName` specifies the group description, which has a maximum length of 30 bytes.

<span id="join"> </span>
### Joining a group
The method for joining a group varies with the group type. The following table describes the specific methods from simple to complex.

| Type | Work Group | Public Group | Meeting Group | AVChatRoom |
|---------|---------|---------|---------|---------|
| Method for joining a group | A user can join this group only after being invited by a group member. | A user can join this group after the application is approved by the group owner or admin. | A user can join this group as desired. | A user can join this group as desired. |

#### Scenario 1: a user joins and quits a group as desired
Meeting groups and AVChatRooms can be used for interactive scenarios where users join and quit the group frequently, such as online conferences and LVB. Therefore, the process of joining these two types of groups is the simplest.

A user can join a group simply by calling [joinGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564). After the user joins the group, all group members (including the user who just joined the group) receive the [onMemberEnter](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) callback. 

#### Scenario 2: a user joins a group only after being invited
A work group is similar to a WeChat group or a WeChat Work group, and is suitable for work-related communication. The interaction pattern is designed to allow a user to join a group only after the user is invited by a member in this group.

A group member can call [inviteUserToGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92) to invite a user to join the group. Then, all group members (including the inviter) receive the [onMemberInvited](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#af6119ca3c6eabcc63acbf012f508b1b1) callback.

#### Scenario 3: a user joins a group only after the application is approved
A public group is similar to an interest group or a tribe in QQ. Any user can apply to join the group, but will not become a member of the group until the application is approved by the group owner or admin. While the approval is required by default, the group owner or admin can call the [setGroupInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) API to set the group joining option `V2TIMGroupAddOpt` to one of the following values:
- V2TIM_GROUP_ADD_FORBID: forbid anyone to join the group.
- V2TIM_GROUP_ADD_AUTH: (default) obtain approval from the group owner or admin before a user can join the group.
- V2TIM_GROUP_ADD_ANY: disable the approval process to allow any user to join the group.

1. **The user sends an application to join the group**
The user calls [joinGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) to send an application for joining the group.
2. **The group owner or admin processes the application**
After receiving the [onReceiveJoinApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#adf0b34684efd46d6e31d31e7bc3643f9) callback, the group owner or admin calls [getGroupApplicationList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4) to obtain the list of applications, and calls [acceptGroupApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07) or [refuseGroupApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd) to approve or reject applications.
3. **The applicant receives the application processing result**
 The user receives the [onApplicationProcessed](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac833c624e33036ec0454fe5444b8f00a) callback in [V2TIMGroupListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html). If `isAgreeJoin` is `true`, the application is approved. Otherwise, the application is rejected. If the application is approved, all members (including the applicant) receive the [onMemberEnter](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) callback.



<span id="quit"> </span>
### Quitting a group
To quit a group, call [quitGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919). Then, the user who quits the group receives the [onQuitFromGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a489004526f1bd8daba7ac63fb0ad965f) callback, and other group members receive the [onMemberLeave](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2169676423875e4c9c376796245ca8d5) callback.
> The group owner of a public group, a meeting group, or an AVChatRoom is not allowed to quit the group, and can only [disband the group](#dismiss).

<span id="dismiss"> </span>
### Disbanding a group
To disband a group, call [dismissGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb). Then, all group members receive the [onGroupDismissed](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a6e89728e160e126460a6b8eeddf00ad5) callback.

> 
>- The group owner of a public group, a meeting group, or an AVChatRoom can disband the group at any time.
>- The group owner of a work group is not authorized to disband the group. To disband the group, call the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34896) from your business server.


### Obtaining the list of joined groups
To obtain a list of work groups, public groups, and meeting groups that a user has joined, call [getJoinedGroupList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a05bfd8f7df6bfba718abc96fdad49791). AVChatRooms are excluded from this list.

## Group Profiles and Group Settings
### Obtaining group profiles
To obtain group profiles, call [getGroupsInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154). You can pass in multiple `groupID` values at a time to obtain profiles of multiple groups in a batch.

### Modifying a group profile
To modify a group profile, call [setGroupInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4). After the modification, all group members receive the [onGroupInfoChanged](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad5968cdb7ca01e2f7a702e2ca2f648fb) callback.
>
> - For a work group, all group members can modify the basic group profile.
> - For a public or meeting group, only the group owner and admin can modify the basic group profile.
> - For an AVChatRoom, only the group owner can modify the group profile.

```
// Sample code: modify the group profile
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupID("the ID of the target group");
v2TIMGroupInfo.setFaceUrl("http://xxxx");
V2TIMManager.getGroupManager().setGroupInfo(v2TIMGroupInfo, new V2TIMCallback() {
		@Override
		public void onError(int code, String desc) {
			// Failed
		}
		@Override
		public void onSuccess() {
			// Succeeded
		}
});
```

### Setting the group message receiving option
Any group member can call the [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6bf8f3eafb5ffcb1d13bd69231de8bd4) API to modify the group message receiving option. Valid values are as follows:
- V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_MESSAGE: group messages are received normally if the user is online, and offline push notifications are received through the vendor’s offline push service if the user is offline.
- V2TIMGroupInfo.V2TIM_GROUP_NOT_RECEIVE_MESSAGE: no group messages are received.
- V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE: group messages are received normally if the user is online, but no offline push notifications are received from the vendor if the user is offline.

You can set the group message receiving option to mute group message notifications:
- **No group messages are received**
After the group message receiving option is set to `V2TIMGroupInfo.V2TIM_GROUP_NOT_RECEIVE_MESSAGE`, no group messages are received, and the conversation list is not updated.
- **Group messages are received, but the user is not notified. A red dot, instead of the unread count, is displayed on the conversation list**
> This configuration requires that the unread count feature be enabled. Therefore, it only applies to work groups and public groups.
>
If the group message receiving option is set to `V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, when new group messages are received and the conversation list needs to be updated, call [getUnreadCount](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e) to obtain the unread count. When the obtained group message receiving option is `V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, use [getRecvOpt](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) to check whether a red dot, instead of the unread count, is displayed.

## Group Member Management
### Obtaining the list of group members
To obtain the member list of a group, call [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be). The list contains profile information of each group member, such as the user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining the group (`joinTime`).
A group may have many members, even over 5,000 members. Therefore, this API provides two advanced features: filter (`filter`) and pulling by page (`nextSeq`).

#### filter
When calling [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be), you can set `filter` to pull the information list of the specified role.

| Filter | Description |
|---------|---------|
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ALL | Pull the information list of all group members. |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER | Pull the information list of the group owner. |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ADMIN | Pull the information list of the group admins. |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of ordinary group members. |

```java
// Sample code: pull the profile of the group owner using `filter`
int role = V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER;
V2TIMManager.getGroupManager().getGroupMemberList("testGroup", role, 0, 
    new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
	@Override
	public void onError(int code, String desc) {
		// Failed to pull the information list
	}

	@Override
	public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
		// Succeeded in pulling the information list
	}
});
```

#### nextSeq
In many cases, only the first page of the group member list, instead of the entire member list of the group, needs to be displayed on the user interface (UI). Information for more group members needs to be pulled only when the user taps **Next**, or pulls down the list. In this scenario, you can specify `nextSeq` to pull the information by page.

When the [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API is called, a maximum of 50 members are returned at a time. You can use `nextSeq` to pull the group member list by page. When the list is pulled for the first time, set `nextSeq` to 0. After the list is pulled successfully for the first time, the `getGroupMemberList` callback result [V2TIMGroupMemberInfoResult](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html) contains the [getNextSeq()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) API.
- If [getNextSeq()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) returns 0, the entire group member list has been pulled.
- If [getNextSeq()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) returns a value greater than 0, more content of the group member list has yet to be pulled. You can then decide whether to call the API again to pull more group member information based on the user’s operation on the UI. To pull the list for the second time, you need to pass in [getNextSeq()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) in `V2TIMGroupMemberInfoResult` returned from the previous call as a parameter to the [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API.

```java
// Sample code: pull the group member list by page using `nextSeq`
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
			// Failed to pull the information list
		}

		@Override
		public void onSuccess(V2TIMGroupMemberInfoResult groupMemberInfoResult) {
			if (groupMemberInfoResult.getNextSeq() != 0) {
				// Continue to pull by page
				getGroupMemberList(groupMemberInfoResult.getNextSeq());
				...
			} else {
				// End of pulling
			}
		}
	});
}
```


### Obtaining the profile of a group member
To obtain the profile of a group member, call [getGroupMembersInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5). You can pass in multiple `userID` values at a time to obtain profiles of multiple group members, which improves network transmission efficiency.

### Modifying the group name card for a member
The group owner or admin can call the [setGroupMemberInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b) API to modify group-related information of a member, including the group name card (`nameCard`), group member role (`role`), and muting duration (`muteUntil`).

```
// Sample code: change the group name card of the group member Denny to "denny-tencent" 
V2TIMGroupMemberFullInfo v2TIMGroupMemberFullInfo = new V2TIMGroupMemberFullInfo();
v2TIMGroupMemberFullInfo.setUserID("denny");
v2TIMGroupMemberFullInfo.setNameCard("denny-tencent");
V2TIMManager.getGroupManager().setGroupMemberInfo(
    groupID, v2TIMGroupMemberFullInfo, new V2TIMCallback() {
	@Override
	public void onError(int code, String desc) {
		// Failed
	}
	@Override
	public void onSuccess() {
		// Succeeded
	}
});
```

<span id="mute"> </span>
### Muting
The group owner or admin can mute a group member and set the muting duration (in seconds) by calling [muteGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5). Muting information is stored in the [muteUtil](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberFullInfo.html#a2caecbec07bdd4fa8e6b8072bc39be58) field of the group member. After the group member is muted, all group members (including the muted member) receive the [onGroupMemberInfoChanged](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a6d8bdea63f14a03faffeb21a274a1e12) callback.
The group owner or admin can mute the entire group by calling the [setGroupInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) API and setting [allMuted](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#a6faf73364372206bfee9c2b99ed5807e) to `true`. There is no time limit for group muting. To unmute the group, specify `setAllMuted(false)` in the group profile.


<span id="kick"> </span>
### Removing group members
The group owner or admin can call the [kickGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a2e4816131f15187ccfcee8fe30e69cda) API to remove a group member. This API is not supported by AVChatRooms because an AVChatRoom does not limit the number of members. However, you can call [muteGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5) to achieve the same effect.
After the member is removed, all group members (including the removed member) receive the [onMemberKicked](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2874b768866c2d255144c128a766c7fe) callback.

### Changing the role of a group member
The group owner can call [setGroupMemberRole](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8) to change the role of a member in a public or meeting group. Only the role of an ordinary member or a group admin can be changed.
- After a member is set as a group admin, all group members (including the new admin) receive the [onGrantAdministrator](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ae4e23c72489eafc882a40a24f36f1ae9) callback.
- After the admin role of a member is revoked, all group members (including the member whose admin role is revoked) receive the [onRevokeAdministrator](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a089480ee71485b5842c75b8c1985f72f) callback.

<span id="transfer"> </span>
### Transferring the group owner role
The group owner can call [transferGroupOwner](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4) to transfer his/her role as the group owner to another group member.
After the transfer, all group members receive the [onGroupInfoChanged](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad5968cdb7ca01e2f7a702e2ca2f648fb) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

## FAQs

### 1. Can an AVChatRoom continue to receive messages after it is disconnected and then reconnected?
Yes. However, as AVChatRooms do not support the storage of historical messages in the cloud, messages exchanged when the AVChatRoom is disconnected cannot be obtained.

### 2. Why can’t notifications be received when users join or quit a group?
Verify the group type:
- A meeting group does not support member change notifications.
- An AVChatRoom can receive up to 40 messages per second. Therefore, high-priority messages are sent or received first, and low-priority messages are the first discarded when the frequency limit is exceeded.

### 3. Why does the unread count of a meeting group remain at 0?
Meeting groups and AVChatRooms are designed for conferencing and livestreaming scenarios respectively. Therefore, these group types do not support the unread count feature.


