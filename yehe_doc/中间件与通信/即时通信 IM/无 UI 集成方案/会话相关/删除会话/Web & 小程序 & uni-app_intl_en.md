## Feature Description

If a user doesn't want to view the historical one-to-one or group messages after deleting a friend or leaving a group, the user can choose to delete the conversation. Multi-client sync is disabled for conversation deletion by default and can be enabled in the [IM console](https://console.cloud.tencent.com/im-detail/login-message).

## Deleting a Conversation

>!
>- Starting from v2.16.1, the historical messages will be deleted after a conversation is deleted.
>- On versions earlier than v2.16.1, the historical messages will not be deleted after a conversation is deleted. For example, if the conversation with user A is deleted, the historical messages are still retained when a new conversation with user A is started.
>- Multi-client sync is disabled for conversation deletion by default. To enable it, log in to the [IM console](https://console.cloud.tencent.com/im-detail/login-message), select **Application Configuration** > **Feature Configuration** > **Login and Message** > **Multi-client Synchronization Settings**, and enable **Sync Conversation Deletion Across Clients**.

**API**

<dx-codeblock>
:::  js

tim.deleteConversation(conversationID);

:::
</dx-codeblock>

**Parameter**

| Name           | Type   | Description                                                  |
| -------------- | ------ | ------------------------------------------------------------ |
| conversationID | String | Conversation ID. Valid values:<br/><li>C2C${userID} (for a one-to-one chat)</li><li>GROUP{groupID} (for a group chat)</li><li>@TIM#SYSTEM (for a system notification conversation)</li> |


**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.deleteConversation('C2CExample');
promise.then(function(imResponse) {
  // Deleted the conversation successfully
  const { conversationID } = imResponse.data;// ID of the deleted conversation
}).catch(function(imError) {
  console.warn('deleteConversation error:', imError); // Failed to delete the conversation
});

:::
</dx-codeblock>
