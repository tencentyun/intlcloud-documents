## Feature Description
The IM SDK provides an API for getting conversations, which can be used to get the `V2TIMConversation` object information of one or multiple specified conversations.

### Getting a specified conversation
Call `getConversation` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a619aaff2bb5664e094d2341819b95096) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ad4b7b80fbe0cff25027371b416ede9f9)) to get the information of a conversation, which is a `V2TIMConversation` object.

Sample code:
<dx-tabs>
::: Android

```java
String conversationID = "conversationID";
V2TIMManager.getConversationManager().getConversation(conversationID, new V2TIMValueCallback<V2TIMConversation>() {
    @Override
    public void onSuccess(V2TIMConversation v2TIMConversation) {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
[V2TIMManager.sharedInstance getConversation:@"conversationID" // ID of the conversation to be queried
                                        succ:^(V2TIMConversation *conv) {
    // The conversation obtained successfully. The `V2TIMConversation` object was returned.
} fail:^(int code, NSString *desc) {
    // Failed to obtain the conversation
}];
```
:::
</dx-tabs>

### Getting specified conversations

Call `getConversationList` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a41ebb09032a6bbda0a78e8734c61fb93) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ab1f5e86e270b122cb725266d234d9dd5)) to get the list of specified conversations that stores `V2TIMConversation` objects.

Sample code:
<dx-tabs>
::: Android
```java
List<String> conversationIDList = new ArrayList<>();
conversationIDList.add("conversationID1");
conversationIDList.add("conversationID1");

V2TIMManager.getConversationManager().getConversationList(conversationIDList, new V2TIMValueCallback<List<V2TIMConversation>>() {
    @Override
    public void onSuccess(List<V2TIMConversation> conversationList) {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
[V2TIMManager.sharedInstance getConversationList:@[@"convID1", @"convID2"] // List of IDs of the conversations to be queried
                                            succ:^(NSArray<V2TIMConversation *> *list) {
    // Conversations obtained successfully. The `list` contains `V2TIMConversation` objects.
} fail:^(int code, NSString *desc) {
    // Failed to obtain the conversations
}];
```
:::
</dx-tabs>


