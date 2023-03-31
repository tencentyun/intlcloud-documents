## Feature Description

Group member management includes pulling the member list, muting group members, removing group members, granting permissions, and transferring the group ownership, which can be implemented through the methods in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.

[](id:getGroupMemberList)

## Getting the Group Member List

You can call `getGroupMemberList` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/getGroupMemberList.html)) to get the list of members in a specified group. This list contains the profile information of each member, such as user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time for joining the group (`joinTime`).

A group may have a large number of members (for example, more than 5,000). In this case, you can use the filter (`filter`) and paged pull (`nextSeq`) advanced features of the API for pulling the group member list.

### Filter (`filter`)

Call the `getGroupMemberList` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/getGroupMemberList.html)) to specify the `filter` to determine whether to pull the list of the information of specified roles.

| Filter                                                     | Type                                                       |
| ---------------------------------------------------------- | ---------------------------------------------------------- |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ALL    | Pull the list of the information of all the group members  |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_OWNER  | Pull the list of the information of the group owner        |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN  | Pull the list of the information of the group admin        |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the list of the information of ordinary group members |

Below is the sample code:

```javascript
// Specify to pull the profile of the group owner through the `filter` parameter
const groupID = "groupID";
const count = 10;
const filter = GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN;
const offset = 0;
const nextSeq = "0";
groupManager.getGroupMemberList(groupID, filter, nextSeq, count, offset);
```

### Paged pull (`nextSeq`)

In many cases, only the first page of the group member list, not the information of all the group members, needs to be displayed on the user UI. More group members need to be pulled only when the user clicks **Next Page** or pulls up the list page. In this case, you can use paged pull.

Directions for paged pull:

1. When you call `getGroupMemberList` for the first time, set `nextSeq` to `0` (indicating to pull the group member list from the beginning). Up to 50 group member objects can be pulled at a time.
2. After the group member list is pulled successfully for the first time, the `V2TIMGroupMemberInfoResult` callback of `getGroupMemberList` will contain `nextSeq` (field for the next pull):

   - If `nextSeq` is `0`, all the group members have been pulled.
   - If `nextSeq` is greater than `0`, there are more group members that can be pulled. This does not mean that the next page of the member list will be pulled immediately. In common communications software, a paged pull is often triggered by a swipe operation.

3. When the user continues to pull up the group member list, if there are more members that can be pulled, you can continue to call the `getGroupMemberList` API and pass in the `nextSeq` parameter (the value is from the `V2TIMGroupMemberInfoResult` object returned by the last pull) for the next pull.

4. Repeat [step 3] until `nextSeq` is `0`.

Below is the sample code:

```javascript
// Specify to pull the profile of the group owner through the `filter` parameter
const groupID = "groupID";
const count = 10;
const filter = GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN;
const offset = 0;
const nextSeq = "0";
groupManager.getGroupMemberList(groupID, filter, nextSeq, count, offset);
```

[](id:mute)

## Muting

### Muting a specified group member

The group owner or admin can call `muteGroupMember` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/muteGroupMember.html)) to mute a specified group member and set the muting period in seconds. The muting information is stored in the `muteUtil` attribute of the group member.

After a group member is muted, all the group members (including the muted member) will receive the `onMemberInfoChanged` callback ([Details](https://comm.qq.com/im/doc/RN/en/Callback/OnMemberInfoChanged.html)).

### Muting the entire group

The group owner or admin can also call the `setGroupInfo` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/setGroupInfo.html)) to mute the entire group by setting the `allMuted` attribute to `true`. The entire group can be muted for an unlimited period of time and needs to be unmuted through `setAllMuted(false)` of the group profile.

> ? Muting all the group members will trigger the `onGroupInfoChanged` callback ([Details](https://comm.qq.com/im/doc/RN/en/Callback/OnGroupInfoChanged.html)). This feature is disabled by default and can be enabled in the console.
> Directions: Go to the [**Group configuration**](https://console.cloud.tencent.com/im/qun-setting) module in the IM console, select **Group system notification configuration**, click **Edit** in the **Operation** column, and modify **Notification of muting all change**.
> Only the group owner can mute the admin.

Below is the sample code:

```javascript
// Mute the `userB` group member for 10 seconds
const groupID = "groupID";
const userID = "userID";
const seconds = 10;
groupManager.muteGroupMember(groupID, userID, seconds);

// Mute all the members
groupManager.setGroupInfo({
  isAllMuted: true,
  groupID: "",
  groupType: "Public",
});

TencentImSDKPlugin.v2TIMManager.addGroupListener({
  onMemberInfoChanged: (groupID, v2TIMGroupMemberChangeInfoList) => {
    // The group member information is changed.
  },
  onGroupInfoChanged: (groupID, info) => {
    // The group information is changed.
  },
});
```

[](id:kickGroupMember)

## Removing a Group Member

The group owner or admin can call the `kickGroupMember` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/kickGroupMember.html)) to remove a specified ordinary group member from the group.

After the ordinary group member is removed, all the members (including the removed member) will receive the `onMemberKicked` callback ([Details](https://comm.qq.com/im/doc/RN/en/Callback/OnMemberKicked.html)).

As there are no limits on joining an audio-video group (AVChatRoom), there is no API for removing a group member from an audio-video group (AVChatRoom). You can use `muteGroupMember` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/muteGroupMember.html)) to mute a specified member to implement similar controls. For detailed directions, see [muteGroupMember](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/muteGroupMember.html).

> ? Only the group member can remove the admin from the group.

Below is the sample code:

```javascript
groupManager.kickGroupMember("groupID", []);
```

## Setting as Admin

The group owner can call `setGroupMemberRole` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/setGroupMemberRole.html)) to set a group member in a public group (Public) or meeting group (Meeting) as the admin.

An ordinary member set as the admin has the admin permission to perform the following operations:

- Modify the basic group profile.
- Remove an ordinary member from the group.
- Mute an ordinary member (prevent the member from speaking during a specified period of time).
- Approve a request to join the group.

For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

After an ordinary member is set as the admin, all the members (including the ordinary member) will receive the `onGrantAdministrator` callback ([Details](https://comm.qq.com/im/doc/RN/en/Callback/OnGrantAdministrator.html)).

After the ordinary member is unset as the admin, all the members (including the ordinary member) will receive the `onRevokeAdministrator` callback ([Details](https://comm.qq.com/im/doc/RN/en/Callback/OnRevokeAdministrator.html)).

Below is the sample code:

```javascript
groupManager.setGroupMemberRole(
  "groupID",
  "userID",
  GroupMemberRoleTypeEnum.V2TIM_GROUP_MEMBER_ROLE_ADMIN
);

// Listen for the role change
TencentImSDKPlugin.v2TIMManager.addGroupListener({
  onMemberInfoChanged: (groupID, v2TIMGroupMemberChangeInfoList) => {},
  onGroupInfoChanged: (groupID, info) => {},
  onGrantAdministrator: (groupID, info, infolist) => {},
  onRevokeAdministrator: (groupID, info, infolist) => {},
});
```

[](id:transfer)

## Transferring the Group Ownership

The group owner can call [transferGroupOwner](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/transferGroupOwner.html) to transfer the group ownership to a group member.

After the group ownership is transferred, all group members receive the [onGroupInfoChanged](https://comm.qq.com/im/doc/RN/en/Callback/OnGroupInfoChanged.html) callback, where the type of `V2TIMGroupChangeInfo` is `V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER` and the value is the UserID of the new group owner.

Below is the sample code:

```javascript
groupManager.transferGroupOwner("groupID", "userID");
```

## Getting the Number of Online Group Members

Call `getGroupOnlineMemberCount` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/getGroupOnlineMemberCount.html)) to get the number of online group members.

> ?
>
> 1. Currently, only the number of online members in an audio-video group (AVChatRoom) can be obtained.
> 2. The SDK can be called once every 60 seconds.

Below is the sample code:

```javascript
groupManager.getGroupOnlineMemberCount("groupID");
```
