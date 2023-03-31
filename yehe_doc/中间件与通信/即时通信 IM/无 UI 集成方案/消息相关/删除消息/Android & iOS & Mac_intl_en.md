## Feature Description
Both local messages and cloud messages can be deleted.
When cloud messages are deleted, such messages will be deleted both locally and from the cloud and **cannot be recovered**.

If the last message is deleted, the `lastMessage` in the conversation will become the last but one message.
* If your SDK version is earlier than v5.5.892 and the `lastMessage` is used for sorting, the sequence in the conversation list will be affected.
* If your SDK is on v5.5.892 or later and `orderKey` is used for sorting, the sequence in the conversation list will not be affected.


### Deleting a local message

Call `deleteMessageFromLocalStorage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa31e3b48fb666b970120fc0bc6343534) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c)) to delete a local message.

> ?
> 1. This API can only be used to delete a historical local message. After deleted, the message will be marked as deleted locally by the SDK and cannot be pulled through `getHistoryMessage`.
> 2. If the application is uninstalled and reinstalled, the delete marker will be lost locally, and the message can still be pulled through `getHistoryMessage`.

Sample code:
<dx-tabs>
::: Android
```java
// `selectedMsg` is the selected message to be deleted.
V2TIMManager.getMessageManager().deleteMessageFromLocalStorage(selectedMsg, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Local message deleted successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to delete the local message
  }
});
```
:::
::: iOS and macOS 
```objectivec
// `selectedMsg` is the selected message to be deleted.
[[V2TIMManager sharedInstance] deleteMessageFromLocalStorage:selectedMessage
                                                        succ:^{
    NSLog(@"Local message deleted successfully");
} fail:^(int code, NSString *msg) {
    NSLog(@"Failed to delete the local message, code: %d, desc: %@", code, msg);
}];
```
:::
</dx-tabs>


### Deleting a message from the cloud

Call `deleteMessages` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adb346fede13d493e415f6574df911e9a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e394ea720ecdc10d497b63b6f2b22c4)) to delete messages from the cloud.

This API deletes messages both locally and from the cloud, which cannot be recovered.

> ?
> 1. Up to 30 messages can be deleted per call.
> 2. Messages to be deleted per call **must** be from the same conversation.
> 3. This API can be called only once per second.
> 4. If messages have been pulled on a device by an account, they will remain on the device after the API is called to delete them from the cloud; in other words, deleted messages are not synced.

Sample code:
<dx-tabs>
::: Android
```java
// `selectedMessageList` is the list of selected messages to be deleted.
V2TIMManager.getMessageManager().deleteMessages(selectedMessageList, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Messages deleted from the cloud successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to delete the messages from the cloud
  }
});
```
:::
::: iOS and macOS
```objectivec
// `selectedMessageList` is the list of selected messages to be deleted.
NSArray *selectedMessageList = @[selectedMessage1, selectedMessage2];
[[V2TIMManager sharedInstance] deleteMessages:selectedMessageList
                                        succ:^{
    NSLog(@"Messages deleted from the cloud successfully");
} fail:^(int code, NSString *desc) {
    NSLog(@"Failed to delete the messages from the cloud, code: %d, desc: %@", code, desc);
}];
```
:::
</dx-tabs>
