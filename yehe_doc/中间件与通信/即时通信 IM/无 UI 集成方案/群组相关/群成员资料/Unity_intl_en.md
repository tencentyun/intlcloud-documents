## Feature Description
The methods to manipulate the group member profile are in the `GroupGetMemberInfoList` and `GroupModifyMemberInfo` core classes.

[](id:getGroupMembersInfo)

## Getting the Profile of a Group Member

Call `GroupGetMemberInfoList` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupGetMemberInfoList.html)) to get the group member profile. This API supports passing in multiple `group_get_members_info_list_param_identifier_array` values at a time to batch get group member profiles and therefore improve the network transfer efficiency.

Sample code:



```c#
// Get the group member profile
GroupGetMemberInfoListParam param = new GroupGetMemberInfoListParam
{
  group_get_members_info_list_param_group_id = "group_id",
  group_get_members_info_list_param_identifier_array = new List<string>
  {
    "user_id"
  }
};
TIMResult res = TencentIMSDK.GroupGetMemberInfoList(param, (int code, string desc, GroupGetMemberInfoListResult result, string user_data)=>{
 // Process the async logic
});
```

[](id:setGroupMemberInfo)

## Modifying the Profile of a Group Member

The group owner or admin can call the `GroupModifyMemberInfo` API ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupModifyMemberInfo.html)) to modify the group name card (`group_modify_member_info_name_card`), custom field (`group_modify_member_info_custom_info`), and other information of a group member.

Sample code:



```java
// Set the group member profile
GroupModifyMemberInfoParam param = new GroupModifyMemberInfoParam
{
  group_modify_member_info_group_id = "group_id",
  group_modify_member_info_identifier = "userB",
  group_modify_member_info_modify_flag = TIMGroupMemberModifyInfoFlag.kTIMGroupMemberModifyFlag_NameCard,
  group_modify_member_info_name_card = "new name card"
};
TIMResult res = TencentIMSDK.GroupModifyMemberInfo(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```
