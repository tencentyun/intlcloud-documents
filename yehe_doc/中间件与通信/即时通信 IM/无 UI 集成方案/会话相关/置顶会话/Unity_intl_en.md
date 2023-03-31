## Feature Description
Pinning a conversation to the top is to fix a one-to-one or group conversation at the top of the conversation list to facilitate search. The status of a conversation being pinned to the top will be stored on the server and synced to new devices.



## Pinning a Conversation to the Top
Call the `ConvPinConversation` API ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_ConvPinConversation_System_String_com_tencent_imsdk_unity_enums_TIMConvType_System_Boolean_com_tencent_imsdk_unity_callback_NullValueCallback_)) to set whether to pin a conversation to the top.

Note that a conversation pinned to the top will always be displayed above others. If multiple conversations are pinned to the top, they will be sorted in the original order. For example, if there are five conversations (1, 2, 3, 4, and 5 in order) and conversations 2 and 3 are pinned to the top, the new order will be 2, 3, 1, 4, and 5. Obviously, conversations 2 and 3 are displayed above others, and conversation 2 is displayed above conversation 3.

When `ConvGetConvList` is called to get the conversation list, it will first return the conversation that is pinned to the top and then other conversations. You can check whether a conversation is pinned to the top through the `conv_is_pinned` field of the `ConvInfo` object.

Sample code:


```c#
// If `conv_is_pinned` is `true`, the conversation is pinned to the top; otherwise, it is not.
bool conv_is_pinned = true;
TIMResult res = TencentIMSDK.ConvPinConversation(conv_id, conv_is_pinned, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


## Notification of the Pinned Status Change
If you have called `SetConvEventCallback` ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_SetConvEventCallback_com_tencent_imsdk_unity_callback_ConvEventCallback_com_tencent_imsdk_unity_callback_ConvEventStringCallback_)) to add a conversation listener, you can get the `conv_is_pinned` value of the `ConvInfo` object in `ConvEventCallback` and determine whether the pinned status of a conversation has changed.
Sample code:

```c#
TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
  foreach(ConvInfo conv_info in conv_list) {
    if (conv_info.conv_is_pinned) {
      // Process the callback logic
    }
  }
});
```
