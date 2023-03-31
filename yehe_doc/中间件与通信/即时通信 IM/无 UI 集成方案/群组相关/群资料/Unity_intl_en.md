## Feature Description
The group profile refers to the information about the group, which can be [obtained](#getGroupInfo) and [modified](#modifyGroupInfo).

[](id:getGroupInfo)

## Getting the Group Profile
Call `GroupGetGroupInfoList` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupGetGroupInfoList.html)) to get the group profile. This API supports passing in multiple `group_id_list` values at a time to batch get group profiles.

Sample code:



```c#
// Get the group profile
TIMResult res = TencentIMSDK.GroupGetGroupInfoList(group_id_list, TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive, (int code, string desc, List<GetGroupInfoResult> result, string user_data)=>{
 // Process the async logic
});
```

[](id:modifyGroupInfo)

## Modifying the Group Profile

Call `GroupModifyGroupInfo` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyGroupInfo.html)) to modify the group profile.

If you have called `SetGroupTipsEventCallback` ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetGroupTipsEventCallback.html)) to add a group event listener, after the group profile is modified, all the group members will receive the callback data.

Member roles that can modify the group profile vary by group type as follows:

| Group Type                     | Member Roles Allowed to Modify the **Basic Group Profile** |
| ------------------------------ | ---------------------------------------------------------- |
| Work group (Work)              | All group members                                          |
| Public group (Public)          | Group owner and admin                                      |
| Meeting group (Meeting)        | Group owner and admin                                      |
| Community (Community)          | Group owner and admin                                      |
| Audio-video group (AVChatRoom) | Group owner                                                |

Sample code:


```c#
GroupModifyInfoParam param = new GroupModifyInfoParam
{
  group_modify_info_param_group_id = "group_id",
  group_modify_info_param_modify_flag = TIMGroupModifyInfoFlag.kTIMGroupModifyInfoFlag_Name, // Rename a group
  group_modify_info_param_group_name = "new group name"
};
TIMResult res = TencentIMSDK.GroupModifyGroupInfo(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```



## Setting the Group Message Receiving Option
Any group member can call the `MsgSetGroupReceiveMessageOpt` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSetGroupReceiveMessageOpt.html)) to change the group message receiving option.

`TIMReceiveMessageOpt` has the following options:

| Message Receiving Option                        | Description                                                  |
| ----------------------------------------------- | ------------------------------------------------------------ |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Receive     | Messages will be received when the user is online, and push notifications will be received when the user is offline. |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive | No group messages will be received.                          |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Notify  | Messages will be received when the user is online, and no push notifications will be received when the user is offline. |

Different `TIMReceiveMessageOpt` options can be used to implement group message notification muting:

**No group messages will be received.**
After the group message receiving option is set to `kTIMRecvMsgOpt_Not_Receive`, no group messages will be received, and the conversation list will not be updated.

**Group messages will be received but will not be notified to the user, and a badge without the unread count will be displayed on the conversation list UI.**
1. The group message receiving option is set to `kTIMRecvMsgOpt_Not_Notify`.
2. When the receiver receives a new group message and needs to update the conversation list, it can get the unread count through `conv_unread_num` ([Details](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html#convunreadnum)) in `ConvInfo` of the conversation.
3. The receiver displays a badge rather than the unread count when identifying the message receiving option as `kTIMRecvMsgOpt_Not_Notify` based on the `conv_recv_opt` ([Details](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html#convrecvopt)) in `ConvInfo`.

> ? As this method requires the unread count feature, it applies only to work groups (Work) and public groups (Public).

Sample code:



```c#
// Set the group message receiving option
GroupModifyInfoParam param = new GroupModifyInfoParam
{
  group_modify_info_param_group_id = "group_id",
  group_modify_info_param_modify_flag = TIMGroupModifyInfoFlag.kTIMGroupModifyInfoFlag_AddOption, // Change the group join option
  group_modify_info_param_add_option = TIMGroupAddOption.kTIMGroupAddOpt_Auth
};
TIMResult res = TencentIMSDK.GroupModifyGroupInfo(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```
