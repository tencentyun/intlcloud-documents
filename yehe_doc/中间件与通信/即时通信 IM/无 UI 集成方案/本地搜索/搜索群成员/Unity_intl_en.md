## Feature Description
Only locally stored group members can be searched for, such as the list of group members or group member profiles that have been pulled.

> ?This feature cannot be used for audio-video groups (AVChatRoom) as the group members are not stored locally.
## Searching a Local Group
Call the `GroupSearchGroupMembers` API ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupSearchGroupMembers.html)) to search for a local group member.
You can set the search keyword `group_search_member_params_keyword_list` and specify the search scope to set whether to search by the `memberUserID`, `memberNickName`, `memberRemark`, and `memberNameCard` fields of a group member.

Depending on whether `group_search_member_params_groupid_list` of the `GroupMemberSearchParam` ([Details](https://comm.qq.com/im/doc/unity/en/types/GroupsAttributes/GroupMemberSearchParam.html)) in `GroupSearchGroupMembers` is empty (`null`), there are two cases:
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
