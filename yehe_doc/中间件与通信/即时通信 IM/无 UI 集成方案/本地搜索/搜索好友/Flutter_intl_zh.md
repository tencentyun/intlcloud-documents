## 功能描述
用户搜索只能搜索本地存储过的用户，例如拉取过的好友列表，拉取过的用户资料等。

> flutter sdk 3.8.0支持

## 搜索本地用户资料
调用接口 `searchFriends` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMFriendshipManager/searchFriends.html)) 可以搜索本地用户资料。
您可以设置搜索关键字 `keywordList`，并指定搜索的范围，即是否搜索用户的 `userID`、`nickName`、`remark` 字段。

示例代码如下：



```dart
// 通过关键词搜索好友
V2TimValueCallback<List<V2TimFriendInfoResult>> serchFriend= await friendshipManager.searchFriends(searchParam: V2TimFriendSearchParam(isSearchNickName: true,isSearchRemark: true,isSearchUserID: true,keywordList: ['关键词']));
```

