## Feature Description
If a message sender wants to know who has or has not read the message, the sender needs to enable the message read receipt feature.
After this feature is enabled, the sender can set whether a message requires a read receipt when sending the message; if yes, the sender will receive a receipt after the message is read by the receiver.

## Message Read Receipt

### Specifying a group type for which to support message read receipts

Log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Group Message Read Receipts**.
    
### Specifying that a message requires a read receipt (by the sender)

The sender creates a message, sets `needReadReceipt` to `true`, and sends the message.

<dx-codeblock>
:::  js

// Create a one-to-one message
let message = tim.createTextMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    text: 'Hello world!'
  },
  // The read receipt feature is supported for one-to-one messages by v2.20.0 or later. To use it, purchase the Ultimate edition package and set `needReadReceipt` to `true` when creating a message.
  needReadReceipt: true
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>


<dx-codeblock>
:::  js

// Create a group message
let message = tim.createTextMessage({
  to: 'test',
  conversationType: TIM.TYPES.CONV_GROUP,
  payload: {
    text: 'Hello world!'
  },
  // The read receipt feature is supported for group messages by v2.18.0 or later. To use it, purchase the Ultimate edition package and set `needReadReceipt` to `true` when creating a message.
  needReadReceipt: true
});
// Send the message
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

### Sending a message read receipt (by the receiver)

After receiving the message, the receiver determines whether the message requires a read receipt based on the `needReadReceipt` field in `Message`. If yes, after the user reads the message, the receiver calls the [sendMessageReadReceipt](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessageReadReceipt) API to send a read receipt.

>!
>- The read receipt feature is supported for group messages by v2.18.0 or later.
>- The read receipt feature is supported for one-to-one messages by v2.20.0 or later.
>- Messages in the `messageList` must be from the same one-to-one or group conversation.
>- After this API is called successfully, the unread count of the conversation will not change, and the sender will receive the [TIM.TYPES.MESSAGE_READ_RECEIPT_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_READ_RECEIPT_RECEIVED) callback which contains the latest read information of the message.

**API**

<dx-codeblock>
:::  js

tim.sendMessageReadReceipt(messageList);

:::
</dx-codeblock>

**Parameter**

| Name        | Type  | Description                                          |
| ----------- | ----- | ---------------------------------------------------- |
| messageList | Array | List of messages (up to 30) in the same conversation |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Pull the group message list
let messageList = null;
tim.getMessageList({conversationID: 'GROUPtest', count: 15}).then(function(imResponse) {
  messageList = imResponse.data.messageList; // Message list
  tim.sendMessageReadReceipt(messageList).then(function() {
    // Read receipt for the group message sent successfully
  }).catch(function(imError) {
    // Failed to send a read receipt for the group message
  });
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Pull the one-to-one message list
let messageList = null;
tim.getMessageList({conversationID: 'C2Ctest', count: 15}).then(function(imResponse) {
  messageList = imResponse.data.messageList; // Message list
  tim.sendMessageReadReceipt(messageList).then(function() {
    // Read receipt for the one-to-one message sent successfully
  }).catch(function(imError) {
    // Failed to send a read receipt for the one-to-one message
  });
});

:::
</dx-codeblock>


### Listening for a message read receipt notification (by the sender)

After the receiver sends a message read receipt, the sender can listen for a receipt notification and update the UI based on the notification to display the message as, for example, "Read by two members".

**Sample**

<dx-codeblock>
:::  js

let onMessageReadReceiptReceived = function(event) {
  // event.data - An array that stores message read receipt information
  const readReceiptInfoList = event.data;
  readReceiptInfoList.forEach((item) => {
    const { groupID, userID, messageID, readCount, unreadCount, isPeerRead } = item;
    // messageID - Message ID
    // userID - one-to-one message receiver
    // isPeerRead - Whether the one-to-one message is read by the receiver
    // groupID - Group ID
    // readCount - Number of members who have read the group message
    // unreadCount - Number of members who have not read the group message
    const message = tim.findMessage(messageID);
    if (message) {
     if (message.conversationType === TIM.TYPES.CONV_C2C) {
       if (message.isPeerRead === true) {
         // Read by the receiver
       }
     } else if (message.conversationType === TIM.TYPES.CONV_GROUP) {
      if (message.readReceiptInfo.unreadCount === 0) {
        // Read by all
      } else {
        // message.readReceiptInfo.readCount - Latest read count of the message
        // To query which group members have read the message, call the [getGroupMessageReadMemberList] API.
      }
     }
    }
  });
}
tim.on(TIM.EVENT.MESSAGE_READ_RECEIPT_RECEIVED, onMessageReadReceiptReceived);

:::
</dx-codeblock>


### Pulling message read receipt information (by the sender)

After entering the message list, the sender pulls historical messages first, and then calls the [getMessageReadReceipt](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList) API to pull the message read receipt information.

>!
>- The read receipt feature is supported for group messages by v2.18.0 or later.
>- The read receipt feature is supported for one-to-one messages by v2.20.0 or later.
>- Messages in the `messageList` must be from the same one-to-one or group conversation.

**API**

<dx-codeblock>
:::  js

tim.getMessageReadReceiptList(messageList);

:::
</dx-codeblock>

**Parameter**

| Name        | Type  | Description                               |
| ----------- | ----- | ----------------------------------------- |
| messageList | Array | List of messages in the same conversation |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Pull the group message list
let messageList = null;
tim.getMessageList({conversationID: 'GROUPtest', count: 15}).then(function(imResponse) {
  messageList = imResponse.data.messageList; // Message list
  tim.getMessageReadReceiptList(messageList).then(function(imResponse) {
    messageList = imResponse.data.messageList; // Message list
    // `getMessageReadReceiptList` is called successfully, `Message.readReceiptInfo` will contain the message read receipt information.
    // Message.readReceiptInfo.readCount - Read count of a message. To query which group members have read the message, call the [getGroupMessageReadMemberList] API.
    // Message.readReceiptInfo.unreadCount - Unread count of a message. `0` indicates that all members have read the message.
  }).catch(function(imError) {
    // Failed to pull the read receipt list
  });
});

:::
</dx-codeblock>


<dx-codeblock>
:::  js

// Pull the one-to-one message list
let messageList = null;
tim.getMessageList({conversationID: 'C2Ctest', count: 15}).then(function(imResponse) {
  messageList = imResponse.data.messageList; // Message list
  tim.getMessageReadReceiptList(messageList).then(function(imResponse) {
    messageList = imResponse.data.messageList; // Message list
    // After the message list is pulled successfully, `Message.readReceiptInfo` will contain the message read receipt information.
    // Message.readReceiptInfo.isPeerRead - Whether the receiver has sent a read receipt
  }).catch(function(imError) {
    // Failed to pull the read receipt list
  });
});

:::
</dx-codeblock>

### Pulling the list of members who have or have not read a group message (by the sender)

To view the list of members who have or have not read a group message, the sender can call the [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList) API to pull the member list by page.

>! This API is supported by v2.18.0 or later.

**API**

<dx-codeblock>
:::  js

tim.getGroupMessageReadMemberList(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name    | Type    | Description                                                  |
| ------- | ------- | ------------------------------------------------------------ |
| message | Message | Message instance                                             |
| cursor  | String  | Cursor for the paged pull. Pass in `''` for the first pull.  |
| filter  | Number  | Specifies to pull the list of members who have or have not read the message. Valid values: 0 - pull the list of members who have read the message; 1 - pull the list of members who have not read the message |
| count   | Number  | Number of members to be pulled per page. Maximum value: 100. |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Pull the list of members who have read the group message
let promise = tim.getGroupMessageReadMemberList({
  message,
  filter: 0,
  cursor: '', // Pass in `''` for the first pull
  count: 30,
});
promise.then(function(imResponse) {
  const { isCompleted, cursor, messageID, readUserIDList } = imResponse.data;
  // isCompleted - true: completed; false: not completed
  // cursor - Used for the subsequent pull when `isCompleted` is `false`
  // messageID - Group message ID
  // readUserIDList - List of `userID` values of members who have read the message
}).catch(function(imError) {
  // Failed to pull the list of members who have read the group message
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Pull the list of members who have not read the group message
let promise = tim.getGroupMessageReadMemberList({
  message,
  filter: 1,
  cursor: '', // Pass in `''` for the first pull
  count: 30,
});
promise.then(function(imResponse) {
  const { isCompleted, cursor, messageID, readUserIDList } = imResponse.data;
  // isCompleted - true: completed; false: not completed
  // cursor - Used for the subsequent pull when `isCompleted` is `false`
  // messageID - Group message ID
  // unreadUserIDList - List of `userID` values of members who have not read the group message
}).catch(function(imError) {
  // Failed to pull the list of members who have not read the group message
  // 10062 - The read receipt information for the group message was not found.
});

:::
</dx-codeblock>