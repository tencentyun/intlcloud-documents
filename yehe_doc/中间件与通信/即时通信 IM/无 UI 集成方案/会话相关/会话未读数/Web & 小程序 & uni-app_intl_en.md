## Feature Description

A user's conversation list usually contains multiple conversations. If there is a new message in one of the conversations, a badge needs to be displayed in the list cell to indicate the unread count.
After the user clicks to enter the conversation and goes back to the conversation list, the unread count is cleared, and the badge disappears. In some applications, the total unread count of all the conversations is calculated and displayed at the bottom tab of the conversation list.

## Clearing the Conversation Unread Count

**API**

<dx-codeblock>
:::  js

tim.setMessageRead(options);

:::
</dx-codeblock>

The `options` parameter is of the `Object` type. It contains the following attribute values:

**Parameter**

| Name           | Type   | Default | Description                                                  |
| -------------- | ------ | ------- | ------------------------------------------------------------ |
| conversationID | String |         | Conversation ID. Valid values:<br/><li>C2C${userID} (for a one-to-one chat)</li><li>GROUP{groupID} (for a group chat)</li><li>@TIM#SYSTEM (for a system notification conversation)</li><li>GROUP${topicID} (for a topic). It is supported by v2.19.1 or later.</li> |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Set all the unread messages in a conversation as read
let promise = tim.setMessageRead({conversationID: 'C2Cexample'});
promise.then(function(imResponse) {
  // Set the unread messages as read successfully. The value of the `unreadCount` attribute of the conversation with the specified ID is set to `0`.
}).catch(function(imError) {
  // Failed to set the unread messages as read
  console.warn('setMessageRead error:', imError);
});

:::
</dx-codeblock>


## Clearing the Unread Count of All Conversations

>! This feature is supported by v2.16.0 or later.

<dx-codeblock>
:::  js

tim.setAllMessageRead(options);

:::
</dx-codeblock>

The `options` parameter is of the `Object` type. It contains the following attribute values:

**Parameter**

| Name  | Type                | Description                                                  |
| ----- | ------------------- | ------------------------------------------------------------ |
| scope | String \| undefined | Set the scope of message processing. Valid values:<br/><li>TIM.TYPES.READ_ALL_C2C_MSG: set the unread messages of all the one-to-one conversations as read</li><li>TIM.TYPES.READ_ALL_GROUP_MSG: set the unread messages of all the group conversations as read</li><li>TIM.TYPES.READ_ALL_MSG (default value): set the unread messages of all the one-to-one and group conversations as read</li> |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Set the unread messages of all the conversations as read
let promise = tim.setAllMessageRead(); // Same as `tim.setAllMessageRead({scope: TIM.TYPES.READ_ALL_MSG})`
promise.then(function(imResponse) {
  // Set the unread messages as read successfully. The values of the `unreadCount` attribute of all the conversations are set to `0`.
}).catch(function(imError) {
  // Failed to set the unread messages as read
  console.warn('setAllMessageRead error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Set the unread messages of all the one-to-one conversations as read
let promise = tim.setAllMessageRead({scope: TIM.TYPES.READ_ALL_C2C_MSG});
promise.then(function(imResponse) {
  // Set the unread messages as read successfully. The values of the `unreadCount` attribute of all the one-to-one conversations are set to `0`.
}).catch(function(imError) {
  // Failed to set the unread messages as read
  console.warn('setAllMessageRead error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Set the unread messages of all the group conversations as read
let promise = tim.setAllMessageRead({scope: TIM.TYPES.READ_ALL_GROUP_MSG});
promise.then(function(imResponse) {
  // Set the unread messages as read successfully. The values of the `unreadCount` attribute of all the one-to-one conversations are set to `0`.
}).catch(function(imError) {
  // Failed to set the unread messages as read
  console.warn('setAllMessageRead error:', imError);
});

:::
</dx-codeblock>

## Sending a Message Excluded from the Conversation Unread Count

In normal cases, both one-to-one messages and group messages that are sent will be included in the unread count. The `unreadCount` attribute of the `Conversation` object indicates the unread message count of a conversation.
If you want to send messages that will not be included in the unread count, such as tips or control messages, you can refer to the following code sample:

**Sample**

<dx-codeblock>
:::  js

// The message control option is supported by v2.16.0 or later.
tim.sendMessage(message, {
  messageControlInfo: {
    excludedFromUnreadCount: true, // `unreadCount` of the conversation is not updated (the message is stored on the roaming server).
    excludedFromLastMessage: true // `lastMessage` of the conversation is not updated (the message is stored on the roaming server).
  }
});

:::
</dx-codeblock>
