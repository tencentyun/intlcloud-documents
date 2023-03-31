## Feature Description
If a user doesn't want to view the historical one-to-one or group messages after deleting a friend or leaving a group, the user can choose to delete the conversation.
> ! When a conversation is deleted, the historical messages will be deleted from both the client and the server and cannot be recovered.

Multi-client sync is disabled for conversation deletion by default and can be enabled in the [IM console](https://console.cloud.tencent.com/im-detail/login-message).


## Deleting a Conversation
Call the `ConvDelete` API ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_ConvDelete_System_String_com_tencent_imsdk_unity_enums_TIMConvType_com_tencent_imsdk_unity_callback_NullValueCallback_)) to delete a specified conversation.

Sample code:


```c#
// Delete a specified conversation
TIMResult res = TencentIMSDK.ConvDelete(conv_id, conv_type, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```
