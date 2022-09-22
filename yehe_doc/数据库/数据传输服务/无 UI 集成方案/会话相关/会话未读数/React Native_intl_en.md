## Feature Description

A user's conversation list usually contains multiple conversations. If there is a new message in one of the conversations, a badge needs to be displayed in the list cell to indicate the unread count.
After the user clicks to enter the conversation and goes back to the conversation list, the unread count is cleared, and the badge disappears.
In some applications, the total unread count of all the conversations is calculated and displayed at the bottom tab of the conversation list.

This document describes how to implement the conversation unread count notification feature.

## Getting the Total Unread Count of All the Conversations

In general cases, to get the total unread count of all the conversations, you can traverse the conversation list to get the `V2TimConversation` information of each conversation and add the `unreadCount` values of all the `V2TimConversation` objects to get the final result and display it on the UI.
The IM SDK provides the `getTotalUnreadMessageCount` API to query the total unread count of all the conversations.
When the total unread count changes, the SDK will notify you of the latest total unread count through the `onTotalUnreadMessageCountChanged` callback.

Below are detailed steps.

### Getting the total unread count

Call `getTotalUnreadMessageCount` ([TS](https://comm.qq.com/im-react-native-doc/classes/ConversationManager________.V2TIMConversationManager.html#getTotalUnreadMessageCount)) to get the total unread count of all the conversations and update it on the UI.

Sample code:

```javascript
// Get the total unread count
const unread = await conversationManager.getTotalUnreadMessageCount();
```

### Notification of a change in the total unread count

Call `addConversationListener` ([TS](https://comm.qq.com/im-react-native-doc/classes/ConversationManager________.V2TIMConversationManager.html#addConversationListener)) to add a conversation listener to receive notifications of a change in the total unread count.

You can get the changed total unread count in `onTotalUnreadMessageCountChanged` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimConversationListener-1.html#onTotalUnreadMessageCountChanged)) of `V2TIMConversationListener`.

Sample code:

```javascript
conversationManager.addConversationListener({
  onTotalUnreadMessageCountChanged: (totalUnreadCount) => {
    // Latest unread count
  },
});
```

## Clearing the Conversation Unread Count

After the user clicks to enter a conversation and goes back to the conversation list, the unread count needs to be cleared, after which the badge in the conversation list needs to disappear.
The IM SDK provides three APIs to clear the unread count for different conversation types:

- `markC2CMessageAsRead` is used to clear the unread count of a **one-to-one conversation**.
- `markGroupMessageAsRead` is used to clear the unread count of a **group conversation**.
- `markAllMessageAsRead` is used to clear the unread count of **all** the conversations.

Below are detailed steps.

> ? This feature is only available for the Enhanced edition on v5.8.1668 or later.

### One-to-one chat

Call `markC2CMessageAsRead` ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#markC2CMessageAsRead)) to clear the unread count of a specified one-to-one conversation.

Sample code:

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .markC2CMessageAsRead("userID");
```

After `markC2CMessageAsRead` is called successfully:

1. If the caller has called `addConversationListener` to add a conversation listener, it will receive the `onConversationChanged` callback and update the UI.
2. The sender will receive the `onRecvC2CReadReceipt` callback that contains the timestamp when the conversation unread count is cleared.

Sample code:

```javascript
// Receiver
conversationManager.addConversationListener({
  onConversationChanged: (conversationList) => {
    // Latest conversation after the change
  },
});

// Sender
TencentImSDKPlugin.v2TIMManager.getMessageManager().addAdvancedMsgListener({
  onRecvC2CReadReceipt: (receiptList) => {
    // The message is read by the receiver.
  },
});
```

### Group chat

Call `markGroupMessageAsRead` ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#markGroupMessageAsRead)) to clear the unread count of a specified group conversation.

Sample code:

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .markGroupMessageAsRead("groupID");
```

After `markGroupMessageAsRead` is called successfully, if the caller has called `addConversationListener` to add a conversation listener, it will receive the `onConversationChanged` callback and update the UI.

Sample code:

```javascript
conversationManager.addConversationListener({
  onConversationChanged: (conversationList) => {
    // Latest conversation after the change
  },
});
```

### All conversations

Call `markAllMessageAsRead` ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#markAllMessageAsRead)) to clear the unread count of all the conversations.

Sample code:

```javascript
TencentImSDKPlugin.v2TIMManager.getMessageManager().markAllMessageAsRead();
```

After `markAllMessageAsRead` is called successfully, if the caller has called `addConversationListener` in advance to add a conversation listener, it will receive the `onConversationChanged` callback and update the UI.

Sample code:

```javascript
conversationManager.addConversationListener({
  onConversationChanged: (conversationList) => {
    // Latest conversation after the change
  },
});
```


