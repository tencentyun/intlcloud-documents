## Feature Description
The sender can recall a successfully sent message.

By default, the sender can recall a message sent within two minutes. You can change the time limit for message recall as instructed in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

Message recall can be implemented through the receiver UI code: When a message is recalled, the receiver will receive the `onRecvMessageRevoked` notification which contains the `msgID` of the recalled message. You can identify the recalled message at the UI layer based on the `msgID` and change the bubble for the message to the "Message recalled" status.

## Recalling a Message (by the Sender)
The sender can call `revokeMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a972ac3fb7744458eb0d6abd96ce35126)) to recall a message.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().revokeMessage(v2TIMMessage, new V2TIMCallback() {
	@Override
	public void onError(int code, String desc) {
		// Failed to recall the message
	}
	@Override
	public void onSuccess() {
		// Message recalled successfully
	}
});
```
:::
::: iOS and macOS
```objectivec
// `selectedMessage` is the message to be recalled.
[[V2TIMManager sharedInstance] revokeMessage:selectedMessage
										succ:^{
	// Message recalled successfully
} fail:^(int code, NSString *msg) {
	// Failed to recall the message
}];
```
:::
</dx-tabs>

## Noticing a Message Recall (by the Receiver)
1. The receiver calls `addAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab)) to set the advanced message listener.
2. The receiver receives the message recall notification in `onRecvMessageRevoked` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a13d8197eaba83bfadc7a2f695d671272) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html)).

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().addAdvancedMsgListener(new V2TIMAdvancedMsgListener() {
	@Override
	public void onRecvMessageRevoked(String msgID) {
		// `msgList` is the list of messages on the current chat UI.
		for (V2TIMMessage msg : msgList) {
			if (msg.getMsgID().equals(msgID)) {
				// `msg` is the recalled message. You need to change the bubble status for the message on the UI.
			}
		}
	}
}
```
:::
::: iOS and macOS
```objectivec
// V2TIMAdvancedMsgListener
- (void)onRecvMessageRevoked:(NSString *)msgID {
	// You need to modify the bubble status for the message on the UI after receiving the message recall notification.
}
```
:::
</dx-tabs>

