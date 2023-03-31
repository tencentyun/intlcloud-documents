## 功能描述
在某些场景下，您可能需要对好友进行分组，例如分为 "大学同学"、"公司同事" 等，您可以调用以下接口实现。

## 好友分组

### 新建好友分组
您可以调用 `createFriendGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMFriendshipManager/createFriendGroup.html)) 接口新建好友分组。

示例代码如下：


```dart
// 创建好友分组，并添加好友进分组
V2TimValueCallback<List<V2TimFriendOperationResult>> friendgroups = await friendshipManager.createFriendGroup(groupName: "分组1",userIDList: ['user1']);
```


### 删除好友分组
您可以调用 `deleteFriendGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMFriendshipManager/deleteFriendGroup.html)) 接口删除好友分组。

示例代码如下：


```dart
// 删除好友分组
V2TimCallback deleteFriendsgroup = await friendshipManager.deleteFriendGroup(groupNameList: ['分组1']);
```


### 重命名好友分组
您可以调用 `renameFriendGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMFriendshipManager/renameFriendGroup.html)) 接口重命名好友分组。

示例代码如下：


```dart
// 修改好友分组名字
V2TimCallback rename = await friendshipManager.renameFriendGroup(newName: "新分组1",oldName: '分组1');
```


### 获取好友分组
您可以调用 `getFriendGroups` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMFriendshipManager/getFriendGroups.html)) 接口获取好友分组列表。

示例代码如下：


```dart
// 按分组名字获取好友分组信息
V2TimValueCallback<List<V2TimFriendGroup>> friendGrous = await friendshipManager.getFriendGroups(groupNameList: ['分组1']);
```


### 添加好友到一个分组
您可以调用 `addFriendsToFriendGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMFriendshipManager/addFriendsToFriendGroup.html)) 接口添加好友到一个分组。

示例代码如下：


```dart
// 将用户添加到分组中
V2TimValueCallback<List<V2TimFriendOperationResult>> addToFrindgroups = await friendshipManager.addFriendsToFriendGroup(groupName: "分组1",userIDList: ['user1']);
```


### 从分组中删除某好友
您可以调用 `deleteFriendsFromFriendGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html)) 从分组中删除某好友。

示例代码如下：


```dart
// 将要有从分组中删除
V2TimValueCallback<List<V2TimFriendOperationResult>> deletefromFriendsGrousps = await friendshipManager.deleteFriendsFromFriendGroup(groupName: "分组1", userIDList: ['user1']);
```
