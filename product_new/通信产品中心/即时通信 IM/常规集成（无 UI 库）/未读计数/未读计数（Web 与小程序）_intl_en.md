
Unread messages are messages that have not been reported as read by users. This does not indicate whether the recipient has actually read the messages. To display the correct unread count, developers need to explicitly call read reports to notify the IM SDK whether the messages in a conversation are read. For example, you can mark all messages as read when the user enters the chat UI.

## Obtaining the Current Unread Count

Every time you use [getConversationList()](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getConversationList), you will obtain a [[Conversation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html)，[Conversation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html), …] array. Each `Conversation` has an unread count for the current conversation, which is represented by `unreadCount`.
The unread count of all conversations is the sum of the `unreadCount` values of each conversation.


## Read Reports

When the user reads a message in a conversation, a read report is sent, and the IM SDK sets all messages before the last read message as read. We recommend that you send read reports when the user clicks to switch between conversations.

>Read reports change the unread count of a conversation, but do not push read receipts to the message sender.

**API**

```javascript
tim.setMessageRead(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute it contains is described in the following table:

| Name | Type | Description |
| ---------------- | -------- | ----------- |
| `conversationID` | `String` | Conversation ID |

**Example**

```javascript
// Send read reports for all unread messages in a conversation
tim.setMessageRead({conversationID: 'C2Cexample'});
```

