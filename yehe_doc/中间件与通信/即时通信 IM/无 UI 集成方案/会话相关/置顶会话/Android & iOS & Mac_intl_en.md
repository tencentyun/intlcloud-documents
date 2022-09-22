## Feature Description
Pinning a conversation to the top is to fix a one-to-one or group conversation at the top of the conversation list to facilitate search. A conversation pinned to the top will not be displayed under another conversation with a update. The status of a conversation being pinned to the top will be stored on the server and synced to new devices.

>? This feature is supported only by the SDK of the Enhanced edition on v5.3.425 or later.

## Pinning a Conversation to the Top
Call the `pinConversation` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a4da7467f54c891c4929152260e42f4b6) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a06cefb398f5a327dff4cefe6fb18c5b8)) to set whether to pin a conversation to the top.

When `getConversationList` is called to get the conversation list, it will first return the conversation that is pinned to the top and then other conversations. You can check whether a conversation is pinned to the top through the `isPinned` field of the `V2TIMConversation` object.

The conversations are sorted based on the `orderKey` field of the `V2TIMConversation` object. This field is an integer that increases as the conversation is activated when a message is sent/received, a draft is set, or the conversation is pinned to the top.

A conversation pinned to the top will always be displayed above others. If multiple conversations are pinned to the top, they will be sorted in the original order.
For example, if there are five conversations (1, 2, 3, 4, and 5 in order) and conversations 2 and 3 are pinned to the top, the new order will be 2, 3, 1, 4, and 5. Obviously, conversations 2 and 3 are displayed above others, and conversation 2 is displayed above conversation 3.

Sample code:
<dx-tabs>
::: Android
```java
// If `isPinned` is `true`, the conversation is pinned to the top; otherwise, it is not.
String conversationID = "conversationID";
V2TIMManager.getConversationManager().pinConversation(conversationID, true, new V2TIMCallback() {
    @Override
    public void onSuccess() {
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
// If `isPinned` is `YES`, the conversation is pinned to the top; otherwise, it is not.
NSString *conversationID = @"conversationID";
[[V2TIMManager sharedInstance] pinConversation:conversationID isPinned:YES succ:^{
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
</dx-tabs>

## Notification of the Pinned Status Change
If you have called `addConversationListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9)) to add a conversation listener, you can get the `isPinned` value of the `V2TIMConversation` object in `onConversationChanged` and determine whether the pinned status of a conversation has changed.

Sample code:
<dx-tabs>
::: Android
```java
public void onConversationChanged(List<V2TIMConversation> conversationList) {
    // Received the notification of a change in the conversation information
    Log.i("imsdk", "onConversationChanged");
}
```
:::
::: iOS and macOS
```objectivec
- (void)onConversationChanged:(NSArray<V2TIMConversation*> *) conversationList {
    for (V2TIMConversation *conv in conversationList) {
        if ([conv.conversationID isEqualToString:self.conversationData.conversationID]) {
            // `conv.isPinned` is the pinned status.
        }
    }
}
```
:::
</dx-tabs>


