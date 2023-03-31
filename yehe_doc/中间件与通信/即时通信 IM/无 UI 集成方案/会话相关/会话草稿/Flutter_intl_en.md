## Feature Description
When sending a message, the user may want to switch to another chat window before finishing the message. The unfinished message can be saved through the `setConversationDraft` API, so that the user can get back to it through the `draftText` field of the `V2TIMConversation` object and finish it.

>! 
>1. A draft can contain only text.
>2. A draft will be stored only in the local database and not on the server. Therefore, it cannot be synced across devices and will not be available after the application is uninstalled and reinstalled.

## Setting a Conversation Draft
Call the `setConversationDraft` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/setConversationDraft.html)) to set a conversation draft.
If the `draftText` parameter of this API is empty, the draft is canceled.

Sample code:


```dart
conversationManager.setConversationDraft(conversationID: "conversationID",draftText: "Draft");
```
