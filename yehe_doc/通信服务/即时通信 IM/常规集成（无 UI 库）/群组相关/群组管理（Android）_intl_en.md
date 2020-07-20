<span id="type"> </span>
## Group Types
Instant Messaging (IM) supports the following group types:
- A **work group for friends (Work group)** is similar to an ordinary WeChat group. After a Work group is created, a user can only join the group by being invited by a friend who is a member of the group. The invitation does not need to be accepted by the invitee or approved by the group owner. 
- A **social networking group for strangers (Public group)** is similar to a QQ group. After a Public group is created, a user can join the group by sending an application or being invited by a group member. The invitation needs to be both accepted by the invitee and approved by the group owner or admin.
- A **temporary meeting group (Meeting group)** allows users to join and leave freely and allows members to view messages from the period before they joined the group. Meeting groups are ideal for scenarios that use Tencent Real-Time Communication (TRTC), such as audio-and-video conferencing and online education.
- A **live streaming group (AVChatRoom)** allows users to join and leave freely, supports an unlimited number of members, and does not store the message history. AVChatRoom groups can be used with Live Video Broadcasting (LVB) to support on-screen comments.


The following table describes the features and limitations of each group type:
>For Pro Edition or Flagship Edition SDKAppIDs, the maximum net increase in group quantity per day is 10,000 for all group types. The free peak group count is 100,000 per month, and you will need to <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">pay for usage exceeding the free quota</a>.

<table>
<tr>
<th>Feature</th>
<th>Work Group</th>
<th>Public Group</th>
<th>Meeting Group</th>
<th>AVChatRoom</th>
</tr>
<tr>
<td>Number of groups</td>
<td><ul style="margin:0;"><li>Trial Edition: up to 100 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition or Flagship Edition: unlimited</li></ul></td>
<td><ul style="margin:0;"><li>Trial Edition: up to 100 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition or Flagship Edition: unlimited</li></ul></td>
<td><ul style="margin:0;"><li>Trial Edition: up to 100 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition or Flagship Edition: unlimited</li></ul></td>
<td><ul style="margin:0;"><li>Trial Edition: up to 10 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition: up to 50 existing groups, and disbanded groups do not count against the quota<br>You can upgrade to unlimited number of AVChatRoom groups by purchasing a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li><li>Flagship Edition: unlimited</li></ul></td>
</tr>
<tr>
<td>Number of group members</td>
<td><ul style="margin:0;"><li>Trial Edition: 20 per group</li><li>Pro Edition: 200 per group by default, and can be increased to 6,000 per group by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li><li>Flagship Edition: 2,000 per group, and can be increased to 6,000 per group by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li></ul></td>
<td><ul style="margin:0;"><li>Trial Edition: 20 per group</li><li>Pro Edition: 200 per group by default, and can be increased to 6,000 per group by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li><li>Flagship Edition: 2,000 per group, and can be increased to 6,000 per group by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li></ul></td>
<td><ul style="margin:0;"><li>Trial Edition: 20 per group</li><li>Pro Edition: 200 per group by default, and can be increased to 6,000 per group by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li><li>Flagship Edition: 2,000 per group, and can be increased to 6,000 per group by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li></ul></td>
<td>Unlimited number of group members</td>
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
<td>Supported with group owner or group admin approval required</td>
<td>Supported with no approval required</td>
<td>Supported with no approval required</td>
</tr>
<tr>
<td>Joining a group through invitation by a group member</td>
<td>Supported, and invitation can be initiated by any member</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Exiting a group by the group owner</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Who can modify the group profile</td>
<td>Any group member</td>
<td>Group owner and group admin</td>
<td>Group owner and group admin</td>
<td>Group owner</td>
</tr>
<tr>
<td>Who can remove members from a group</td>
<td>Group owner</td>
<td>Group owner and group admin. Group admins can only remove ordinary group members.</td>
<td>Group owner and group admin. Group admins can only remove ordinary group members.</td>
<td>Group members cannot be removed. The same effect can be achieved by muting members.</td>
</tr>
<tr>
<td>Who can mute members</td>
<td>Muting members is not supported.</td>
<td>Group owner and group admin. Group admins can only mute ordinary group members.</td>
<td>Group owner and group admin. Group admins can only mute ordinary group members.</td>
<td>Group owner</td>
</tr>
<tr>
<td>Unread message counting</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Storing historical messages in the cloud</td>
<td><ul style="margin:0;"><li>Trial Edition: 7 days</li><li>Pro Edition: 7 days by default, and can be extended to up to 360 days by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li><li>Flagship Edition: 30 days by default, and can be extended to up to 360 days by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li></ul></td>
<td><ul style="margin:0;"><li>Trial Edition: 7 days</li><li>Pro Edition: 7 days by default, and can be extended to up to 360 days by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li><li>Flagship Edition: 30 days by default, and can be extended to up to 360 days by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li></ul></td>
<td><ul style="margin:0;"><li>Trial Edition: 7 days</li><li>Pro Edition: 7 days by default, and can be extended to up to 360 days by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li><li>Flagship Edition: 30 days by default, and can be extended to up to 360 days by using a <a href="https://intl.cloud.tencent.com/document/product/1047/34350" target="_blank">value-added service</a></li></ul></td>
<td>Not supported</td>
</tr>
<tr>
<td>Viewing the message history of the period earlier than the joining time of a member</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
</table>

## Group Management
<span id="create"> </span>
### Creating a group
#### Simple API
You can quickly create a group by calling the [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) API and specifying `groupType`, `groupID`, and `groupName`.

#### Advanced API
To initialize group information, such as the group introduction, group profile photo, and initial group members, when creating a group, call the [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) API in the `V2TIMGroupManager` management class. The `V2TIMGroupManager` management class can be obtained from `V2TIMManager.getGroupManager`.

```
// Sample code for creating a Work group through the advanced createGroup API 
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
		// Failed to create the group
	}
	@Override
	public void onSuccess(String groupID) {
		// Created the group successfully
	}
});
```

- The value of `groupType` is a string and can be "Work", "Public", "Meeting", or "AVChatRoom". To learn about the differences among group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` under the same SDKAppID. If you set `groupID` to null, you will be assigned a group ID by default.
- `groupName` specifies the group description, whose maximum length is 30 bytes.

<span id="join"> </span>
### Joining a group
Group joining processes for different group types are described as follows:

| Type | Work Group (Work) | Social Networking Group (Public) | Temporary Meeting Group (Meeting) | Live Streaming Group (AVChatRoom) |
|---------|---------|---------|---------|---------|
| How to join a group | Must be invited by a group member | User joins the group after the application is approved by the group owner or group admin | User can join freely | User can join freely |

#### Scenario 1: users can join and exit the group freely
Meeting groups and AVChatRoom groups can be used for interactive scenarios where users join and exit the group frequently, such as online conferences and runway live streaming. Therefore, the joining procedure is very simple for these groups.

After a user successfully joins a group by calling [joinGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564), all group members (including the joined user) receive the [onMemberEnter](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) callback. 

#### Scenario 2: users must be invited to the group
Similar to WeChat and WeChat Work groups, Work groups are suitable for communication in work environments. The interaction pattern is designed to deny active group joining and only allows users to be invited to a group by existing group members.

A group member calls [inviteUserToGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92) to invite a user to the group. Then, all group members (including the inviter) receive the [onMemberInvited](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#af6119ca3c6eabcc63acbf012f508b1b1) callback.

#### Scenario 3: users join the group after applications are approved
Public groups are similar to the interest groups and tribes in QQ. Any user can apply to join a group of this type, but will not become a member of the group until the application is approved by the group owner or group admin. While approval is required by default, the group owner or group admin can call the [setGroupInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) API to set the group joining option (`V2TIMGroupAddOpt`) to "forbid anyone to join" (which imposes stricter restrictions) or to "disable the approval process" (which loosens the restrictions).
- V2TIM_GROUP_ADD_FORBID: forbid anyone to join the group.
- V2TIM_GROUP_ADD_AUTH: (default) group owner or admin approval is required for group joining.
- V2TIM_GROUP_ADD_ANY: disable the approval process to allow any user to join the group.

1. **The user sends an application to join the group.**
The user calls [joinGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) to apply to join the group.
2. **The group owner or group admin handles the group joining application.**
After the [onReceiveJoinApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#adf0b34684efd46d6e31d31e7bc3643f9) callback is received, the group owner or group admin calls [getGroupApplicationList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4) to obtain the list of group joining applications and approves or rejects applications by using [acceptGroupApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07) or [refuseGroupApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd).
3. **The applicant receives the approval result.**
 The user receives the [onApplicationProcessed](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac833c624e33036ec0454fe5444b8f00a) callback in [V2TIMGroupListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html). If `isAgreeJoin` is `true`, the application was approved, otherwise the application was rejected. If the application was approved, all members (including the requester) receive the [onMemberEnter](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) callback.



<span id="quit"> </span>
### Exiting a group
Call [quitGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919) to exit a group. The user who exits the group then receives the [onQuitFromGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a489004526f1bd8daba7ac63fb0ad965f) callback, and other group members receive the [onMemberLeave](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2169676423875e4c9c376796245ca8d5) callback.
>The group owner of a Public group, Meeting group, or AVChatRoom group is not allowed to exit the group. Instead, the group owner can [disband the group](#dismiss).

<span id="dismiss"> </span>
### Disbanding a group
Call [dismissGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb) to disband a group. Then, all group members receive the [onGroupDismissed](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a6e89728e160e126460a6b8eeddf00ad5) callback.

> 
>- The group owner can disband a Public group, Meeting group, or AVChatRoom group at any time.
>- For a Work group, the group owner does not have the privilege to disband the group. To disband the group, you must have your business server call the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34896).


### Obtaining the list of joined groups
Call [getJoinedGroupList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a05bfd8f7df6bfba718abc96fdad49791) to obtain the list of Work groups, Public groups, and Meeting groups the current user has joined. AVChatRoom groups are excluded from this list.

## Group Profiles and Group Settings
### Obtaining group profiles
Call [getGroupsInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154) to obtain the group profile of one or more groups at a time. To obtain the group profiles of multiple groups with a single call, pass in multiple `groupID` values at a time.

### Modifying group profiles
Call [setGroupInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) to modify the group profile. When the modification is completed, all group members receive the [onGroupInfoChanged](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad5968cdb7ca01e2f7a702e2ca2f648fb) callback.
>
> - For Work groups, all group members can modify the basic group profile.
> - For Public groups and Meeting groups, only the group owner and group admin can modify the basic group profile.
> - For AVChatRoom groups, only the group owner can modify the basic group profile.

```
// Sample code for modifying the group profile
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupID("<ID of the group whose group profile needs to be modified>");
v2TIMGroupInfo.setFaceUrl("http://xxxx");
V2TIMManager.getAdvancedGroupManager().setGroupInfo(v2TIMGroupInfo, new V2TIMCallback() {
		@Override
		public void onError(int code, String desc) {
			// Failed to modify the group profile
		}
		@Override
		public void onSuccess() {
			// Modified the group profile successfully
		}
});
```

### Setting the group message receiving option
Any group member can call the [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6bf8f3eafb5ffcb1d13bd69231de8bd4) API to modify the group message receiving option. Possible values of this option are as follows:
- V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_MESSAGE: messages will be received when the user is online, and push notifications will be received when the user is offline.
- V2TIMGroupInfo.V2TIM_GROUP_NOT_RECEIVE_MESSAGE: no group messages will be received.
- V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE: messages will be received when the user is online, and no push notifications will be received when the user is offline.

The group message receiving option enables you to mute group messages:
- **No group messages will be received**
With the group message receiving option set to `V2TIMGroupInfo.V2TIM_GROUP_NOT_RECEIVE_MESSAGE`, no group messages will be received, and the conversation list will not be updated.
- **Group messages will be received but the user will not be notified, and a badge without the unread count will be displayed on the conversation list interface**
>Unread counting needs to be enabled for this to work. Therefore, it only applies to Work groups and Public groups.
>
With the group message receiving option set to `V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, when new group messages are received and the conversation list needs to be updated, you can obtain the unread count through [getUnreadCount](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e). In this case, use [getRecvOpt](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) to verify that the group message receiving option is set to `V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE` and then display a badge without the unread count.

## Group Member Management
### Obtaining the group member list
Call [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) to obtain the list of group members of a given group. The list contains profile information of individual members, such as their user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining the group (`joinTime`).
As a group might have a large number of members (even over 5,000), this API supports two advanced properties: `filter` and `nextSeq`.

#### Filter
When calling [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be), you can specify `filter` to pull the information list of certain group members.

| Filter | Description |
|---------|---------|
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ALL | Pull the information list of all group members |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER | Pull the information list of the group owner |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ADMIN | Pull the information list of group admins |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of ordinary group members |

```java
// Sample code for pulling the profile of the group owner by using the filter parameter
int role = V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER;
V2TIMManager.getGroupManager().getGroupMemberList("testGroup", role, 0, 
    new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
	@Override
	public void onError(int code, String desc) {
		// Failed to pull the information
	}

	@Override
	public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
		// Pulled the information successfully
	}
});
```

#### Pulling paginated results with nextSeq
In many cases, it makes more sense for the user interface to display the first page of the group member list instead of the full list. More group members can be pulled when the user clicks "Next Page" or slides down on the list to refresh. In this scenario, you can apply the method for pulling paginated results.

The [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API returns a maximum of 50 members at a time. You can use the `nextSeq` pagination flag to pull the paginated group member list. In the first attempt to pull the group member list, enter 0 for `nextSeq`. When the first pull succeeds, the `getGroupMemberList` callback result [V2TIMGroupMemberInfoResult](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html) contains the [getNextSeq()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) API.
- If [getNextSeq()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) returns 0, the full group member list has been pulled.
- If [getNextSeq()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) returns a value greater than 0, in indicates that additional group member information can be pulled. In this case, you can decide whether to make another call to pull more group member information based on the user’s action on the UI. During the second pull, you need to pass in the [getNextSeq()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) in the `V2TIMGroupMemberInfoResult` returned from the previous pull as a parameter to the [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API.

```java
// Sample code for pulling the paginated group member list by using nextSeq
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
			// Failed to pull the list
		}

		@Override
		public void onSuccess(V2TIMGroupMemberInfoResult groupMemberInfoResult) {
			if (groupMemberInfoResult.getNextSeq() != 0) {
				// Continue to pull the list
				getGroupMemberList(groupMemberInfoResult.getNextSeq());
				...
			} else {
				// Pull ended
			}
		}
	});
}
```


### Obtaining the profiles of group members
Call [getGroupMembersInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5) to obtain the profiles of group members in batches. You can pass in multiple `userID` values at a time to improve network transmission efficiency.

### Modifying group name cards for members
The group owner or group admin can call the [setGroupMemberInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b) API to modify group-related information for members, including the group name card (`nameCard`), group member role (`role`), and muting duration (`muteUntil`).

```
// Sample code for changing the group name card of group member denny to denny-tencent 
V2TIMGroupMemberFullInfo v2TIMGroupMemberFullInfo = new V2TIMGroupMemberFullInfo();
v2TIMGroupMemberFullInfo.setUserID("denny");
v2TIMGroupMemberFullInfo.setNameCard("denny-tencent");
V2TIMManager.getAdvancedGroupManager().setGroupMemberInfo(
    groupID, v2TIMGroupMemberFullInfo, new V2TIMCallback() {
	@Override
	public void onError(int code, String desc) {
		// Failed to change the group name card
	}
	@Override
	public void onSuccess() {
		// Changed the group name card successfully
	}
});
```

<span id="mute"> </span>
### Muting
The group owner or group admin can mute a group member and set a muting duration (in seconds) through [muteGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5). Muting information is stored in the [muteUtil](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberFullInfo.html#a2caecbec07bdd4fa8e6b8072bc39be58) field of the group member. After the group member is muted, all group members (including the muted member) receive the [onGroupMemberInfoChanged](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a6d8bdea63f14a03faffeb21a274a1e12) callback.
The group owner or group admin can mute the entire group through the [setGroupInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) API by setting [allMuted](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#a6faf73364372206bfee9c2b99ed5807e) to `true`. There is no time limit for group muting. The group can be unmuted by using `setAllMuted(false)` in the group profile.


<span id="kick"> </span>
### Removing group members
The group owner or group admin can call the [kickGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a2e4816131f15187ccfcee8fe30e69cda) API to remove a group member. As an AVChatRoom group can have unlimited members, it does not support the API. Instead, you can use [muteGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5) for the same purpose.
After the member is removed, all group members (including the removed member) receive the [onMemberKicked](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2874b768866c2d255144c128a766c7fe) callback.

### Changing group member roles
The group owner can call [setGroupMemberRole](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8) to change the role of a member of a Public group or Meeting group. You can change the role to ordinary member or group admin.
- After a member is set as a group admin, all group members (including the new admin) receive the [onGrantAdministrator](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ae4e23c72489eafc882a40a24f36f1ae9) callback.
- After the admin role is removed from a member, all group members (including the member whose admin role was removed) receive the [onRevokeAdministrator](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a089480ee71485b5842c75b8c1985f72f) callback.

<span id="transfer"> </span>
### Transferring a group
The group owner can call [transferGroupOwner](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4) to transfer the ownership of a group to another group member.
After the group ownership is transferred, all group members receive the [onGroupInfoChanged](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad5968cdb7ca01e2f7a702e2ca2f648fb) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

## FAQs

### 1. Can an AVChatRoom group continue to receive messages after it was disconnected and then reconnected?
Yes. However, AVChatRoom groups do not support storing the message history in the cloud, and it cannot pull the messages that were sent when it was disconnected.

### 2. Why no notifications are received when users join or exit the group?
Check the following reasons for different group types:
- Meeting groups do not support member change notifications.
- An AVChatRoom group can receive up to 40 messages per second, and therefore the group prioritizes the sending and receiving of high-priority messages and discards messages with the lowest priority once the frequency limit is exceeded.

### 3. Why does the unread count of a Meeting group remain at 0?
Meeting groups and AVChatRoom groups are designed for conferencing and livestreaming scenarios respectively, so they do not support unread counting.


