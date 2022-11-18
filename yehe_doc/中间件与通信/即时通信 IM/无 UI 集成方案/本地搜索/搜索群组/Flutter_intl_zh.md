## 功能描述
群组搜索只能搜索本地存储过的群组，例如已加入的群组列表，拉取过的群组资料等。

> ? flutter sdk 3.8.0支持

## 搜索本地群组
您可以调用接口 `searchGroups` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/searchGroups.html)) 搜索本地群组。
您可以设置搜索关键字 `keywordList`，并指定搜索的范围，即是否搜索群组的 `userID`、`groupName` 字段。

示例代码如下：



```dart
// 通过关键搜索群组
V2TimValueCallback<List<V2TimGroupInfo>> searchGroup  = await groupManager.searchGroups(searchParam: V2TimGroupSearchParam(keywordList: ['关键词'],isSearchGroupID: true,isSearchGroupName: true));
```





