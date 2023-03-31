## Feature Description

After a user logs in to the application, the list of recent conversations can be displayed as in WeChat or QQ to make it easy to locate the target conversation.
The conversation list features include getting the conversation list and processing the conversation list update.
This document describes how to implement such features.

## Getting the Conversation List

You can call `getConversationList` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMConversationManager/getConversationList.html)) to get the conversation list. This API pulls locally cached conversations. If any server conversation is updated, the SDK will automatically sync the update and notify you in the `V2TIMConversationListener` callback.

User conversations are returned in a list that stores `V2TIMConversation` objects. Currently, the IM SDK sorts conversations according to the following rules:

- The conversations obtained through this API are sorted based on the `orderKey` conversation object by default. The greater the `orderKey` value of a conversation, the higher position the conversation is in the list. The `orderKey` field is an integer that increases as the conversation is activated when a message is sent/received, a draft is set, or the conversation is pinned to the top.

You can use `getConversationList` to implement one-time or paged pull as detailed below.

### One-time pull

One-time pull is suitable for scenarios with a small number of conversations (up to 100). You can set the `count` of the pull to `INT_MAX` (which is generally greater than the number of conversations).

Below is the sample code:

```javascript
const nextSeq = "0";
const count = 100;
const convList = await TencentImSDKPlugin.v2TIMManager
  .getConversationManager()
  .getConversationList(count, nextSeq);
```

### Paged pull

If the number of conversations is great, paged pull is recommended to enhance the loading efficiency and save network traffic. The recommended number of conversations pulled per page is up to 100.

Directions for paged pull:

1. When you call `getConversationList` for the first time, set `nextSeq` to `0` (indicating to pull the conversation list from the beginning) and `count` to `50` (indicating to pull 50 conversation objects at a time).
2. After the conversation list is pulled successfully for the first time, the `V2TIMConversationResult` callback of `getConversationList` will contain `nextSeq` (field for the next pull) and `isFinish` (indicating whether the conversation pull is completed).

   - If `isFinished` is `true`, all the conversations have been pulled.
   - If `isFinished` is `false`, there are more conversations that can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common communications software, a paged pull is often triggered by a swipe operation.

3. When the user continues to pull up the conversation list, if there are more conversations that can be pulled, you can continue to call the `getConversationList` API and pass in the `nextSeq` and `count` parameters (the values are from the `V2TIMConversationResult` object returned by the last pull) for the next pull.

4. Repeat step 3 until `isFinished` is `true`.

Below is the sample code:

```javascript
const nextSeq = "0";
const count = 100;
const convList = await TencentImSDKPlugin.v2TIMManager
  .getConversationManager()
  .getConversationList(count, nextSeq);
const seq = convList.data.nextSeq;
if (!convList.data.isFinished) {
  // If there are more conversations that can be pulled

  const convList = await TencentImSDKPlugin.v2TIMManager
    .getConversationManager()
    .getConversationList(count, seq);
}
```

## Updating the Conversation List

After the IM SDK is logged in successfully, the user goes online, or the network is disconnected and reconnected, the IM SDK will automatically update the conversation list.
You can get the updated conversation list in the following steps:

1. Add a conversation listener.
2. Receive and process conversation changes.
3. Remove the conversation listener. This step is optional and can be performed as needed.

### Adding a conversation listener

Call `addConversationListener` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMConversationManager/addConversationListener.html)) to add a conversation listener to receive conversation change events.

Below is the sample code:

```javascript
TencentImSDKPlugin.v2TIMManager
  .getConversationManager()
  .addConversationListener({
    onConversationChanged: (conversationList) => {},
    // Others                                                                                                                ));
  });
```

### Getting the notification of a conversation change

You can listen for the event in `V2TIMConversationListener` ([Details](https://comm.qq.com/im/doc/RN/en/Interface/Listener/V2TimConversationListener.html)) to get the notification of a conversation list change.

Currently, the IM SDK supports the following conversation change events:

| Event                            | Description                                                  | Suggestion                                                   |
| -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| onSyncServerStart                | Server conversation sync started.                            | The SDK will automatically sync server conversations after a successful login or network reconnection. You can listen for such an event and display the event progress on the UI. |
| onSyncServerFinish               | Server conversation sync was completed.                      | If there is a conversation change, the change will be notified through the `onNewConversation`/`onConversationChanged` callback. |
| onSyncServerFailed               | Server conversation sync failed.                             | You can listen for such an event and display the event exception on the UI. |
| onNewConversation                | A new conversation was added.                                | When the user receives a one-to-one message from a new colleague or is invited to a new group, you can re-sort the conversations. |
| onConversationChanged            | There is a conversation update                               | When the unread count changes or the last message is updated, you can re-sort the conversations. |
| onTotalUnreadMessageCountChanged | Notification of a change in the total unread count of the conversation | For more information, see [unreadCount](https://comm.qq.com/im/doc/RN/en/Interface/Message/V2TimConversation.html#unreadcount). |

Below is the sample code:

```javascript
// Listen for the conversation
TencentImSDKPlugin.v2TIMManager
  .getConversationManager()
  .addConversationListener({
    onConversationChanged: (conversationList) => {},
    onNewConversation: (conv) => {},
    onSyncServerFailed: () => {},
    onSyncServerFinish: () => {},
    onSyncServerStart: () => {},
    onTotalUnreadMessageCountChanged: (count) => {},
  });
```

### Removing a conversation listener

Call `removeConversationListener` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMConversationManager/removeConversationListener.html)) to remove a conversation listener to stop receiving conversation change events.
This step is optional and can be performed as needed.

Below is the sample code:

```javascript
conversationManager.removeConversationListener(conversationListener);
```

### Sending a message without updating the lastMessage

On the conversation list UI, it is usually necessary to display the preview and send time of the latest message in each conversation. In this case, you can use `lastMessage` of `V2TIMConversation` as the data source for implementation. However, in some cases, if you don't want some messages (such as system tips) to be displayed as the latest message in a conversation, you can set `isExcludedFromLastMessage` to `false`/`no` when calling `sendMessage`.

For directions on how to send a message, see [sendMessage](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html).
