The Unity SDK supports local search but you need to upgrade to the Flagship Edition package by referring to [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/36021).

The search API interface consists of three parts: the upper part is for friend search, the middle part is for group and group member search, and the lower part is for message search, where messages are classified by conversation.

## SDK Integration Guide

### Searching for friends

You can use the `FriendshipSearchFriends` API to search for friends by user ID, nickname, and remarks. The following is a call example of the API:

```c#
FriendSearchParam searchparam  = new FriendSearchParam();
searchparam.friendship_search_param_keyword_list = ["Jack"];
searchparam.friendship_search_param_search_field_list = [TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_Identifier,TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_NikeName,TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_Remark]
TencentIMSDK.FriendshipSearchFriends(searchparam,(int code, string desc, string json_param, string user_data)=>{
  // Search result
});
```



### Searching for local messages

You can use `MsgSearchLocalMessages` to search for local messages. For parameter details, see [MessageSearchParam](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.types.MessageSearchParam.html).

- Use `msg_search_param_message_type_array` to specify the message type to search.
- Use `msg_search_param_conv_id` to specify the conversation for message search.
- Use `msg_search_param_search_time_position` to specify the start time for message search.

```c#
MessageSearchParam searchparam  = new MessageSearchParam();
searchparam.msg_search_param_keyword_array = ["Jack"]; // Keyword
searchparam.msg_search_param_message_type_array = [TIMElemType.kTIMElem_Text]; // Search for text messages only
searchparam.msg_search_param_conv_id = ""; // Search for messages in a specified conversation
// ...
TencentIMSDK.FriendshipSearchFriends(searchparam,(int code, string desc, string json_param, string user_data)=>{
  // Search result
});
```



### Searching for group profiles

You can call [GroupSearchGroups](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupSearchGroups_com_tencent_imsdk_unity_types_GroupSearchParam_com_tencent_imsdk_unity_callback_ValueCallback_) to search for group profiles. For parameter details, see [GroupSearchParam](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.types.GroupSearchParam.html).

```c#
GroupSearchParam searchparam  = new GroupSearchParam();
searchparam.group_search_params_keyword_list = ["Jack"];
searchparam.group_search_params_field_list = [TIMGroupSearchFieldKey.kTIMGroupSearchFieldKey_GroupId,TIMGroupSearchFieldKey.kTIMGroupSearchFieldKey_GroupName];// Specify the search region
TencentIMSDK.GroupSearchGroups(searchparam,(int code, string desc, string json_param, string user_data)=>{
  // Search result
});
```


### Searching for group members

You can call [GroupSearchGroupMembers](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupSearchGroupMembers_com_tencent_imsdk_unity_types_GroupMemberSearchParam_com_tencent_imsdk_unity_callback_ValueCallback_) to search for group members. For parameter details, see [GroupMemberSearchParam](https://comm.qq.com/im/doc/unity/en/types/GroupsAttributes/GroupMemberSearchParam.html).

```c#
GroupSearchParam searchparam  = new GroupMemberSearchParam();
searchparam.group_search_member_params_keyword_list = ["Jack"];
searchparam.group_search_member_params_groupid_list = ['id','id2'];// Specify a group
searchparam.group_search_member_params_field_list = [] // Search region `TIMGroupMemberSearchFieldKey`
TencentIMSDK.GroupSearchGroups(searchparam,(int code, string desc, string json_param, string user_data)=>{
  // Search result
});
```

