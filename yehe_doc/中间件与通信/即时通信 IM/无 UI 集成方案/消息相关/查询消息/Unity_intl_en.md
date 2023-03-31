## Feature Description
You can call `MsgFindMessages` to query a local message by `messageID`.
1. Only local messages can be queried, for example, received messages or historical messages pulled by API.
2. Audio-video group (AVChatRoom) messages cannot be queried, as they are not saved locally.

## Querying a Local Message
Call the `MsgFindMessages` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgFindMessages.html)) to query a local message.

Sample code:



```c#
// Query a message by message ID
TIMResult res = TencentIMSDK.MsgFindMessages(message_id_array, (int code, string desc, List<Message> messages, string user_data) => {
  // Process the callback logic
});
```
