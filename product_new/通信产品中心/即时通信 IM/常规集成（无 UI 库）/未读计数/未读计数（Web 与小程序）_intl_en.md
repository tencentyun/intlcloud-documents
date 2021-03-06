
Unread messages are messages that have not been reported as read by users. This does not indicate whether the recipient has actually read the messages. To display the correct unread count, developers need to explicitly call read reports to notify the IM SDK whether the messages in a conversation are read. For example, you can mark all messages as read when the user enters the chat UI.

## Obtaining the Current Unread Count

Every time you use [getConversationList()](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getConversationList), you will obtain a [[Conversation](https://web.sdk.qcloud.com/im/doc/zh-cn/Conversation.html)，[Conversation](https://web.sdk.qcloud.com/im/doc/zh-cn/Conversation.html), …] array. Each `Conversation` has an unread count for the current conversation, which is represented by `unreadCount`.
The unread count of all conversations is the sum of the `unreadCount` values of each conversation.


## Read Reports

When the user reads a message in a conversation, a read report is sent, and the IM SDK sets all messages before the last read message as read. We recommend that you send read reports when the user clicks to switch between conversations.

>? Read reports will change the unread count of a conversation. If you set `C2C` messages to read in SDK v2.7.0 or later versions, read receipts will be pushed to the message sender. For more information, see [TIM.EVENT.MESSAGE_READ_BY_PEER](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.MESSAGE_READ_BY_PEER).

**API**

```javascript
tim.setMessageRead(options)；
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute it contains is described in the following table:

| Name | Type | Description |
| ---------------- | -------- | ----------- |
| `conversationID` | `String` | Conversation ID |

**Example**

```javascript
//Send read reports for all unread messages in a conversation
let promise = tim.setMessageRead({conversationID: 'C2Cexample'});
promise.then(function(imResponse) {
//Read reports sent successfully
}).catch(function(imError) {
//Failed to send read reports
  console.warn('setMessageRead error:', imError);
});
```

