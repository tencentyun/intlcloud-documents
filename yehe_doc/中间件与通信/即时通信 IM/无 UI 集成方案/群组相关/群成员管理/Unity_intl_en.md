## Feature Description
Group member management includes pulling the member list, muting group members, removing group members, granting permissions, and transferring the group ownership.

[](id:GroupGetMemberInfoList)

## Getting the Group Member List

Call `GroupGetMemberInfoList` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupGetMemberInfoList.html)) to get the list of members in a specified group. This list contains the profile information of each member, such as user ID (`group_member_info_identifier`), group name card (`group_member_info_name_card`), profile photo (`group_member_info_face_url`), nickname (`group_member_info_nick_name`), and time for joining the group (`group_member_info_join_time`).

A group may have a large number of members (for example, more than 5,000). In this case, you can use the filter (`group_get_members_info_list_param_option`) and paged pull (`group_get_members_info_list_param_next_seq`) advanced features of the API for pulling the group member list.

### Filter (`filter`)
When calling the `GroupGetMemberInfoList` API ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupGetMemberInfoList.html)), you can specify to pull the list of the information of specified roles.

| Filter                                                | Type                                                       |
| ----------------------------------------------------- | ---------------------------------------------------------- |
| TIMGroupMemberRoleFlag.kTIMGroupMemberRoleFlag_All    | Pull the list of the information of all the group members  |
| TIMGroupMemberRoleFlag.kTIMGroupMemberRoleFlag_Owner  | Pull the list of the information of the group owner        |
| TIMGroupMemberRoleFlag.kTIMGroupMemberRoleFlag_Admin  | Pull the list of the information of the group admin        |
| TIMGroupMemberRoleFlag.kTIMGroupMemberRoleFlag_Member | Pull the list of the information of ordinary group members |

Sample code:



```c#
// Specify to pull the profile of the group owner through the `filter` parameter
GroupGetMemberInfoListParam param = new GroupGetMemberInfoListParam
{
  group_get_members_info_list_param_group_id = "group_id",
  group_get_members_info_list_param_option = new GroupMemberGetInfoOption
  {
    group_member_get_info_option_role_flag = TIMGroupMemberRoleFlag.kTIMGroupMemberRoleFlag_Owner
  }
};
TIMResult res = TencentIMSDK.GroupGetMemberInfoList(param, (int code, string desc, GroupGetMemberInfoListResult result, string user_data)=>{
 // Process the async logic
});
```


### Pulling by page (`nextSeq`)
In many cases, only the first page of the group member list, not the information of all the group members, needs to be displayed on the user UI. More group members need to be pulled only when the user clicks **Next Page** or pulls up the list page. In this case, you can use paged pull.

Directions for pulling by page:
1. When you call `GroupGetMemberInfoList` for the first time, set `nextSeq` to `0` (indicating to pull the group member list from the beginning). Up to 50 group member objects can be pulled at a time.

2. After the group member list is pulled successfully for the first time, the `GroupGetMemberInfoListResult` callback of `GroupGetMemberInfoList` will contain `group_get_memeber_info_list_result_next_seq` (which is the field for the next pull):
   * If `group_get_memeber_info_list_result_next_seq` is `0`, all the group members have been pulled.
   * If `group_get_memeber_info_list_result_next_seq` is greater than `0`, there are more group members that can be pulled. This doesn't mean that the next page of the member list will be pulled immediately. In common communications software, a paged pull is often triggered by a swipe operation.

3. When the user continues to pull up the group member list, if there are more members that can be pulled, you can continue to call the `GroupGetMemberInfoList` API and pass in the `nextSeq` parameter (the value is from the `GroupGetMemberInfoListResult` object returned by the last pull) for the next pull.

4. Repeat [step 3] until `nextSeq` is `0`.

Sample code:



```c#
// Specify to pull the profile of the group owner through the `filter` parameter
GroupGetMemberInfoListParam param = new GroupGetMemberInfoListParam
{
  group_get_members_info_list_param_group_id = "group_id",
  group_get_members_info_list_param_option = new GroupMemberGetInfoOption
  {
    group_member_get_info_option_role_flag = TIMGroupMemberRoleFlag.kTIMGroupMemberRoleFlag_Owner
  },
  group_get_members_info_list_param_next_seq = 0
};
TIMResult res = TencentIMSDK.GroupGetMemberInfoList(param, (int code, string desc, GroupGetMemberInfoListResult result, string user_data)=>{
 // Process the async logic
});
```


[](id:mute)
## Muting

### Muting a specified group member
The group owner or admin can call `GroupModifyMemberInfo` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyMemberInfo.html)) to mute a specified group member and set the muting period in seconds. The muting information is stored in the `group_member_info_shutup_time` attribute of the group member.

After a group member is muted, all the group members (including the muted member) will receive the `GroupTipsEventCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html)).

### Muting the entire group
The group owner or admin can also call the `GroupModifyGroupInfo` API ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyGroupInfo.html)) to mute the entire group by setting the `group_modify_info_param_is_shutup_all` attribute to `true`. The entire group can be muted for an unlimited period of time and needs to be unmuted by changing `group_modify_info_param_is_shutup_all` to `false`.

> ? Only the group owner can mute the admin.

Sample code:



```c#
// Mute the group member `userB` for ten minutes
GroupModifyMemberInfoParam param = new GroupModifyMemberInfoParam
{
  group_modify_member_info_group_id = "group_id",
  group_modify_member_info_identifier = "userB",
  group_modify_member_info_modify_flag = TIMGroupMemberModifyInfoFlag.kTIMGroupMemberModifyFlag_ShutupTime,
  group_modify_member_info_shutup_time = 600
};
TIMResult res = TencentIMSDK.GroupModifyMemberInfo(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});

// Mute all
GroupModifyInfoParam param = new GroupModifyInfoParam
{
  group_modify_info_param_group_id = "group_id",
  group_modify_info_param_modify_flag = TIMGroupModifyInfoFlag.kTIMGroupModifyInfoFlag_ShutupAll,
  group_modify_info_param_is_shutup_all = true
};
TIMResult res = TencentIMSDK.GroupModifyGroupInfo(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


[](id:kickGroupMember)
## Removing a Group Member
The group owner or admin calls the `GroupDeleteMember` API ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupDeleteMember.html)) to remove a specified ordinary group member from the group.

After the ordinary group member is removed, all the members (including the removed member) will receive the `GroupTipsEventCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html)).

As an audio-video group (AVChatRoom) can be joined freely, there is no API for removing a group member from an audio-video group (AVChatRoom). You can use `GroupModifyMemberInfo` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyMemberInfo.html)) to mute a specified member to implement similar controls.

> ? Only the group owner can remove the admin from the group.

Sample code:



```c#
GroupDeleteMemberParam param = new GroupDeleteMemberParam
{
  group_delete_member_param_group_id = "group_id",
  group_delete_member_param_identifier_array = new List<string>
  {
    "user_id"
  }
};
TIMResult res = TencentIMSDK.GroupDeleteMember(param, (int code, string desc, List<GroupDeleteMemberResult> result, string user_data)=>{
 // Process the async logic
});
```


## Setting an Admin
The group owner can call `GroupModifyMemberInfo` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyMemberInfo.html)) to set a group member in a public group (Public) or meeting group (Meeting) as the admin.

An ordinary member set as the admin has the admin permission to perform the following operations:
* Modify the basic group profile
* Remove an ordinary member from the group
* Mute an ordinary member (prevent the member from speaking during a specified period of time)
* Approve a request to join the group

For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

After an ordinary member is set/unset as the admin, all the members (including the ordinary member) will receive the `GroupTipsEventCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html)).

Sample code:


```c#
GroupModifyMemberInfoParam param = new GroupModifyMemberInfoParam
{
  group_modify_member_info_group_id = "group_id",
  group_modify_member_info_identifier = "user_id",
  group_modify_member_info_modify_flag = TIMGroupMemberModifyInfoFlag.kTIMGroupMemberModifyFlag_MemberRole,
  group_modify_member_info_member_role = TIMGroupMemberRole.kTIMMemberRole_Admin
};
TIMResult res = TencentIMSDK.GroupModifyMemberInfo(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


[](id:transfer)

## Transferring the Group Ownership
The group owner can call `GroupModifyMemberInfo` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyMemberInfo.html)) to transfer the group ownership to a group member.


Sample code:



```c#
GroupModifyMemberInfoParam param = new GroupModifyMemberInfoParam
{
  group_modify_member_info_group_id = "group_id",
  group_modify_member_info_identifier = "user_id",
  group_modify_member_info_modify_flag = TIMGroupMemberModifyInfoFlag.kTIMGroupMemberModifyFlag_MemberRole,
  group_modify_member_info_member_role = TIMGroupMemberRole.kTIMMemberRole_Owner
};
TIMResult res = TencentIMSDK.GroupModifyMemberInfo(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


## Getting the Number of Online Group Members
Call `GroupGetOnlineMemberCount` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupGetOnlineMemberCount.html)) to get the number of online group members.

> ?
> 1. Currently, only the number of online members in an audio-video group (AVChatRoom) can be obtained.
> 2. This API can be called once every 60 seconds in the SDK.

Sample code:


```c#
TIMResult res = TencentIMSDK.GroupGetOnlineMemberCount("group_id", (int code, string desc, GroupGetOnlineMemberCountResult result, string user_data)=>{
 // Process the async logic
});
```
