## Feature Description
The group profile refers to the information about the group, which can be [obtained](#getGroupInfo) and [modified](#modifyGroupInfo).

[](id:getGroupInfo)

## Getting the Group Profile
Call `GroupGetGroupInfoList` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupGetGroupInfoList_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_GetGroupInfoResult___)) to get the group profile. This API supports passing in multiple `group_id_list` values at a time to batch get group profiles.

Sample code:



```c#
// Get the group profile
TIMResult res = TencentIMSDK.GroupGetGroupInfoList(group_id_list, TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive, (int code, string desc, List<GetGroupInfoResult> result, string user_data)=>{
 // Process the async logic
});
```

[](id:modifyGroupInfo)

## Modifying the Group Profile

Call `GroupModifyGroupInfo` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupModifyGroupInfo_com_tencent_imsdk_unity_types_GroupModifyInfoParam_com_tencent_imsdk_unity_callback_NullValueCallback_)) to modify the group profile.

If you have called `SetGroupTipsEventCallback` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_SetGroupTipsEventCallback_com_tencent_imsdk_unity_callback_GroupTipsEventCallback_com_tencent_imsdk_unity_callback_GroupTipsEventStringCallback_)) to add a group event listener, after the group profile is modified, all the group members will receive the callback data.

Member roles that can modify the group profile vary by group type as follows:

| Group Type | Member Roles Allowed to Modify the **Basic Group Profile** |
| --- | --- |
| Work group (Work) | All group members |
| Public group (Public)| Group owner and admin |
| Meeting group (Meeting)| Group owner and admin |
| Community (Community)| Group owner and admin |
| Audio-video group (AVChatRoom)| Group owner |

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
Any group member can call the `MsgSetGroupReceiveMessageOpt` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgSetGroupReceiveMessageOpt_System_String_com_tencent_imsdk_unity_enums_TIMReceiveMessageOpt_com_tencent_imsdk_unity_callback_NullValueCallback_)) to change the group message receiving option.

`TIMReceiveMessageOpt` has the following options:

| Message Receiving Option | Description |
| --- | --- |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Receive | Messages will be received when the user is online, and push notifications will be received when the user is offline. |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive | No group messages will be received. |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Notify | Messages will be received when the user is online, and no push notifications will be received when the user is offline. |

Different `TIMReceiveMessageOpt` options can be used to implement group message notification muting:

**No group messages will be received.**
After the group message receiving option is set to `kTIMRecvMsgOpt_Not_Receive`, no group messages will be received, and the conversation list will not be updated.

**Group messages will be received but will not be notified to the user, and a badge without the unread count will be displayed on the conversation list UI.**
1. The group message receiving option is set to `kTIMRecvMsgOpt_Not_Notify`.
2. When the receiver receives a new group message and needs to update the conversation list, it can get the unread count through `conv_unread_num` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.types.ConvInfo.html#com_tencent_imsdk_unity_types_ConvInfo_conv_unread_num)) in `ConvInfo` of the conversation.
3. The receiver displays a badge rather than the unread count when identifying the message receiving option as `kTIMRecvMsgOpt_Not_Notify` based on the `conv_recv_opt` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.types.ConvInfo.html#com_tencent_imsdk_unity_types_ConvInfo_conv_recv_opt)) in `ConvInfo`.

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





