## 用户资料管理
### 查询和修改自己的资料
**查询自己的资料**接口为 [getUsersInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a0071a5be9f333698f05fd80aff203560)，其中参数 `userIDList` 需填入自己的 UserID。
**修改自己的资料**接口为 [setSelfInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2ff0139742c4a0bf6dce1ef7423f3bee)。修改自己的资料成功后，会收到 [onSelfInfoUpdated](http://doc.qcloudtrtc.com/im/protocolV2TIMSDKListener-p.html#ab3e8543e99934530763daa7eeffbab89) 回调。

### 查询非好友用户资料
查询非好友资料接口同查询自己的资料 [getUsersInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a0071a5be9f333698f05fd80aff203560)，参数 `userIDList` 填入非好友的 UserID 即可。

### 查询和修改好友资料
**查询指定的好友资料**接口为 [getFriendsInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a930bb2a8cd664a4037797970ce9fc0d8)，从回调信息中通过 `V2TIMFriendGetResult` 的 `relation` 字段可以得到该用户与自己的关系：
- `V2TIM_FRIEND_RELATION_TYPE_NONE` 表示不是好友。
- `V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY` 表示互为好友。
- `V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST` 表示对方在我的好友列表中。

**修改指定的好友信息**接口为 [setFriendInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a97409aaccf135d60344f002aca06e63e) ，可修改好友备注等资料。

## 屏蔽某人消息
- **拉黑某人**
如需屏蔽某人的消息，请调用 [addToBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ad1de7b4712309ce4164e4db6574486f0) 接口把该用户加入黑名单，即拉黑该用户。
被拉黑的用户默认不会感知到“被拉黑”的状态，消息发送后不会返回已被对方拉黑的错误码。如果希望被拉黑的用户在发消息时返回已被对方拉黑的错误提醒，可以参考 [被拉黑的用户发消息怎么给错误提示](#sos)。

- **解除拉黑**
从黑名单中移除对方后可再次接收对方的消息，可调用 [deleteFromBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#afe61664e0afee949f99ec63a288316e2)。

- **获取黑名单列表**
您可以通过 [getBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aa0e6338aefd556a23507c2798af6e717) 查看已拉黑多少用户，并对黑名单人员进行管理。

## 好友管理

### 是否需要加好友
IM SDK 在发送单聊消息的时候，默认不检查好友关系。在客服场景中，如果用户需要先加客服为好友才能进行沟通非常不方便，因此该默认设置常用于在线客服等场景。
如需实现类似“微信”或者“QQ”中“先加好友，再发消息”的交互体验，您可以在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【好友关系检查】中开启"发送单聊消息检查关系链"。开启后，用户只能给好友发送消息，当用户给非好友发消息时，SDK 会报20009错误码。


### 好友列表管理

IM SDK 支持好友关系链逻辑，您可以调用 [getFriendList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a8d03aec2e3efd16b7942944c6cb30d0e) 接口获取好友列表，调用 [deleteFromFriendList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2786c60824ea6ec117429ef2b59630a1) 接口删除好友关系，也可以调用 [addFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) 接口添加好友。

根据对方用户资料中的加好友需要验证与否，可以分为两种处理流程：

#### 第一种：加好友不需要对方验证
 1. 用户 A 和 B 调用 [setFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443) 设置关系链监听。
 2. 用户 B 通过 [setSelfInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2ff0139742c4a0bf6dce1ef7423f3bee) 函数里的 [allowType](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMUserFullInfo.html#a39e2e474ee15e2a642a430baae72a787) 字段设置为加好友不需要验证 `V2TIM_FRIEND_ALLOW_ANY`。
 3. 用户 A 调用  [addFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) 申请添加 B 为好友即可添加成功。
- 如果申请参数 `V2TIMFriendAddApplication` 中 [addType](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFriendAddApplication.html#a0b48b53a403cf4bf6aced22ee5557257) 设置为双向好友即 `V2TIM_FRIEND_TYPE_BOTH`，则用户 A 和 B 都会收到 [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) 回调；
- 如果设置为单向好友即 `V2TIM_FRIEND_TYPE_SINGLE`，则只有用户 A 收到 [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) 回调。

#### 第二种：加好友需要通过对方验证
1. 用户 A 和 B 调用 [setFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443) 设置关系链监听。
2. 用户 B 通过 [setSelfInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2ff0139742c4a0bf6dce1ef7423f3bee) 函数里的 [allowType](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMUserFullInfo.html#a39e2e474ee15e2a642a430baae72a787) 字段设置为加好友需要验证 `V2TIM_FRIEND_NEED_CONFIRM`。 
3. 用户 A 调用  [addFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) 申请添加 B 为好友，接口的成功回调参数中 `V2TIMFriendOperationResult` 中的 `resultCode` 返回30539，表示需要等待用户 B 的验证，同时 A 和 B 都会收到 [onFriendApplicationListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a54c7c648088b88ebf0f235d363670566) 的回调。
4. 用户 B 会收到 [onFriendApplicationListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a54c7c648088b88ebf0f235d363670566) 的回调，当参数 `V2TIMFriendApplication` 中的 [type](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFriendApplication.html#a9e52fd30b3c8d77f7f6f50034f6ce2b7) 为 `V2TIM_FRIEND_APPLICATION_COME_IN` 时，可以选择接受或者拒绝：
    - 调用 [acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2546222b4994a5be9f67dfa8eb504e6b) 接受好友请求，如果参数接受类型为 `V2TIM_FRIEND_ACCEPT_AGREE` 仅同意加单向好友时，A 会收到 [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) 回调，说明单向加好友成功，B 会收到 [onFriendApplicationListDeleted](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a143207515faa3de58c8222afc21736e6) 回调，此时 B 成为 A 的好友，但 A 仍不是 B 的好友。
	- 调用 [acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2546222b4994a5be9f67dfa8eb504e6b) 接受好友请求，如果参数接受类型为 `V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD` 同意加双向好友时，A 和 B 都会收到  [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) 回调，说明互相加好友成功。
    - 调用 [refuseFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acb564676b24c76609acf645c4ad999ad) 拒绝好友请求，双方都会收到 [onFriendApplicationListDeleted](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a143207515faa3de58c8222afc21736e6) 回调。

### 好友分组管理
在某些场景下，您可能需要对好友进行分组，例如分为 "大学同学"、"公司同事" 等，您可以调用以下接口实现。

| 功能描述 | 接口指引 |
|---------|---------|
| 新建好友分组 | [createFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acd85704b4a6ad4293d8bbcdb73385f4c) |
| 删除好友分组 | [deleteFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a73a1219065649398d4ba1001f9bd1c9b) |
| 修改好友分组 | [renameFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2677f9d9febe8f28f16f3972f7c45638) |
| 获取好友分组 |  [getFriendGroupList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a44c12380968b1d51c5ea5f90fa627a56) |
| 添加好友到一个分组 |  [addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a24b2297a1d9c2c3fa816839b3108ef72) |
| 从分组中删除某好友 |  [deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a65380db025573ac7c6d20f66a8b40ee2) |



## 常见使用问题

### 1. 非好友之间怎么禁止收发消息？
SDK 默认不限制非好友之间收发消息。如果您希望只允许好友之间收发消息，请在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【好友关系检查】中开启"发送单聊消息检查关系链"。开启之后，给陌生人发消息时，SDK 会报20009错误码。

[](id:sos) 
### 2. 被拉黑的用户发消息怎么给错误提示？
当消息发送者被拉黑后，发送者默认不会感知到“被拉黑”的状态，即发送消息后仍展示发送成功（实际上此时接收方不会收到消息）。如果需要被拉黑的发送者收到消息发送失败的提示，请在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【黑名单检查】中关闭"发送消息后展示发送成功"，关闭后，被拉黑的发送者在发送消息时，SDK 会报20007错误码。

### 3. 增强版获取用户资料为什么不是最新的？
增强版 SDK 中用户资料的更新分好友和陌生人两种情况：
 - 好友资料：由于好友资料更新时，后台会主动向 SDK 发送系统通知，因此好友资料可以实时更新。
 - 陌生人资料：陌生人资料更新时，由于没有好友关系，后台无法向 SDK 发送系统通知，因此无法实时更新；为了避免每次获取用户资料都向后台发起网络请求，SDK 增加了缓存逻辑，对同一个用户主动向后台拉取资料的时间间隔为10分钟。

