## Feature Description
Only locally stored group members can be searched for, such as the list of group members or group member profiles that have been pulled.

> ?This feature cannot be used for audio-video groups (AVChatRoom) as the group members are not stored locally.
## Searching a Local Group
Call the `GroupSearchGroupMembers` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_GroupSearchGroupMembers_com_tencent_imsdk_unity_types_GroupMemberSearchParam_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_GroupGetOnlineMemberCountResult___)) to search for a local group member.
You can set the search keyword `group_search_member_params_keyword_list` and specify the search scope to set whether to search by the `memberUserID`, `memberNickName`, `memberRemark`, and `memberNameCard` fields of a group member.

Depending on whether `group_search_member_params_groupid_list` of the `GroupMemberSearchParam` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.types.GroupMemberSearchParam.html)) in `GroupSearchGroupMembers` is empty (`null`), there are two cases:
- If `group_search_member_params_groupid_list` is left empty, members in all the groups will be searched for and returned by `groupID`.
- If `group_search_member_params_groupid_list` is not left empty, members in the specified group will be searched for.

Sample code:



```c#
// Search for group members by the keyword and group ID
GroupMemberSearchParam param = new GroupMemberSearchParam
{
  group_search_member_params_groupid_list = new List<string>
  {
    "group_id"
  },
  group_search_member_params_keyword_list = new List<string>
  {
    "Keyword 1"
  },
  group_search_member_params_field_list = new List<TIMGroupMemberSearchFieldKey>
  {
    TIMGroupMemberSearchFieldKey.kTIMGroupMemberSearchFieldKey_Identifier,
    TIMGroupMemberSearchFieldKey.kTIMGroupMemberSearchFieldKey_NikeName,
    TIMGroupMemberSearchFieldKey.kTIMGroupMemberSearchFieldKey_Remark,
    TIMGroupMemberSearchFieldKey.kTIMGroupMemberSearchFieldKey_NameCard,
  }
};
TIMResult res = TencentIMSDK.GroupSearchGroupMembers(param, (int code, string desc, List<GroupGetOnlineMemberCountResult> result, string user_data)=>{
 // Process the async logic
});
```




