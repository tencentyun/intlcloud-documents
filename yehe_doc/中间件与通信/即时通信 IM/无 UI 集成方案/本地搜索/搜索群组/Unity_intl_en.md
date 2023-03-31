## Feature Description
Only locally stored groups can be searched for, such as the list of joined groups and group profiles that have been pulled.


## Searching a Local Group
Call the `GroupSearchGroups` API ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupSearchGroups.html)) to search a local group.
You can set the search keyword `group_search_params_keyword_list` and specify the search scope to set whether to search by the `userID` and `groupName` fields of a group.

Sample code:



```c#
// Search for a group by the keyword
GroupSearchParam param = new GroupSearchParam
{
  group_search_params_keyword_list = new List<string>
  {
    "Keyword 1"
  },
  group_search_params_field_list = new List<TIMGroupSearchFieldKey>
  {
    TIMGroupSearchFieldKey.kTIMGroupSearchFieldKey_GroupId,
    TIMGroupSearchFieldKey.kTIMGroupSearchFieldKey_GroupName,
  }
};
TIMResult res = TencentIMSDK.GroupSearchGroups(param, (int code, string desc, List<GroupDetailInfo> result, string user_data)=>{
 // Process the async logic
});
```
