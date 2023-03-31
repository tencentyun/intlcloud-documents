## 功能描述

清空消息分为两种：清空单聊消息、清空群聊消息。
清空消息会同时清空当前会话内所有的消息，包含**本地和云端**消息，但不会删除会话本身。

> ?如果不想清空云端消息，请**不要**使用本接口。

如果删除的是最后一条消息，会话的 `lastMessage` 会变为前一条消息。

### 清空单聊消息

您可以调用 `clearC2CHistoryMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/clearC2CHistoryMessage.html)) 清空单聊消息。

示例代码如下：

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .clearC2CHistoryMessage("userid");
```

### 清空群聊消息

您可以调用 `clearGroupHistoryMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/clearGroupHistoryMessage.html)) 清空群聊消息。

示例代码如下：

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .clearGroupHistoryMessage("groupID");
```
