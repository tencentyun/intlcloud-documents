## 展示会话列表
用户在登录 App 后，可以最近会话列表。整个过程分为**拉取会话列表**、**处理更新通知**和**更新 UI 内容（包括未读计数）**，本文主要介绍这些步骤的详细细节。

![](https://qcloudimg.tencent-cloud.cn/raw/9645e51a0a98b5aa7725ff742920cfa3.png)

### 拉取会话列表
用户在登录后调用 [getConversationList()](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/getConversationList.html) 拉取本地会话列表做 UI 展示，会话列表是一个 [V2TIMConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html) 对象的列表，每一个对象都代表一个会话。

由于本地会话可能很多（例如超过500个），一次性全部加载完毕可能会耗时很久，导致界面展示比较慢。为了提升用户体验，`getConversationList()` 接口支持分页拉取能力：
1. 首次调用 `getConversationList()` 接口时，可以指定其参数 `nextSeq` 为0 ，表示从头开始拉取会话列表，并指定 `count` 为50， 表示一次拉取50个会话对象。
2. IM SDK 按照从新到旧的顺序拉取会话列表，当首次拉取会话列表成功后，`getConversationList()` 的回调结果 [V2TIMConversationResult](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversationResult.html) 中会包含下次分页拉取的 `nextSeq`  字段以及会话拉取是否完成的 `isFinish` 字段：
 - 如果 `isFinished` 返回 `true`，表示所有会话已经拉取完成。
 - 如果 `isFinished` 返回 `false` ，表示还有更多的会话可以拉取。此时并不意味着要立刻开始拉取“下一页”的会话列表。在常见的通信软件中，分页拉取通常由用户的滑动操作触发的，用户每下拉一次会话列表就触发一次分页拉取。
[](id:get_step3)
3. 当用户继续下拉会话列表时，如果还有没有拉取下来的会话列表，可以继续调用 [getConversationList](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/getConversationList.html) 接口，并传入新一轮的 `nextSeq` 和 `count` 参数（数值来自上一次拉取返回的 [V2TimConversationResult](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversationResult.html) 对象）。
5. 重复执行 [步骤3](#get_step3) 直至 [isFinished](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversationResult.html) 返回 `true`。

### 显示会话信息
获取到 [V2TimConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html)  对象后，即可在 UI 上展示，`V2TIMConversation` 有如下关键字段常被用于构造会话列表：

| 字段名称                                                                                                        | 含义                                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [showName](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#showname)          | 会话名称：<li>如果是单聊，此接口会优先返回对方好友备注，若没有备注或者不是好友，则返回对方昵称，若昵称也没有，则返回对方的 UserID。</li><li>如果是群聊，会显示群的名称。</li> |
| [faceUrl](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#faceurl)            | 会话头像：<li>如果是单聊，会显示对方的头像。</li><li>如果是群聊，会显示群头像。</li>                                                                                          |
| [recvOpt](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html?q=#recvopt)         | 消息接收选项，一般用于群会话，可以显示该群是否设置了“消息免打扰”模式。                                                                                                        |
| [readCount](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#unreadcount)      | 用于显示未读计数，表示有多少条未读消息。                                                                                                                                      |
| [lastMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html?q=#lastmessage) | 最后一条消息，用于显示会话的消息摘要。                                                                                                                                        |

### 更新会话列表

IM SDK 会在登录成功后、用户上线后、以及断线重连后，自动更新会话列表。更新过程如下：
- 当有会话更新时，例如新收到一条消息，SDK 会通过 `V2TIMConversationListener`  中的 [onConversationChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnConversationChangedCallback.html) 事件通知您。
- 当有会话新增时，SDK 会通过 `V2TIMConversationListener`  中的 [onNewConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnNewConversation.html) 事件通知您。

>!为保证会话列表顺序符合最后一条消息的排序原则，您需要根据 [lastMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#lastmessage) 中的 [timestamp](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html#timestamp) 对数据源重新排序。

### 示例代码
示例代码将介绍如何拉取、展示和更新会话列表：

```dart
// 1. 注册会话监听器
    await TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .setConversationListener(
          listener: new V2TimConversationListener(
            onConversationChanged: (List<V2TimConversation> list){
				// ...
			},
            onNewConversation:(List<V2TimConversation> list){
				// ...
			},
			// 其他监听...
          ),
        );
// 2. 先拉取50个本地会话做 UI 展示，nextSeq 第一次拉取传0
  getConversationList() async {
    V2TimValueCallback<V2TimConversationResult> res = await TencentImSDKPlugin
        .v2TIMManager
        .getConversationManager()
        .getConversationList(nextSeq: nextSeq, count: 10);
    V2TimValueCallback<V2TimConversationResult> nextRes =
        await TencentImSDKPlugin.v2TIMManager
            .getConversationManager()
            .getConversationList(nextSeq: res.data?.nextSeq ?? "0", count: 20);
// 3.1 收到会话新增的回调
    await TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .setConversationListener(
          listener: new V2TimConversationListener(
            onNewConversation:(List<V2TimConversation> conversationList){
				// .......
			},
          ),
        );
// 3.2 收到会话更新的回调
     TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .setConversationListener(
          listener: new V2TimConversationListener(
            onConversationChanged: (List<V2TimConversation> list){
				// 调用更新方法
				_onConversationListChanged(list);
				// ...
			},
          ),
        );
	
	final List<V2TimConversation> _conversationList = [];
  // 排序方法
  sort() {
    _conversationList.sort((a, b) => b!.orderkey!.compareTo(a!.orderkey!));
  }

  _onConversationListChanged(List<V2TimConversation> list) {
    for (int element = 0; element < list.length; element++) {
      int index = _conversationList.indexWhere(
          (item) => item!.conversationID == list[element].conversationID);
      if (index > -1) {
        _conversationList.setAll(index, [list[element]]);
      } else {
        _conversationList.add(list[element]);
      }
    }

    
  }

  // 排序
  sort();
	//...
	
	
}

```
## 获取所有未读消息总数
调用 [getTotalUnreadMessageCount](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/getTotalUnreadMessageCount.html)  接口可以获取所有会话的未读消息总数。您不用再遍历会话列表，把单个会话的未读数相加，才能得到未读总数。当会话的未读总数发生变更的时候，SDK 会主动向您的 App 回调  [onTotalUnreadMessageCountChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnTotalUnreadMessageCountChanged.html)，把最新的未读总数通知给您。


## 置顶会话
会话置顶指的是把特定的好友或者群会话固定在会话列表的最前面，新版本 SDK 增加了主动设置或者取消会话置顶的接口  [pinConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/pinConversation.html) ，同时支持漫游和多端同步。
会话对象 [V2TIMConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html)  新增了 [isPinned](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#ispinned) 接口，用于判断会话的置顶状态。当会话的置顶状态发生变更的时候，SDK 会向您的 App 回调 [onConversationChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnConversationChangedCallback.html)。

## 删除会话
调用 [deleteConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/deleteConversation.html) 接口可以删除某个会话，会话删除默认关闭多端同步，可在控制台开启多端同步，删除会话时默认删除本地和服务器历史消息，且无法恢复。


## 草稿箱
在发送消息时，可能会遇到消息尚未编辑完就要切换至其它聊天窗口的情况，这些未编辑完的消息可通过 [setConversationDraft](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/setConversationDraft.html) 接口保存，以便于回到聊天界面后使用 [V2TimConversation中的draftText](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html) 继续编辑内容。

>?
>- 草稿仅支持文本内容。
>- 草稿仅在本地保存，不会存储到服务器，因此不能多端同步，程序卸载重装会失效。

## 常见问题
### 1. 最近会话列表的保存数量上限是多少？
本地存储的会话列表没有数量上限，云端存储的会话列表最大数量为100。
如果一个会话长时间没有信息变更，该会话在云端最多保存7天，如需放宽限制，请 [联系我们](https://console.cloud.tencent.com/workorder/category)。

### 2. 为什么换了一个手机登录相同帐号后拉取的会话列表不一致？
本地存储的会话和云端存储的会话并不总是一致的，如果用户不主动调用 [deleteConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/deleteConversation.html) 接口删除本地的会话，该会话就会一直存在。而云端存储的会话最大只会保存100条，且对于长时间没有信息变更的会话，云端最多保存7天，所以不同的终端本地显示的会话可能会不一样。

### 3. 为什么会拉取到重复的会话？
调用 `getConversationList` 接口拉取的会话可能已经通过 `onNewConversation` 回调接口添加到了 UI 会话列表的数据源中，因此为了避免重复添加同一个会话，您需要在 UI 会话列表数据源中根据 [ConversationID](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#conversationid) 找到相同的会话并做替换。

### 4. IM SDK 支持会话置顶吗？
支持，会话列表，会话信息都会获取到 isPinned 字段。
