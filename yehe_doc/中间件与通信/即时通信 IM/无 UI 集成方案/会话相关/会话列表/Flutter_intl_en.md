## Feature Description
After a user logs in to the application, the list of recent conversations can be displayed to make it easy to locate the target conversation.
The conversation list is as follows:
<img src="https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/res/RPReplay_Final0511.gif" alt="" style="zoom:40%;" />

The conversation list features include getting the conversation list and processing the conversation list update.
This section describes how to implement such features.

## Getting the Conversation List
You can call `getConversationList` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/getConversationList.html)) to get the conversation list. This API pulls locally cached conversations. If any server conversation is updated, the SDK will automatically sync the update and notify you in the `V2TIMConversationListener` callback.

User conversations are returned in a list that stores `V2TIMConversation` objects. Currently, the IM SDK sorts conversations according to the following rules:
* Starting from the SDK for Flutter 3.8.0, the conversations obtained through this API are sorted based on the `orderKey` conversation object by default. The greater the `orderKey` value of a conversation, the higher position the conversation is in the list. The `orderKey` field is an integer that increases as the conversation is activated when a message is sent/received, a draft is set, or the conversation is pinned to the top.
* For the SDK for Flutter earlier than v3.8.0, the conversations obtained through this API are sorted based on the `lastMessage` > `timestamp` of the conversation by default. The greater the `timestamp` value, the higher position the conversation is in the list.

> ! In certain cases, the `lastMessage` of a conversation might be empty, such as when the messages in the conversation are cleared. If you use the SDK earlier than v3.8.0, you need to handle the exception when sorting the conversations by `lastMessage`. We recommend you upgrade the SDK to v3.8.0 or later and sort the conversations by `orderKey`.

You can use `getConversationList` to implement one-time or paged pull as detailed below.

### One-time pull
One-time pull is suitable for scenarios with a small number of conversations (up to 100). You can set the `count` of the pull to `INT_MAX` (which is generally greater than the number of conversations).

Sample code:


```dart
V2TimValueCallback<V2TimConversationResult> convList = await TencentImSDKPlugin.v2TIMManager.getConversationManager().getConversationList(nextSeq: '0',count: 100);
```
### Pulling by page
If the number of conversations is great, pulling by page is recommended to enhance the loading efficiency and save network traffic. The recommended number of conversations pulled per page is up to 100.

Directions:
1. When you call `getConversationList` for the first time, set `nextSeq` to `0` (indicating to pull the conversation list from the beginning) and `count` to `50` (indicating to pull 50 conversation objects at a time).
   
2. After the conversation list is pulled successfully for the first time, the `V2TIMConversationResult` callback of `getConversationList` will contain `nextSeq` (field for the next pull) and `isFinish` (indicating whether the conversation pull is completed).
   * If `isFinished` is `true`, all the conversations have been pulled.
   * If `isFinished` is `false`, there are more conversations that can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common communications software, a paged pull is often triggered by a swipe operation.

3. When the user continues to pull up the conversation list, if there are more conversations that can be pulled, you can continue to call the `getConversationList` API and pass in the `nextSeq` and `count` parameters (the values are from the `V2TIMConversationResult` object returned by the last pull) for the next pull.

4. Repeat step 3 until `isFinished` is `true`.

Sample code:


```dart
V2TimValueCallback<V2TimConversationResult> convList = await TencentImSDKPlugin.v2TIMManager.getConversationManager().getConversationList(nextSeq: '0',count: 100);
var seq = convList.data.nextSeq;
  if(!convList.data.isFinished){
    // If there are more conversations that can be pulled
    
    V2TimValueCallback<V2TimConversationResult> convList = await TencentImSDKPlugin.v2TIMManager.getConversationManager().getConversationList(nextSeq: seq,count: 100);
  }
```



## Updating the Conversation List
After the IM SDK is logged in successfully, the user goes online, or the network is disconnected and reconnected, the IM SDK will automatically update the conversation list.
You can get the updated conversation list in the following steps:

1. Add a conversation listener.
2. Receive and process conversation changes.
3. Remove the conversation listener. This step is optional and can be performed as needed.

### Adding a conversation listener
Call `addConversationListener` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/addConversationListener.html)) to add a conversation listener to receive conversation change events.

Sample code:

```dart
TencentImSDKPlugin.v2TIMManager.getConversationManager().addConversationListener(listener: V2TimConversationListener(onConversationChanged: (conversationList) {
    
  },
	// Others                                                                                                                ));
```


### Getting the notification of a conversation change
You can listen for the event in `V2TIMConversationListener` to get the notification of a conversation list change.

Currently, the IM SDK supports the following conversation change events:

| Event                            | Description                                         | Suggestion                                                                                                                                        |
| -------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| onSyncServerStart                | Server conversation sync started.                   | Listen for such an event when the user logged in successfully or the network was disconnected and reconnected and display the progress on the UI. |
| onSyncServerFinish               | Server conversation sync was completed.             | Notify a conversation change through the `onNewConversation`/`onConversationChanged` callback.                                                    |
| onSyncServerFailed               | Server conversation sync failed.                    | Listen for such an event and display the exception on the UI.                                                                                     |
| onNewConversation                | A new conversation was added.                       | Re-sort the conversations when the user receives a one-to-one message from a new colleague or is invited to a new group.                          |
| onConversationChanged            | A conversation was updated.                         | Re-sort the conversations when the unread count changes or the last message is updated.                                                           |
| onTotalUnreadMessageCountChanged | The total unread count of the conversation changed. | For more information, see [unreadCount property](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#unreadcount).  |

> ? To ensure that the conversations are sorted by the last message, you need to re-sort the data sources each time a conversation is changed/added.
> * If you use the SDK for Flutter earlier than v3.8.0, you can sort the conversations by `lastMessage`, but note that sometimes `lastMessage` may be empty (such as when messages in a conversation are cleared).
> * If you use the SDK for Flutter on v3.8.0 or later, you can sort the conversations by `orderKey`.
> * We recommend you upgrade the SDK for Flutter to v3.8.0 or later.

Sample code:


```java
// Listen for the conversation
TencentImSDKPlugin.v2TIMManager.getConversationManager().addConversationListener(listener: V2TimConversationListener(onConversationChanged: (conversationList) {
    
  },
  onNewConversation: (conv){},
  onSyncServerFailed: (){},
  onSyncServerFinish: (){},
  onSyncServerStart: (){},
  onTotalUnreadMessageCountChanged: (count){}
  ));
```


### Removing a conversation listener
Call `removeConversationListener` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/removeConversationListener.html)) to remove a conversation listener to stop receiving conversation change events.
This step is optional and can be performed as needed.

Sample code:


```dart
conversationManager.removeConversationListener(conversationListener);
```



### Sending a message without updating the lastMessage
On UI of the conversation list, it is usually necessary to display the preview and send time of the latest message in each conversation. In this case, you can use `lastMessage` of `V2TIMConversation` as the data source for implementation. However, in some cases, if you don't want some messages (such as system tips) to be displayed as the latest message in a conversation, you can set `isExcludedFromLastMessage` to `false`/`no` when calling `sendMessage`.

For directions on how to send a message, see [sendMessage method](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html).


>? `isExcludedFromLastMessage` is supported only by the SDK for Flutter on v4.0.0 or later.



