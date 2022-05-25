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
>- Group types are upgraded in the new SDK version and they are **work group (Work)**, **public group (Public)**, **meeting group (Meeting)**, **community group (Community)**, and **audio-video group (AVChatRoom)**. Private group (Private) and chat room (ChatRoom) in earlier versions (which have Public, Private, ChatRoom, and AVChatRoom groups) correspond to work group (Work) and meeting group (Meeting) in the new version respectively.
>- In the Pro Edition or Flagship Edition SDKAppID, the maximum net increase in group count per day is 10,000 for all group types. Free peak group count is 100,000 per month, and you will need to <a href="https://intl.cloud.tencent.com/document/product/1047/34350"> pay for usage not covered by the free quota</a>.
>- Community group (Community) is supported only in native SDK 5.8.1668 enhanced edition or higher and web SDK 2.17.0 or later. To use the feature, you need to purchase the Flagship Edition package and [apply for activation](https://intl.cloud.tencent.com/document/product/1047/44322).
>- Work groups (Work) and public groups (Public) do not allow group members to view messages sent before they join the group. To enable the feature, submit a change request by referring to [Configuration Change Ticket](https://intl.cloud.tencent.com/document/product/1047/44322).


## Group Management
[](id:create)
### Creating a group
#### Simple API
You can quickly create a group by calling the [createGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) API and specifying `groupType`, `groupID`, and `groupName`.

#### Advanced API
If you want to initialize group information (for example, group introduction, group profile photo, and initial group members) when creating a group, call the [createGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) API in the `V2TIMGroupManager` management class. The `V2TIMGroupManager` management class can be obtained via `V2TIMManager.getGroupManager`.

```
// Sample code: Use the advanced `createGroup` API to create a work group 
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
		// Group created successfully
	}
});
```

- The value of `groupType` is a string and can be one of `Work`, `Public`, `Meeting`, or `AVChatRoom`. For the differencesbetween group types, see [Group Types](#type).
- `groupID` specifies the group ID, which uniquely identifies a group. Do not create groups with the same `groupID` in a SDKAppID. If you set `groupID` to `null`, you will be assigned a group ID by default.
- `groupName` specifies the group description, which can have a maximum length of 30 bytes.

[](id:join)

### Joining a group
The group joining method varies according to the group type, as described below:

| Group Type | Work Group (Work) | Public Group (Public) | Meeting Group (Meeting) | Community Group (Community) | Audio-Video Group (AVChatRoom) |
|---------|---------|---------|---------|---------|---------|
| Group Joining Method | Users must be invited by group member. | Users can join the group only after their requests are approved by group owner or admin. | Users can join the group freely. | Users can join the group freely. | Users can join the group freely. |

#### Scenario 1: Users can join the group freely
Meeting groups (Meeting) and audio-video groups (AVChatRoom) can be used for interactive scenarios where users join and leave groups frequently, such as online conferencing and show live streaming. The group joining procedure is therefore the simplest.

After a user successfully joins a group by calling [joinGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564), all group members (including the joined user) receive the [onMemberEnter](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) callback. 

#### Scenario 2: Users must be invited to join the group
Resembling WeChat and WeCom groups, work groups (Work) are suitable for communication in work environments. The interaction pattern is designed to disable proactive group joining and only allow users to be invited to join the group by group members.

A group member calls [inviteUserToGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92) to invite a user to the group, then all group members (including the inviter) receive the [onMemberInvited](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#af6119ca3c6eabcc63acbf012f508b1b1) callback.

#### Scenario 3: Users can join the group only after their requests are approved
Public groups (Public) are similar to interest groups and tribes. Any user can request to join the group, but will not become a member of the group until the request is approved by the group owner or admin. While approval is required by default, the group owner or admin can call the [setGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) API to set the group joining option (`V2TIMGroupAddOpt`) to **forbid anyone to join** which is tighter, or to **disable the approval process**, which is more flexible.
- V2TIM_GROUP_ADD_FORBID: Forbid anyone to join the group.
- V2TIM_GROUP_ADD_AUTH (default): Group owner or admin approval is required for group joining.
- V2TIM_GROUP_ADD_ANY: Disable the approval process to allow any user to join the group.

The diagram illustrates the process of group joining that requires approval:
![](https://main.qcloudimg.com/raw/9164de02268e14b178937bbd85465f4f.png)

1. **The user sends a request to join the group**
The user calls [joinGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) to request to join the group.
2. **The group owner or admin processes the group joining request**
After receiving the [onReceiveJoinApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#adf0b34684efd46d6e31d31e7bc3643f9) callback, the group owner or admin calls the [getGroupApplicationList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4) API to get the list of group joining requests, and accepts or rejects a request with [acceptGroupApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07) or [refuseGroupApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd).
3. **The user receives the result**
 The user receives the [onApplicationProcessed](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac833c624e33036ec0454fe5444b8f00a) callback in [V2TIMGroupListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html). If `isAgreeJoin` is `true`, the request is accepted. Otherwise, the request is rejected. If the request is accepted, all members (including the requester) receive the [onMemberEnter](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) callback.



[](id:quit)
### Leaving a group
Call [quitGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919) to leave a group. The user who leaves the group then receives the [onQuitFromGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a489004526f1bd8daba7ac63fb0ad965f) callback and other group members receive the [onMemberLeave](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2169676423875e4c9c376796245ca8d5) callback.
>!For a public group (Public), meeting group (Meeting), community group (Community), or audio-video group (AVChatRoom), the group owner is not allowed to leave the group but can [delete the group](#dismiss).

[](id:dismiss)
### Deleting a group
Call [dismissGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb) to delete a group. Then all group members receive the [onGroupDismissed](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a6e89728e160e126460a6b8eeddf00ad5) callback.

>! 
>- For a public group (Public), meeting group (Meeting), community group (Community), or audio-video group (AVChatRoom), the group owner can delete the group at any time.
>- For a work group (Work), the group owner does not have the permission to delete the group. To delete the group, you must have your service server call the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34896).


### Getting the list of joined groups
Call [getJoinedGroupList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a05bfd8f7df6bfba718abc96fdad49791) to get a list of work groups (Work), public groups (Public), meeting groups (Meeting), and community groups (Community) the current user has joined. Audio-video groups (AVChatRoom) will not be included in this list.

## Group Profiles and Group Settings
[](id:getGroupsInfo)
### Getting group profiles
Call [getGroupsInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154) to get the group profile of one or more groups at a time. To get the group profiles of multiple groups by a single call, pass in multiple `groupID` values at a time.

[](id:setGroupsInfo)
### Modifying group profiles
Call [setGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) to modify the group profile. When the modification is completed, all group members receive the [onGroupInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad5968cdb7ca01e2f7a702e2ca2f648fb) callback.
>!
> - For work groups (Work), all group members can modify the basic group profile.
> - For public groups (Public), meeting groups (Meeting), and community groups (Community), only the group owner and admin can modify the group profile.
> - For audio-video groups (AVChatRoom), only the group owner can modify the group profile.

```
// Sample code: Modify group profile
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

[](id:setGroupReceiveMessageOpt)
### Setting the group message receiving option
Any group member can call the [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e) API to modify the group message receiving option. Available values are as follows:
- V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_MESSAGE: Messages will be received when the user is online, and push notifications will be received when the user is offline.
- V2TIMGroupInfo.V2TIM_GROUP_NOT_RECEIVE_MESSAGE: No group messages will be received.
- V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE: Messages will be received when the user is online, and no push notification will be received when the user is offline.

The group message receiving option allows you to mute group messages:
- **No group message will be received**
With the group message receiving option set to `V2TIMGroupInfo.V2TIM_GROUP_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.
- **Group messages will be received but the user will not be notified. A badge without the unread count will be displayed on the conversation list interface.**
>?This mode requires the unread count feature and therefore it applies only to work groups (Work) and public groups (Public).
>
With the group message receiving option set to `V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`, when new group messages are received and the conversation list needs to be updated, you can get the unread count through [getUnreadCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e). Use [getRecvOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) to verify that a red dot instead of the unread count is displayed when the group message receiving option is `V2TIMGroupInfo.V2TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE`.

## Group Attributes (Custom Group Fields)
New custom group fields, also called group attributes, are designed based on API 2.0. They have the following features:
1. You can CRUD group attributes directly in the client without console configuration.
2. You can configure up to 16 group attributes. The size of each group attribute can be up to 4 KB, and the total size of all group attributes can be up to 16 KB.
3. Only audio-video groups (AVChatRoom) support group attributes.
4. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs each can be called by the SDK for up to 10 times per five seconds, and the error code 8511 will be called back if the limit is exceeded. The APIs each can be called by the backend for up to five times per second, and the error code 10049 will be called back if the limit is exceeded.
5. The `getGroupAttributes` API can be called by the SDK for up to 20 times per five seconds.

With group attributes, you can manage the seats of audio chat rooms. When a user mic on, you can set a group attribute to manage the information of the user. When the user mic off, you can delete the group attribute. Other members can get the list of group attributes to display the seat list.

### Initializing group attributes
Call the [initGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a17569b57abc77adb6be9356b9eb70182) API to initialize group attributes. If the group has existing group attributes, they will be deleted first.

### Setting group attributes

Call the [setGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3ec31101e4763dab7a1c99a71bc3da08) API to set group attributes. If the group attributes to set do not exist, they will be automatically added.

### Deleting group attributes
Call the [deleteGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a45f211bafddc58bf5e199e18a6814578) API to delete specified group attributes. If you set the `keys` parameter to `null`, all group attributes will be deleted.

### Getting group attributes
Call the [getGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ade2155fb24ed1c0b8eb976e146c14e3d) API to get specified group attributes. If you set the `keys` parameter to `null`, all group attributes will be returned.

### Updating group attributes
If any group attribute is updated, all group attribute fields will be called back via [onGroupAttributeChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#aa390fa93bc73a0262bdddb540227dc45).

## Group Member Management
[](id:getGroupMemberList)
### Getting the group member list
Call [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) to get the list of group members of a given group. The list contains profile information about individual members, such as user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and group joining time (`joinTime`).
As a group might have a large number of members (for example, over 5,000), this API supports two advanced features: filter (`filter`) and pulling by page (`nextSeq`).

#### Filter (`filter`)
When calling the [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API, you can specify `filter` to pull the information of certain roles.

| Filter | Description |
|---------|---------|
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ALL | Pull the information list of all group members |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER | Pull the information list of the group owner |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ADMIN | Pull the information list of the group admin |
| V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of common group members |

```java
// Sample code: Pull the profile of the group owner using the `filter` parameter
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

#### Pulling by page (`nextSeq`)
In many cases, it makes more sense for the user interface to display the first page of the group member list instead of the complete list. More group members can be pulled when the user clicks **Next Page** or scroll down the list to refresh. For this scenario, you can apply the method of pulling by page.

The [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API returns a maximum of 50 members at a time. You can use the pagination flag `nextSeq` to pull the group member list by page. In the first attempt to pull the group member list, enter `0` for `nextSeq`. When the first pull succeeds, the callback result [V2TIMGroupMemberInfoResult](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html) contains the [getNextSeq()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) API.
- If [getNextSeq()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) returns `0`, the complete group member list has been pulled.
- If [getNextSeq()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) returns a value greater than 0, there remains group member information to be pulled. You can then decide whether to make another call to pull group member information based on the user’s action on the UI. In the second pull, you need to pass [getNextSeq()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberInfoResult.html#a09991b5faeb8b67a0afac0c45ff4395e) in `V2TIMGroupMemberInfoResult` returned from the previous pull as a parameter to the [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API.

```java
// Sample code: Use `nextSeq` to pull the group member list by page
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

[](id:getGroupMembersInfo)
### Getting group member profiles
Call [getGroupMembersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5) to get the profiles of group members in batches. You can pass in multiple `userID` values at a time to improve network transmission efficiency.

[](id:setGroupMemberInfo)
### Modifying group member profiles
The group owner or admin can call the [setGroupMemberInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b) API to modify the group-related information of members, including group name card (`nameCard`), group member role (`role`), muting duration (`muteUntil`), and custom fields.

[](id:mute)
### Muting group members
The group owner or admin can mute a group member and set muting duration (in seconds) via [muteGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5). Muting information is stored in the [muteUtil](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberFullInfo.html#a2caecbec07bdd4fa8e6b8072bc39be58) attribute field of the group member. After the group member is muted, all group members (including the muted member) receive the [onMemberInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a4ac777faad07e32408ae7ef5e2e3fc86) event callback.
The group owner or admin can mute the entire group via the [setGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) API by setting [allMuted](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#a6faf73364372206bfee9c2b99ed5807e) to `true`. There is no time limit for group muting. The group can be unmuted through `setAllMuted(false)` in the group profile.


[](id:kick)
### Removing group members
The group owner or admin can call the [kickGroupMember](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a2e4816131f15187ccfcee8fe30e69cda) API to remove a group member. As an audio-video group (AVChatRoom) can have unlimited members, it does not support the API. You can use [muteGroupMember](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5) to achieve the same effect instead.
After the member is removed, all group members (including the kicked member) receive the [onMemberKicked](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2874b768866c2d255144c128a766c7fe) callback.

### Changing group member roles
The group owner can call [setGroupMemberRole](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8) to change the role of a member of public group (Public) or meeting group (Meeting). Roles available for changing are common member and group admin.
- After a member is set as group admin, all group members (including the new admin) receive the [onGrantAdministrator](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ae4e23c72489eafc882a40a24f36f1ae9) callback.
- After the admin role is removed for a member, all group members (including the member with admin role removed) receive the [onRevokeAdministrator](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a089480ee71485b5842c75b8c1985f72f) callback.

[](id:transfer)
### Transferring the ownership of a group
The group owner can call [transferGroupOwner](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4) to transfer the ownership of a group to other group members.
After the group ownership is transferred, all group members receive the [onGroupInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad5968cdb7ca01e2f7a702e2ca2f648fb) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.



## Community Group Topics

A community group is a large group of people brought together by common topics, and multiple topics can be created under the same community group based on different interests.
Community groups are used to manage group members. All topics under the same community group share community members, and can send and receive messages independently without interfering with each other.

>! Community group topics are supported only in 6.2.2363 and later versions.

### Community group management
#### Creating a community group

You need to perform two steps to create a community group that supports topics:

1. Create the [V2TIMGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html) object, and set `groupType` to `Community` and `isSupportTopic` to `true` in the object.
2. Call the [createGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) API to create the group.

Sample code:

```java
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupName("This is a Community");
v2TIMGroupInfo.setGroupType(V2TIMManager.GROUP_TYPE_COMMUNITY);
v2TIMGroupInfo.setSupportTopic(true);
V2TIMManager.getGroupManager().createGroup(v2TIMGroupInfo, null, new V2TIMValueCallback<String>() {
  @Override
  public void onSuccess(String groupID) {
    // Community group created successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Creation failed
  }
});
```

#### Getting the list of community groups joined

Call the [getJoinedCommunityList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#acb37b83f357fc7ee04905f8bcd5a5c67) API to get the list of community groups the current user has joined.

Sample code:

```java
V2TIMManager.getGroupManager().getJoinedCommunityList(new V2TIMValueCallback<List<V2TIMGroupInfo>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfo> v2TIMGroupInfos) {
  	// Community group list got successfully
  }
  @Override
  public void onError(int code, String desc) {
  	// Failed to get the community group list
  }
});

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
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564">joinGroup</a></td>
</tr>
<tr>
<td><a href="#quit">Leaving a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919">quitGroup</a></td>
</tr>
<tr>
<td><a href="#dismiss">Deleting a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb">dismissGroup</a></td>
</tr>
<tr>
<td><a href="#getGroupsInfo">Getting the profile of a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154">getGroupsInfo</a></td>
</tr>
<tr>
<td><a href="#setGroupsInfo">Modifying the profile of a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf">setGroupInfo</a></td>
</tr>
<tr>
<td rowspan="4">Community group member management</td>
<td><a href="#getGroupMemberList">Getting the list of community group members</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be">getGroupMemberList</a></td>
</tr>
<tr>
<td><a href="#getGroupMembersInfo">Getting the profiles of specified group members</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5">getGroupMembersInfo</a></td>
</tr>
<tr>
<td><a href="#setGroupMemberInfo">Modifying the profiles of specified group members</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b">setGroupMemberInfo</a></td>
</tr>
<tr>
<td><a href="#kick">Removing a member from a community group</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6da6755c6e0c46e96cb02575074a5333">kickGroupMember</a></td>
</tr>
</table>

### Topic management

#### Creating a topic
You need to perform two steps to create a topic:

1. Create the [V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html) object.
2. Call the [createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0) API to create the topic.

Sample code:

```java
V2TIMTopicInfo topicInfo = new V2TIMTopicInfo();
topicInfo.setTopicName(topicName);
topicInfo.setTopicFaceUrl(topicFaceUrl);
topicInfo.setIntroduction(topicIntroduction);
topicInfo.setNotification(topicNotification);
topicInfo.setCustomString(topicCustomString);

// Set `groupID` to the ID of a community group that supports topics
V2TIMManager.getGroupManager().createTopicInCommunity(groupID, topicInfo, new V2TIMValueCallback<String>() {
  @Override
  public void onSuccess(String topicID) {
  	// Topic created successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to create the topic
  }
});

```
#### Deleting a topic
Call the [deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a77c4502346e800e43c22a0f15138d699) API to delete a topic.
Sample code:

```java
V2TIMManager.getGroupManager().deleteTopicFromCommunity(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMTopicOperationResult> v2TIMTopicOperationResults) {
  	// Topic deleted successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to delete the topic
  }
});
```

#### Modifying topic information
You need to perform two steps to modify the information of a topic:

1. Create the [V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html) object and set the fields to be modified in the object.
2. Call the [setTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#acaff2edad6eb208478be9ab06d30035d) API to modify the topic information.

Sample code:

```java
V2TIMTopicInfo topicInfo = new V2TIMTopicInfo();
topicInfo.setTopicID(topicID);
topicInfo.setTopicName(topicName);
topicInfo.setTopicFaceUrl(topicFaceUrl);
topicInfo.setIntroduction(topicIntroduction);
topicInfo.setNotification(topicNotification);
topicInfo.setCustomString(topicCustomString);
topicInfo.setDraft(topicDraft);
topicInfo.setAllMute(false);
V2TIMManager.getGroupManager().setTopicInfo(topicInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Topic information modified successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to modify the topic information
  }
});

```

To modify other topic information, see [Muting members](#mute) and [Modifying the topic message receiving option](#setGroupReceiveMessageOpt).

#### Getting the topic list
Call the [getTopicInfoList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a5d2b18a76cff650cb9bb2abf2ef07306) API to get the list of topics.
- If `topicIDList` is empty, the list of all topics of the community group will be got.
- If `topicIDList` is the ID of specified topics, the list of the specified topics will be got.

Sample code:

```java
V2TIMManager.getGroupManager().getTopicInfoList(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicInfoResult>>() {
  @Override
  public void onSuccess(List<V2TIMTopicInfoResult> v2TIMTopicInfoResults) {
		// Topic list got successfully
  }

  @Override
  public void onError(int code, String desc) {
		// Failed to get the topic list
  }
});
```

#### Listing for topic callbacks
In [V2TIMGroupListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html), topic related callback methods `onTopicCreated`, `onTopicDeleted`, and `onTopicInfoChanged` are added for topic event listening. 

Sample code:

```java
V2TIMGroupListener v2TIMGroupListener = new V2TIMGroupListener() {
  @Override
  public void onTopicCreated(String groupID, String topicID) {
  	// Listening for topic creation notifications
  }

  @Override
  public void onTopicDeleted(String groupID, List<String> topicIDList) {
  	// Listening for topic deletion notifications
  }

  @Override
  public void onTopicInfoChanged(String groupID, V2TIMTopicInfo topicInfo) {
  	// Listening for topic information update notifications
  }
};
// Add an event listener for groups
V2TIMManager.getInstance().addGroupListener(v2TIMGroupListener);
```

### Topic messages

Messages can be sent and received within a topic, and messages between different topics are independent of each other.

Topic message APIs are in the core class `V2TIMMessageManager` and are described in the following table.

<table>
<tr>
<th width="15%">Feature</th>
<th width="40%">API</th>
<th width="30%">Remarks</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36359">Sending messages</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795">sendMessage</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36359">Receiving messages</a></td>
<td>`onRecvNewMessage` method in <a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html">V2TIMAdvancedMsgListener</a></td>
<td>Set `groupID` in the message to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36359">Marking messages as read</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69">markGroupMessageAsRead</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36359">Getting the message history</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597">getGroupHistoryMessageList</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/36359">Recalling messages</a></td>
<td><a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1">revokeMessage</a></td>
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

