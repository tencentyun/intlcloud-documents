## Feature Description

After a message is deleted successfully, its `isDeleted` is `true`. In one-to-one conversations, deleted messages cannot be pulled on the next login, but the receiver will not be affected. In group conversations, deleted messages cannot be pulled on the next login, but other group members will not be affected.

>!
>- This API is supported by v2.12.0 or later.
>- Up to 30 messages can be deleted at a time. If more than 30 messages are selected, the first 30 messages will be deleted.
>- Messages to be deleted must be from the same conversation, that is, the conversation of the first message in the message list.
>- This API can be called only once per second.
>- Deleted messages are not synced.
>- Messages cannot be deleted from audio-video groups (AVChatRoom), and if you call this API, the error code 10035 will be returned.

**API**

<dx-codeblock>
:::  js

tim.deleteMessage(messageList);

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

// Delete the messages (supported by v2.12.0 or later)
let promise = tim.deleteMessage([message1, message2, message3, ...]);
promise.then(function(imResponse) {
  // Messages deleted successfully
}).catch(function(imError) {
  // Failed to delete the messages
  console.warn('deleteMessage error:', imError);
});

:::
</dx-codeblock>