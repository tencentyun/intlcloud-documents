## Feature Description
One-to-one messages and group messages can be cleared.
When messages in a conversation are cleared, all the messages in the conversation will be cleared both **locally and from the cloud**, but the conversation itself will not be deleted.

> ?
> - **Do not** use this API if you do not want to clear messages from the cloud.
> - This API is supported by v5.4.666 or later.

After messages are cleared, the `lastMessage` in the conversation will become empty, and:
* If your SDK version is earlier than v5.5.892 and the `lastMessage` is used for sorting, the sequence in the conversation list will be affected.
* If your SDK is on v5.5.892 or later and `orderKey` is used for sorting, the sequence in the conversation list will not be affected.
For more information, see [Conversation List](https://intl.cloud.tencent.com/document/product/1047/48326).

### Clearing one-to-one messages

Call `clearC2CHistoryMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a29aa6e75c2238c35cc609bef0e5a46ce) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a005c7767172d9a3980974b68c780c33b)) to clear one-to-one messages.


Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().clearC2CHistoryMessage(userID, new V2TIMCallback() {
	@Override
	public void onSuccess() {
		// One-to-one messages cleared successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to clear one-to-one messages
	}
});
```
:::
::: iOS and macOS
```objectivec
[V2TIMManager.sharedInstance clearC2CHistoryMessage:userID
                                               succ:^{
    NSLog(@"One-to-one messages cleared successfully");
} fail:^(int code, NSString *desc) {
    NSLog(@"Failed to clear one-to-one messages, code: %d, desc: %@", code, desc);
}];
```
:::
</dx-tabs>


### Clearing group messages

Call `clearGroupHistoryMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6e1a1dce441243d0bd5ac2f8bcecb3d9) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a16c01c19a285e2bd11443c868c8256e6)) to clear group messages.


Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().clearGroupHistoryMessage(GroupID, new V2TIMCallback() {
	@Override
	public void onSuccess() {
		// Group messages cleared successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to clear group messages
	}
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] clearGroupHistoryMessage:groupID
                                                   succ:^{
    NSLog(@"Group messages cleared successfully");
} fail:^(int code, NSString *desc) {
    NSLog(@"Failed to clear group messages, code: %d, desc: %@", code, desc);
}];
```
:::
</dx-tabs>


