````java
## Overview
Pinning a conversation to the top is to fix a one-to-one or group conversation at the top of the conversation list to facilitate search. The status of a conversation being pinned to the top will be stored on the server and synced to new devices.

>!The maximum number of conversations pinned to the top is 50, and this limit cannot be increased.

## Pinning a Conversation to the Top
Call the `pinConversation` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/pinConversation.html)) to set whether to pin a conversation to the top.

The conversations are sorted based on the `orderKey` field of the `V2TimConversation` object. This field is an integer that increases as the conversation is activated when a message is sent/received, a draft is set, or the conversation is pinned to the top.

Note that a conversation pinned to the top will always be displayed above others. If multiple conversations are pinned to the top, they will be sorted in the original order. For example, if there are five conversations (1, 2, 3, 4, and 5 in order) and conversations 2 and 3 are pinned to the top, the new order will be 2, 3, 1, 4, and 5. Obviously, conversations 2 and 3 are displayed above others, and conversation 2 is displayed above conversation 3.

When `getConversationList` is called to get the conversation list, it will first return the conversation that is pinned to the top and then other conversations. You can check whether a conversation is pinned to the top through the `isPinned` field of the `V2TIMConversation` object.

Sample code:


```dart
// If `isPinned` is `true`, the conversation is pinned to the top; otherwise, it is not.
bool isPinned = true;
conversationManager.pinConversation(conversationID: "conversationID", isPinned: isPinned);
```


## Notification of the Pinned Status Change
If you have called the `addConversationListener` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/addConversationListener.html)) in advance to add a conversation listener, you can get the `isPinned` value of the `V2TimConversation` object in `onConversationChanged` and determine whether the pinned status of a conversation has changed.
Sample code:

```java
conversationManager.addConversationListener(listener: V2TimConversationListener(onConversationChanged: (conversationList) {
    // Latest conversation after the change
  },));
```xxxxxxxxxx conversationManager.addConversationListener(listener: V2TimConversationListener(onConversationChanged: (conversationList) {    // Latest conversation after the change  },));java
````
