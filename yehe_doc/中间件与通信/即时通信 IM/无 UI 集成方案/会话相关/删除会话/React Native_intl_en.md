## Feature Description

If a user don't want to view the historical one-to-one or group messages after deleting a friend or leaving a group, the user can choose to delete the conversation.

> ! When a conversation is deleted, the historical messages will be deleted from both the client and the server and cannot be recovered.

Multi-client sync is disabled for conversation deletion by default and can be enabled in the [IM console](https://console.cloud.tencent.com/im-detail/login-message).

## Deleting a Conversation

Call the `deleteConversation` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMConversationManager/deleteConversation.html)) to delete a specified conversation.

Below is the sample code:

```javascript
// Delete a specified conversation
conversationManager.deleteConversation("conversationID");
```
