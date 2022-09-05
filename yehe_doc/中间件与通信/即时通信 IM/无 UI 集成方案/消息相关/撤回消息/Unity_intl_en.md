## Feature Description
- The method for recalling a message is `MsgRevoke` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgRevoke_System_String_com_tencent_imsdk_unity_enums_TIMConvType_com_tencent_imsdk_unity_types_Message_com_tencent_imsdk_unity_callback_NullValueCallback_)).
- The receiver listens for a message recall notification through `SetMsgRevokeCallback` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_SetMsgRevokeCallback_com_tencent_imsdk_unity_callback_MsgRevokeCallback_com_tencent_imsdk_unity_callback_MsgRevokeStringCallback_)).

## Recalling a Message
The sender can recall a successfully sent message.

By default, the sender can recall a message sent within two minutes. You can change the time limit for message recall as instructed in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

Message recall can be implemented through the receiver UI code: When a message is recalled, the receiver will receive the `MsgRevokeCallback` notification which contains the `msgID` of the recalled message. You can identify the recalled message at the UI layer based on the `msgID` and change the bubble for the message to the "Message recalled" status.

### Recalling a message (by the sender)
The sender calls `MsgRevoke` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgRevoke_System_String_com_tencent_imsdk_unity_enums_TIMConvType_com_tencent_imsdk_unity_types_Message_com_tencent_imsdk_unity_callback_NullValueCallback_)) to recall a message.

Sample code:


```c#
    Message message = new Message(); // Here, the message can be an instance returned by another API, such as the message list API.

    TIMResult res = TencentIMSDK.MsgRevoke(conv_id, TIMConvType.kTIMConv_C2C, message, (int code, string desc, string user_data) => {
      // Process the callback logic
    });
```


### Noticing a message recall (by the receiver)
- The receiver receives a message recall notification through `SetMsgRevokeCallback` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_SetMsgRevokeCallback_com_tencent_imsdk_unity_callback_MsgRevokeCallback_com_tencent_imsdk_unity_callback_MsgRevokeStringCallback_)).

Sample code:


```c#
TencentIMSDK.SetMsgRevokeCallback((List<MsgLocator> msg_locator, string user_data) => {
      // Process the recalled message among locally maintained messages
});
```

