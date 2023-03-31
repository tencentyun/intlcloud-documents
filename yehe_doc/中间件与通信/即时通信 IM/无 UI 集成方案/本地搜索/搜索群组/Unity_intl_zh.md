## 功能描述
群组搜索只能搜索本地存储过的群组，比如已加入的群组列表，拉取过的群组资料等。


## 搜索本地群组
您可以调用接口 `GroupSearchGroups` ([Details](https://comm.qq.com/im/doc/unity/en/api/GroupApi/GroupSearchGroups.html)) 搜索本地群组。
您可以设置搜索关键字 `group_search_params_keyword_list`，并指定搜索的范围，即是否搜索群组的 `userID`、`groupName` 字段。

示例代码如下：



```c#
// 通过关键搜索群组
GroupSearchParam param = new GroupSearchParam
{
  group_search_params_keyword_list = new List<string>
  {
    "关键词1"
  },
  group_search_params_field_list = new List<TIMGroupSearchFieldKey>
  {
    TIMGroupSearchFieldKey.kTIMGroupSearchFieldKey_GroupId,
    TIMGroupSearchFieldKey.kTIMGroupSearchFieldKey_GroupName,
  }
};
TIMResult res = TencentIMSDK.GroupSearchGroups(param, (int code, string desc, List<GroupDetailInfo> result, string user_data)=>{
 // 处理异步逻辑
});
```
