## Feature Description
In certain cases, you might want a message to be received by the receiver only when online; that is, the receiver won't notice the message when offline.
You only need to set `onlineUserOnly` to `true/YES` when calling `sendMessage`. A message sent in this way differs from a general one in that:

1. It cannot be stored offline; that is, it cannot be received if the receiver is offline.
2. It cannot be roamed across devices; that is, if it is received on a device, it cannot be received on another, whether it is read or not.
3. It cannot be stored locally; that is, it cannot be pulled from local or cloud historical messages.

## Sample

### Implementing the feature of "The other party is typing..."

In one-to-one chats, you can use `sendMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send a specified custom online message. After receiving the specified custom online message and determining that the sender is typing, the receiver can display "The other party is typing..." on the UI.

Sample code:
<dx-tabs>
::: Android
```java
// Send the prompt "Typing…" to user A
JSONObject jsonObject = new JSONObject();
try {
	jsonObject.put("command", "textInput");
} catch (JSONException e) {
	e.printStackTrace();
}
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createCustomMessage(jsonObject.toString().getBytes());
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "userA", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, true,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onError(int code, String desc) {}
	@Override
	public void onSuccess(V2TIMMessage v2TIMMessage) {}
	@Override
	public void onProgress(int progress) {}
});
```
:::
::: iOS and macOS
```objectivec
// Send the prompt "Typing..." to user A
NSString *customStr = @"{\"command\": \"textInput\"}";
NSData *customData = [customStr dataUsingEncoding:NSUTF8StringEncoding];
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createCustomMessage:customData];
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:YES offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // Message sent successfully
} fail:^(int code, NSString *msg) {
    // Failed to send the message
}];
```
:::
</dx-tabs>


