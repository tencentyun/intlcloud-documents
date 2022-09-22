## Feature Description
After a user deletes a friend or leaves a group, the SDK will not automatically delete the corresponding one-to-one or group conversation. The user can call the following API to delete the conversation.
> ! When a conversation is deleted, the historical messages will be deleted from both the client and the server and cannot be recovered.

Multi-client sync is not supported for conversation deletion by default and can be enabled in the [IM console](https://console.cloud.tencent.com/im-detail/login-message).
<img src="https://qcloudimg.tencent-cloud.cn/raw/c872395299ea796824453808f5a1c781.png" alt="" style="zoom:90%;" />

> ? Multi-client sync for conversation deletion is supported only by the SDK on v5.1.1 or later.

## Deleting a Conversation
Call the `deleteConversation` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a142f5289632f29a603937f1d770748c6)) to delete a specified conversation.

Sample code:
<dx-tabs>
::: Android
```java
String conversationID = "conversationID";
V2TIMManager.getConversationManager().deleteConversation(conversationID,  new V2TIMCallback() {
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
NSString *conversationID = @"conversationID";
[[V2TIMManager sharedInstance] deleteConversation:conversationID succ:^{
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
</dx-tabs>


