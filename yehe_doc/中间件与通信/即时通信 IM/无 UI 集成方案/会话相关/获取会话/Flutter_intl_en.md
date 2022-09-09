## Feature Description
The IM SDK provides an API for getting conversations, which can be used to get the `V2TimConversation` object information of one or multiple specified conversations.

### Getting a specified conversation
Call `getConversation` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/getConversation.html)) to get the information of a conversation, which is a `V2TimConversation` object.

Sample code:


```dart
V2TimValueCallback<V2TimConversation> conv = await conversationManager.getConversation(conversationID: "conversationID");
```


### Getting specified conversations

Call `getConversationList` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/getConversationList.html)) to get the list of specified conversations that stores `V2TimConversation` objects.

Sample code:


```dart
V2TimValueCallback<V2TimConversationResult> convList = await conversationManager.getConversationList(nextSeq: '', count: 10);
```



