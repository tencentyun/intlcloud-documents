## Feature Description
In some cases, you may need to mark a conversation, for example, as "favorite", "collapsed", "hidden", or "unread", which can be implemented through the following API.
> ?
- To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8).
- This feature is supported only by the SDK of the Enhanced edition on v6.5.2803 or later.

## Conversation Mark

### Marking a conversation
Call the `markConversation` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#aa1dab66f08df9aef4acb0aad8cb77d72) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a77c02a146f774979e1e04d7334cd2d06)) to mark or unmark a conversation.
> ! When a user marks a conversation, the SDK records only the mark value and will not change the underlying logic of the conversation. For example, if a conversation is marked as `V2TIM_CONVERSATION_MARK_TYPE_UNREAD`, the unread count at the underlying layer will not change.

Parameters of the API for marking a conversation are as described below:

| Attribute | Definition | Description  |
| --- |  --- | --- |
| conversationIDList | List of conversation IDs | Up to 100 conversations can be marked at a time. |
| markType | Mark type| A conversation can be marked as a favorite, unread, collapsed, or hidden.|
| enableMark | Mark/Unmark | A conversation can be marked/unmarked. |

> ? The SDK provides four default marks ("favorite", "collapsed", "hidden", and "unread"). If they cannot meet your requirements, you can customize extended marks, which must meet the following conditions:
1. The value of an extended mark cannot be the same as that of an existing one.
2. The value of an extended mark must be 0x1LL << displacement value of n (`32 ≤ n < 64` indicates that `n` must be equal to or greater than 32 and less than 64). For example, `0x1LL << 32` indicates "Online on an iPhone".

Sample code:
<dx-tabs>
::: Android
```java
List<String> conversationIDList = new ArrayList<>();
conversationIDList.add("c2c_user1");
// Mark type
long markType = V2TIMConversation.V2TIM_CONVERSATION_MARK_TYPE_STAR;
// Extended mark type
// long markType = 0x1L << 32;
V2TIMManager.getConversationManager().markConversation(conversationIDList, markType, true, new V2TIMValueCallback<List<V2TIMConversationOperationResult>>() {
    @Override
    public void onSuccess(List<V2TIMConversationOperationResult> v2TIMConversationOperationResults) {
        // Marked the conversation successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to mark the conversation
    }
});
```
:::
::: iOS and macOS
```objectivec
// Mark type
NSNumber *markType = @(V2TIM_CONVERSATION_MARK_TYPE_STAR);
// Extended mark type
// NSNumber *markType = @(0x1LL << 32);
// Mark a conversation
BOOL enableMark = YES; 
// Unmark a conversation
//  BOOL enableMark = NO; 
[[V2TIMManager sharedInstance] markConversation:@[@"c2c_yahaha"] markType:markType enableMark:enableMark succ:^(NSArray<V2TIMConversationOperationResult *> *result){
    // Marked the conversation successfully
} fail:^(int code, NSString *desc) {
    // Failed to mark the conversation
}];
```
:::
</dx-tabs>

### Listening for the notification of a conversation mark change
After a conversation is marked or unmarked, the `markList` field ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#af8ed1769cee83f972be1727d35e10eb6) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a1778161ca64b919acb1a10c8520538e6)) in `V2TIMConversation` of the conversation will change. You can call the `addConversationListener` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9)) to listen for such a change notification.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMConversationListener listener = new V2TIMConversationListener() {
    @Override
    public void onConversationChanged(List<V2TIMConversation> conversationList) {
        for (V2TIMConversation conversation : conversationList) {
            // Get the new mark information of the conversation
            List<Long> markList = conversation.getMarkList();
        }
    }
};
V2TIMManager.getConversationManager().addConversationListener(listener);
```
:::
::: iOS and macOS
```objectivec
// Delete the conversation group
[[V2TIMManager sharedInstance] addConversationListener:self];
- (void)onConversationChanged:(NSArray<V2TIMConversation*> *) conversationList
{
    for (V2TIMConversation *conv in conversationList) {
        // Get the new mark information of the conversation
        NSArray *mark_list = conv.markList;
    }
}
```
:::
</dx-tabs>


### Pulling a specified marked conversation
Call the `getConversationListByFilter` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9)) to pull a specified marked conversation.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMConversationListFilter filter = new V2TIMConversationListFilter();
filter.setMarkType(V2TIMConversation.V2TIM_CONVERSATION_MARK_TYPE_STAR);
filter.setCount(50);
filter.setNextSeq(0);
V2TIMManager.getConversationManager().getConversationListByFilter(filter, new V2TIMValueCallback<V2TIMConversationResult>() {
    @Override
    public void onSuccess(V2TIMConversationResult v2TIMConversationResult) {
        // Obtained the conversation list successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to obtain the conversation list
    }
});
```
:::
::: iOS and macOS
```objectivec
// Pull a specified marked conversation
V2TIMConversationListFilter *filter = [[V2TIMConversationListFilter alloc] init];
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;
filter.count = 50;
filter.nextSeq = 0;
[[V2TIMManager sharedInstance] getConversationListByFilter:filter succ:^(NSArray<V2TIMConversation *> *list, uint64_t nextSeq, BOOL isFinished) {
   // Obtained the conversation list successfully. `list` is the conversation list.
} fail:^(int code, NSString *desc) {
   // Failed to obtain the conversation list
}];
```
:::
</dx-tabs>


