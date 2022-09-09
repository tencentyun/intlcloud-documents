## Feature Description
You can call `findMessages` to query a local message based on the `messageID`. Note that:
1. Only local messages can be queried, for example, received messages or historical messages pulled by API.
2. Audio-video group (AVChatRoom) messages cannot be queried, as they are not saved locally.

## Querying a Local Message
Call the `findMessages` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dbaec04bc389d01f815f46c550e2fd) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a4a0c47d706d8784656225c1e9065f6f1)) to query a local message.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().findMessages(messageIDList, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {}

    @Override
    public void onError(int code, String desc) {}
});
```
:::
::: iOS and macOS
```objectivec
[V2TIMManager.sharedInstance findMessages:messageIDList
                                        succ:^(NSArray<V2TIMMessage *> *msgs) {
    // Messages queried successfully
} fail:^(int code, NSString *desc) {
    // Failed to query the messages
}];
```
:::
</dx-tabs>


