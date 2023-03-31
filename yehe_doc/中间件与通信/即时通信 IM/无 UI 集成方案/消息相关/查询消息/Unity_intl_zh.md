## 功能描述
根据 messageID 可以调用 `MsgFindMessages` 查询本地消息。
1. 只支持查询本地消息，例如接收到的消息或者调用拉取历史消息接口获取到的消息。
2. 不支持查询直播群（AVChatRoom）的消息，因为其消息不会保存在本地。

## 查询本地消息
查询本地消息的接口为 `MsgFindMessages` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgFindMessages.html)) 。

示例代码如下：



```c#
// 根据消息id查询消息
TIMResult res = TencentIMSDK.MsgFindMessages(message_id_array, (int code, string desc, List<Message> messages, string user_data) => {
  // 处理回调逻辑
});
```
