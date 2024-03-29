## 用户资料管理
### 查询和修改自己的资料
**查询自己的资料**接口为 [getUsersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e)，其中参数 `userIDList` 需填入自己的 UserID。
**修改自己的资料**接口为 [setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a)。修改自己的资料成功后，会收到 [onSelfInfoUpdated](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94852c92bb087e5aabb6cf6fe9ba77f8) 回调。

### 查询非好友用户资料
查询非好友资料接口同查询自己的资料 [getUsersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e)，参数 `userIDList` 填入非好友的 UserID 即可。

### 查询和修改好友的资料
**查询指定的好友资料**接口为 [getFriendsInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a88732b0f7a5e77a9dd34403fe7bbdd21)，从回调信息中通过 `V2TIMFriendInfoResult` 的 `getRelation()` 可以得到该用户与自己的关系：
- `V2TIMFriendCheckResult.V2TIM_FRIEND_RELATION_TYPE_NONE` 表示不是好友。
- `V2TIMFriendCheckResult.V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY` 表示互为好友。
- `V2TIMFriendCheckResult.V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST` 表示对方在我的好友列表中。
- `V2TIMFriendCheckResult.V2TIM_FRIEND_RELATION_TYPE_IN_OTHER_FRIEND_LIST` 表示我在对方的好友列表中。

**修改指定的好友信息**接口为 [setFriendInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a151b7de6219d966b4194ad7fcc8450fe) ，可修改好友备注等资料。

## 屏蔽某人消息
- **拉黑某人**
如需屏蔽某人的消息，请调用 [addToBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456) 接口把该用户加入黑名单，即拉黑该用户。
被拉黑的用户默认不会感知到“被拉黑”的状态，消息发送后不会返回已被对方拉黑的错误码。如果希望被拉黑的用户在发消息时返回已被对方拉黑的错误提醒，可以参考 [被拉黑的用户发消息怎么给错误提示](#msgSendTips)。

- **解除拉黑**
从黑名单中移除对方后可再次接收对方的消息，可调用 [deleteFromBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3dcd8f1c70dceafa94ab48796c2f26aa)。

- **获取黑名单列表**
您可以通过 [getBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6269df2d96c910648ab2f0c43e1931c6) 查看已拉黑多少用户，并对黑名单人员进行管理。

## 好友管理
### 是否需要加好友
IM SDK 在发送单聊消息的时候，默认不检查好友关系。在客服场景中，如果用户需要先加客服为好友才能进行沟通非常不方便，因此该默认设置常用于在线客服等场景。
如需实现类似“微信”或者“QQ”中“先加好友，再发消息”的交互体验，您可以在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【好友关系检查】中开启"发送单聊消息检查关系链"。开启后，用户只能给好友发送消息，当用户给非好友发消息时，SDK 会报20009错误码。


### 好友列表管理

IM SDK 支持好友关系链逻辑，您可以调用 [getFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624) 接口获取好友列表，调用 [deleteFromFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af7ecf8641b58462d038a9c97bfbd4d61) 接口删除好友关系，也可以调用 [addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) 接口添加好友。

根据对方用户资料中的加好友需要验证与否，可以分为两种处理流程：

#### 第一种 加好友不需要验证
1. 用户 A 和 B 调用 [setFriendListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a17e92c5ca9abad7afe25b654f1fcd75c) 设置关系链监听。
2. 用户 B 调用 [setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a) 接口并将参数 `info` 通过接口 [setAllowType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMUserFullInfo.html#a80c0d66aff28d26d9aee2bd8c5f41e61) 设置为加好友不需要验证 `V2TIM_FRIEND_ALLOW_ANY`。
3. 用户 A 调用  [addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) 申请添加 B 为好友即可添加成功。如果申请参数 `V2TIMFriendAddApplication` 中 [setAddType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendAddApplication.html#a2c03288fc9e47b30eb49259c206f97b5) 设置为双向好友即 `V2TIMFriendInfo.V2TIM_FRIEND_TYPE_BOTH`，则用户 A 和 B 都会收到 [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adf243539e005e2f7cdaa833fa4cd221c) 回调；
	如果设置为单向好友即 `V2TIMFriendInfo.V2TIM_FRIEND_TYPE_SINGLE`，则只有用户 A 收到 [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adf243539e005e2f7cdaa833fa4cd221c) 回调。

#### 第二种 加好友需要验证
1. 用户 A 和 B 调用 [setFriendListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a17e92c5ca9abad7afe25b654f1fcd75c) 设置关系链监听。
2. 用户 B 调用 [setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a) 接口并将参数 `info` 通过接口 [setAllowType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMUserFullInfo.html#a80c0d66aff28d26d9aee2bd8c5f41e61)  设置为加好友需要验证 `V2TIM_FRIEND_NEED_CONFIRM`。
3. 用户 A 调用  [addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) 申请添加 B 为好友，接口的成功回调参数中 `V2TIMFriendOperationResult` 中的 [getResultCode](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendOperationResult.html#ae27793c0f10a54e83dc5a7c5b6fc8843) 返回30539，表示需要等待用户 B 的验证，同时 A 和 B 都会收到 [onFriendApplicationListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adffb4589ee3fbeb1b7e0e95c4a80ccfa) 的回调。
4. 用户 B 会收到 [onFriendApplicationListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adffb4589ee3fbeb1b7e0e95c4a80ccfa) 的回调，当参数 `V2TIMFriendApplication` 中的 [getType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendApplication.html#aec389cbe6ac7aff8ce7196e7dbc007df) 为 `V2TIMFriendApplication.V2TIM_FRIEND_APPLICATION_COME_IN` 时，可以选择接受或者拒绝
	- 调用 [acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ab69ed69330428caff6f468b7df5259fa) 接受好友请求，如果参数接受类型为 `V2TIMFriendApplication.V2TIM_FRIEND_ACCEPT_AGREE` 仅同意加单向好友时，A 会收到 [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adf243539e005e2f7cdaa833fa4cd221c) 回调，说明单向加好友成功，B 会收到 [onFriendApplicationListDeleted](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#a64a3bec67f85ddfee3e0d4dafb3b1e46) 回调，此时 B 成为 A 的好友，但 A 仍不是 B 的好友。
	- 如果参数接受类型为 `V2TIMFriendApplication.V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD` 同意加双向好友时，双方都会收到  [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adf243539e005e2f7cdaa833fa4cd221c) 回调，说明互相加好友成功。
	- 调用 [refuseFriendApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af1bcbc196015de8e7a94b1575c466f89) 拒绝好友请求，双方都会收到 [onFriendApplicationListDeleted](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#a64a3bec67f85ddfee3e0d4dafb3b1e46) 回调。

### 好友分组管理
在某些场景下，您可能需要对好友进行分组，例如分为 "大学同学"、"公司同事" 等，您可以调用以下接口实现。

| 功能描述 | 接口指引 |
|---------|---------|
| 新建好友分组 | [createFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#afe729e7a74d1e7fd06a5f23c155a08ae) |
| 删除好友分组 | [deleteFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac9f06f447ee4452aa12e078b48023cee) |
| 修改好友分组 | [renameFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5345957f4d75d8e57ea3b4cff9adee13) |
| 获取好友分组 |  [getFriendGroupList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a0043ca81fdeec5d3e842e85278003d1e) |
| 添加好友到一个分组 |  [addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6de9168d476ac14e21025ec5c26251df) |
| 从分组中删除某好友 |  [deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae367dfec88522e96d96c5ab942e50653) |

## 常见使用问题

### 1. 非好友之间怎么禁止收发消息？
SDK 默认不限制非好友之间收发消息。如果您希望只允许好友之间收发消息，请在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【好友关系检查】中开启"发送单聊消息检查关系链"。开启之后，给陌生人发消息时，SDK 会报20009错误码。

[](id:msgSendTips)
### 2. 被拉黑的用户发消息怎么给错误提示？
当消息发送者被拉黑后，发送者默认不会感知到“被拉黑”的状态，即发送消息后仍展示发送成功（实际上此时接收方不会收到消息）。如果需要被拉黑的发送者收到消息发送失败的提示，请在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【黑名单检查】中关闭"发送消息后展示发送成功"，关闭后，被拉黑的发送者在发送消息时，SDK 会报20007错误码。

### 3. 增强版获取用户资料为什么不是最新的？
增强版 SDK 中用户资料的更新分好友和陌生人两种情况：
 - 好友资料：由于好友资料更新时，后台会主动向 SDK 发送系统通知，因此好友资料可以实时更新。
 - 陌生人资料：陌生人资料更新时，由于没有好友关系，后台无法向 SDK 发送系统通知，因此无法实时更新；为了避免每次获取用户资料都向后台发起网络请求，SDK 增加了缓存逻辑，对同一个用户主动向后台拉取资料的时间间隔为10分钟。
