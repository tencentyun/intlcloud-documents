## Feature Description
You can call `MsgFindMessages` to query a local message by `messageID`.
1. Only local messages can be queried, for example, received messages or historical messages pulled by API.
2. Audio-video group (AVChatRoom) messages cannot be queried, as they are not saved locally.

## Querying a Local Message
Call the `MsgFindMessages` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgFindMessages_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_Message___)) to query a local message.

Sample code:



```c#
// Query a message by message ID
TIMResult res = TencentIMSDK.MsgFindMessages(message_id_array, (int code, string desc, List<Message> messages, string user_data) => {
  // Process the callback logic
});
```


