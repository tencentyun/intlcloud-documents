## Feature Description
The group management feature allows creating a group, joining a group, getting the joined groups, leaving a group, or disbanding a group.

[](id:listener)

## Group Event Listener
In the group management feature as described below, the IM SDK will automatically trigger the group event notification callback, for example, when someone joins or leaves a group.

Call `SetGroupTipsEventCallback` ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetGroupTipsEventCallback.html)) to add a group event listener.

To stop receiving group events, call `SetGroupTipsEventCallback` again ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetGroupTipsEventCallback.html)) and pass in `null` to remove the group event listener.

> ! You need to set the group event listener in advance to receive group event notifications.

Sample code:


```c#
TencentIMSDK.SetGroupTipsEventCallback((GroupTipsElem message, string user_data)=>{
 // Process the callback logic
});
```


## Creating a Group
To initialize the group information such as group introduction, group profile photo, and existing group members when creating a group, call the `GroupCreate` advanced API ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupCreate.html)), and the `create_group_result_groupid` will be returned in the callback for successful creation.

Sample code:



```c#
// Create a public group and specify group attributes
CreateGroupParam param = new CreateGroupParam
{
  create_group_param_group_id = "group_id",
  create_group_param_group_name = "group_name",
  create_group_param_group_type = TIMGroupType.kTIMGroup_Public,
  create_group_param_add_option = TIMGroupAddOption.kTIMGroupAddOpt_Any,
};

TIMResult res = TencentIMSDK.GroupCreate(param, (int code, string desc, CreateGroupResult result, string user_data)=>{
 // Process the async logic
});
```

[](id:joinGroup)

## Joining a Group
The method for joining a group may vary by group type as follows:

| Type                           | Method for Joining a Group                                   |
| ------------------------------ | ------------------------------------------------------------ |
| Work group (Work)              | By invitation                                                |
| Public group (Public)          | On request from the user and on approval from the group owner or admin |
| Meeting group (Meeting)        | Free to join                                                 |
| Community (Community)          | Free to join                                                 |
| Audio-video group (AVChatRoom) | Free to join                                                 |

The following describes how to join the groups in an easy-to-hard sequence.

> ! You need to call `SetGroupTipsEventCallback` to add a group event listener in advance to receive the following group events.

#### Free to join a group
Meeting groups (Meeting), audio-video groups (AVChatRoom), and communities are mainly used for free interaction scenarios, such as online meeting and live show. The process of joining such groups is the simplest:
1. The user calls `GroupJoin` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupJoin.html)) to join the group.
2. After the user has successfully joined the group, all the group members (including the user) will receive the `GroupTipsEventCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html)).

Sample code:


```c#
// Listen for the group join event
TencentIMSDK.SetGroupTipsEventCallback((GroupTipsElem message, string user_data)=>{
 // Process the callback logic
});


// Join a group
TIMResult res = TencentIMSDK.GroupJoin(group_id, "greeting message", (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


#### Joining a group by invitation
Resembling WeChat and WeCom groups, work groups (Work) are suitable for communication in work environments. The interaction pattern is designed to disable proactive group joining and only allow users to be invited to join the group by group members.
The steps to join a group are as follows:
1. A group member calls `GroupInviteMember` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupInviteMember.html)) to invite a user to the group.
2. All the group members (including the user) will receive the `GroupTipsEventCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/callback/GroupTipsEventCallback.html)).

Sample code:


```c#
// Listen for the group invitation event
TencentIMSDK.SetGroupTipsEventCallback((GroupTipsElem message, string user_data)=>{
 // Process the callback logic
});


// Invite the `userA` user to join the `groupA` group
GroupInviteMemberParam param = new GroupInviteMemberParam
{
  group_invite_member_param_group_id = "group_id",
  group_invite_member_param_identifier_array = new List<string> {
    "1234"
  } // Array of IDs of the users invited to the group
};
TIMResult res = TencentIMSDK.GroupInviteMember(param, (int code, string desc, List<GroupInviteMemberResult> result, string user_data)=>{
 // Process the async logic
});
```


#### Joining a group on request and on approval
A public group (Public) is similar to the interest group and clan group of QQ. Anyone can join it on request and on approval from the group owner or admin.


Description of process:
1. Set the callback for a group system message `SetGroupTipsEventCallback` ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetGroupTipsEventCallback.html)).

2. The user calls `GroupJoin` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupJoin.html)) to request to join the group.

3. The group owner or admin traverses the group join request list and calls `GroupHandlePendency` ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupHandlePendency_com_tencent_imsdk_unity_types_GroupHandlePendencyParam_com_tencent_imsdk_unity_callback_NullValueCallback_)) to approve/reject the request.

4. On approval, all the group members (including the user) will receive the `SetGroupTipsEventCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetGroupTipsEventCallback.html)), notifying the group members that someone joined the group.



The group owner or admin can also call the `GroupModifyGroupInfo` API ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyGroupInfo.html)) to change the group join option (`group_modify_info_param_add_option`) to "no group join allowed" or "no approval required".

`group_modify_info_param_add_option` has the following options:

| Group Join Option                        | Description                                                  |
| ---------------------------------------- | ------------------------------------------------------------ |
| TIMGroupAddOption.kTIMGroupAddOpt_Forbid | No users can join the group.                                 |
| TIMGroupAddOption.kTIMGroupAddOpt_Auth   | Approval from the group owner or admin is required to join the group (default value). |
| TIMGroupAddOption.kTIMGroupAddOpt_Any    | Any user can join the group without approval.                |


## Getting the Joined Groups
Call `GroupGetJoinedGroupList` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupGetJoinedGroupList.html)) to get the list of joined work groups (Work), public groups (Public), meeting groups (Meeting), and communities (Community, which **don't support** the topic feature). Audio-video groups (AVChatRoom) and communities (Community, which **support** the topic feature) are not included in this list.

Sample code:



```c#
// Get the joined groups
TIMResult res = TencentIMSDK.GroupGetJoinedGroupList((int code, string desc, List<GroupBaseInfo> info_list, string user_data)=>{
 // Process the async logic
});
```

[](id:quitGroup)

## Leaving a Group

Call `GroupQuit` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupQuit.html)) to leave a group.
Other group members will receive the `SetGroupTipsEventCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetGroupTipsEventCallback.html)).

> ! The group owner **cannot** leave a public group (Public), meeting group (Meeting), community, or audio-video group (AVChatRoom) and can only disband it.

Sample code:



```c#
// Leave a group
TIMResult res = TencentIMSDK.GroupQuit(group_id, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


[](id:deleteGroup)

## Disbanding a Group

Call `GroupDelete` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupDelete.html)) to disband a group, and all the group members will receive the `SetGroupTipsEventCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetGroupTipsEventCallback.html)).

Sample code:



```c#
// Disband a group
TIMResult res = TencentIMSDK.GroupDelete(group_id, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```
