## Feature Description

You can set the message receiving option for a **one-to-one or group chat** to implement the notification muting feature.

The IM SDK supports the following three message receiving options:

| Message Receiving Option                                     | Feature Description                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TIM.TYPES.MSG_REMIND_ACPT_AND_NOTE](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_REMIND_ACPT_AND_NOTE) | Messages will be received when the user is online, and offline push notifications will be received when the user is offline. |
| [TIM.TYPES.MSG_REMIND_ACPT_NOT_NOTE](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_REMIND_ACPT_NOT_NOTE) | The SDK receives a message and notifies you (by reporting the message receiving event), and you display no notification. This option is usually used to implement message notification muting. |
| [TIM.TYPES.MSG_REMIND_DISCARD](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_REMIND_DISCARD) | The SDK rejects a message.                                   |


## Setting the Conversation Message Notification Type

>!
>- Group members can set the message notification type for their group.
>- Starting from v2.16.0, the message notification type can be set for a one-to-one conversation.
>- If the message notification type is set to mute message notifications, messages will be received when the user is online and will not be received when the user is offline (with offline push supported).
>- If the message notification type is set to reject messages, no messages will be received no matter whether the user is online or offline, and messages sent by the sender can be obtained through [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList).
>- Starting from v2.19.1, this API can be used to set the message notification type for a community topic by passing in `topicID` for `groupID`, and this setting will be ignored if `TIM.TYPES.MSG_REMIND_DISCARD` is set for the community of the topic.
>- Since v2.21.0, multi-terminal and multi-instance synchronization of group session messages and topic messages is supported. 

**API**

<dx-codeblock>
:::  js

tim.setMessageRemindType(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name              | Type   | Description                                                  |
| ----------------- | ------ | ------------------------------------------------------------ |
| groupID           | String | Group ID or topic ID                                         |
| userIDList        | Array  | List of `userID` values of the receivers of the one-to-one conversation. The number of `userID` values cannot exceed 30 per request. |
| messageRemindType | String | Group message notification type. Valid values:<br/><li>TIM.TYPES.MSG_REMIND_ACPT_AND_NOTE (The SDK receives messages and notifies the receiver (by reporting the message receiving event), and a notification is displayed for the receiver.)</li><li>TIM.TYPES.MSG_REMIND_ACPT_NOT_NOTE (The SDK receives messages and notifies the receiver (by reporting the message receiving event), and no notification is displayed. This option is usually used to implement message notification muting.)</li><li>TIM.TYPES.MSG_REMIND_DISCARD (The SDK rejects messages.)</li> |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Set to reject group messages (The `getMessageList` API can be called to pull messages sent by other group members)
let promise = tim.setMessageRemindType({ groupID: 'group1', messageRemindType: TIM.TYPES.MSG_REMIND_DISCARD });
promise.then(function(imResponse) {
  // The SDK triggers the `TIM.EVENT.CONVERSATION_LIST_UPDATED` event (after traversing the list and reading `Conversation.messageRemindType`).
}).catch(function(imError) {
  console.warn('setMessageRemindType error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Set to reject group messages (The `getMessageList` API can be called to pull messages sent by other group members)
let promise = tim.setMessageRemindType({ groupID: 'group1', messageRemindType: TIM.TYPES.MSG_REMIND_DISCARD });
promise.then(function(imResponse) {
  // The SDK triggers the `TIM.EVENT.CONVERSATION_LIST_UPDATED` event (after traversing the list and reading `Conversation.messageRemindType`).
}).catch(function(imError) {
  console.warn('setMessageRemindType error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Enable message notifications after setting to reject group messages
let promise = tim.setMessageRemindType({ groupID: 'group1', messageRemindType: TIM.TYPES.MSG_REMIND_ACPT_AND_NOTE });
promise.then(function(imResponse) {
  // The SDK triggers the `TIM.EVENT.CONVERSATION_LIST_UPDATED` event (after traversing the list and reading `Conversation.messageRemindType`).
}).catch(function(imError) {
  console.warn('setMessageRemindType error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// If the message notification type for a one-to-one conversation is set to mute message notifications, messages will be received when the user is online and will not be received when the user is offline (with offline push supported). This option is supported by v2.16.0 or later.
let promise = tim.setMessageRemindType({ userIDList: ['user1', 'user2'], messageRemindType: TIM.TYPES.MSG_REMIND_ACPT_NOT_NOTE });
promise.then(function(imResponse) {
  // The SDK triggers the `TIM.EVENT.CONVERSATION_LIST_UPDATED` event (after traversing the list and reading `Conversation.messageRemindType`).
  const { successUserIDList, failureUserIDList } = imResponse.data;
  // List of successfully deleted `userID` values
  successUserIDList.forEach((item) => {
    const { userID } = item;
  });
  // List of `userID` values failed to be deleted
  failureUserIDList.forEach((item) => {
    const { userID, code, message } = item;
  });
}).catch(function(imError) {
  console.warn('setMessageRemindType error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// If the message notification type for a group chat is set to mute message notifications, messages will be received when the user is online and will not be received when the user is offline (with offline push supported).
let promise = tim.setMessageRemindType({ groupID: 'group1', messageRemindType: TIM.TYPES.MSG_REMIND_ACPT_NOT_NOTE });
promise.then(function(imResponse) {
  // Message notification muting set successfully
}).catch(function(imError) {
  // Failed to set message notification muting
  console.warn('setMessageRemindType error:', imError);
});

:::
</dx-codeblock>


<dx-codeblock>
:::  js

// If the message notification type for a community topic is set to mute message notifications, messages will be received when the user is online and will not be received when the user is offline (with offline push supported).
let promise = tim.setMessageRemindType({ groupID: 'topicID', messageRemindType: TIM.TYPES.MSG_REMIND_ACPT_NOT_NOTE });
promise.then(function(imResponse) {
  // Message notification muting set successfully
}).catch(function(imError) {
  // Failed to set message notification muting
  console.warn('setMessageRemindType error:', imError);
});

:::
</dx-codeblock>
