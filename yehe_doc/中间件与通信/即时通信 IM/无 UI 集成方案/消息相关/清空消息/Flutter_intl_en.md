## Feature Description
One-to-one messages and group messages can be cleared.
When messages in a conversation are cleared, all the messages in the conversation will be cleared both **locally and from the cloud**, but the conversation itself will not be deleted.

> ?**Do not** use this API if you do not want to clear messages from the cloud.

If the last message is deleted, the `lastMessage` in the conversation will become the last but one message.



### Clearing one-to-one messages

Call `clearC2CHistoryMessage` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/clearC2CHistoryMessage.html)) to clear one-to-one messages.


Sample code:



```dart
TencentImSDKPlugin.v2TIMManager.getMessageManager().clearC2CHistoryMessage(userID: "userid");
```



### Clearing group messages

Call `clearGroupHistoryMessage` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/clearGroupHistoryMessage.html)) to clear group messages.

Sample code:


```dart
 TencentImSDKPlugin.v2TIMManager.getMessageManager().clearGroupHistoryMessage(groupID: "");
```

