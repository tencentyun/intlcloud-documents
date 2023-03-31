## Feature Description
* The method for sending a message is in the core classes `V2TIMManager` and `V2TIMMessageManager (Android)` / `V2TIMManager(Message) (iOS and macOS)`.
* It supports sending text, custom, and rich media messages, and all of which belong to the `V2TIMMessage` type.
* `V2TIMMessage` can contain `V2TIMElem` sub-types to indicate different types of messages.

## API Description
The `sendMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) is one of the core APIs for message sending. It supports sending messages of all types.

> ? The advanced message sending API mentioned below refers to `sendMessage`.

The API is as described below:

<dx-tabs>
::: Android
API prototype:
```java
// V2TIMMessageManager
public abstract String sendMessage(
	V2TIMMessage message,
	String receiver,
	String groupID,
	int priority,
	boolean onlineUserOnly,
	V2TIMOfflinePushInfo offlinePushInfo,
	V2TIMSendCallback<V2TIMMessage> callback);
```
Parameter description:
<table>
   <tr>
      <th width="0px" style="text-align:center">Parameter</td>
      <th width="0px" style="text-align:center">Definition</td>
      <th width="0px"  style="text-align:center">Valid for One-to-One Chat</td>
      <th width="0px"  style="text-align:center">Valid for Group Chat</td>
			<th width="0px"  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td>message</td>
      <td>Message object</td>
      <td>YES</td>
      <td>YES</td>
			<td>It needs to be created through the `createXxxMessage` API. Here, `Xxx` indicates the specific type.</td>
   </tr>
   <tr>
      <td>receiver</td>
      <td>`userID` of the one-to-one message receiver</td>
      <td>YES</td>
      <td><b>NO</td>
			<td>Just specify `receiver` for sending one-to-one chat messages.</td>
   </tr>
	 <tr>
      <td>groupID</td>
      <td>`groupID` of the group chat</td>
      <td><b>NO</td>
      <td>YES</td>
			<td>Just specify `groupID` for sending group messages.</td>
   </tr>
	 <tr>
      <td>priority</td>
      <td>Message priority</td>
      <td><b>NO</td>
      <td>YES</td>
			<td>Set a higher priority for important messages (such as red packets and gifts) and a lower priority for frequent and unimportant messages (such as likes).</td>
   </tr>
	 <tr>
      <td>onlineUserOnly</td>
      <td>Whether the message can be received by online users only</td>
      <td>YES</td>
      <td>YES</td>
	    <td>If it is set to `true`, the message cannot be pulled when a receiver pulls historical messages. This is often used to implement weak prompts, such as "The other party is typing..." and unimportant prompts in a group.</td>
   </tr>
	 <tr>
      <td>offlinePushInfo</td>
      <td>Offline push message</td>
      <td>YES</td>
      <td>YES</td>
	    <td>The title and content carried when a message is pushed offline.</td>
   </tr>
	 <tr>
      <td>callback</td>
      <td>Callback for message sending</td>
      <td>YES</td>
      <td>YES</td>
	    <td>Includes the callback for upload progress, callback for successful sending, and callback for failed sending.</td>
   </tr>
</table>
:::

::: iOS and macOS
Method prototype:
```objectivec
// V2TIMManager+Message.h
- (NSString *)sendMessage:(V2TIMMessage *)message
                 receiver:(NSString *)receiver
                  groupID:(NSString *)groupID
                 priority:(V2TIMMessagePriority)priority
           onlineUserOnly:(BOOL)onlineUserOnly
          offlinePushInfo:(V2TIMOfflinePushInfo *)offlinePushInfo
                 progress:(V2TIMProgress)progress
                     succ:(V2TIMSucc)succ
                     fail:(V2TIMFail)fail;
```
Parameter description:
<table>
   <tr>
      <th width="0px" style="text-align:center">Parameter</td>
      <th width="0px" style="text-align:center">Definition</td>
      <th width="0px"  style="text-align:center">Valid for One-to-One Chat</td>
      <th width="0px"  style="text-align:center">Valid for Group Chat</td>
			<th width="0px"  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td>message</td>
      <td>Message object</td>
      <td>YES</td>
      <td>YES</td>
			<td>It needs to be created through the `createXxxMessage` API. Here, `Xxx` indicates the specific type.</td>
   </tr>
   <tr>
      <td>receiver</td>
      <td>`userID` of the one-to-one message receiver</td>
      <td>YES</td>
      <td><b>NO</td>
			<td>Just specify `receiver` for sending one-to-one messages.</td>
   </tr>
	 <tr>
      <td>groupID</td>
      <td>`groupID` of the group chat</td>
      <td><b>NO</td>
      <td>YES</td>
			<td>Just specify `groupID` for sending group messages.</td>
   </tr>
	 <tr>
      <td>priority</td>
      <td>Message priority</td>
      <td><b>NO</td>
      <td>YES</td>
			<td>Set a higher priority for important messages (such as red packets and gifts) and a lower priority for frequent and unimportant messages (such as likes).</td>
   </tr>
	 <tr>
      <td>onlineUserOnly</td>
      <td>Whether the message can be received by online users only</td>
      <td>YES</td>
      <td>YES</td>
	    <td>If it is set to `true`, the message cannot be pulled when a receiver pulls historical messages. This is often used to implement weak prompts, such as "The other party is typing..." and unimportant prompts in a group.</td>
   </tr>
	 <tr>
      <td>offlinePushInfo</td>
      <td>Offline push message</td>
      <td>YES</td>
      <td>YES</td>
	    <td>The title and content carried when a message is pushed offline.</td>
   </tr>
	<tr>
      <td>progress</td>
      <td>File upload progress</td>
      <td>YES</td>
      <td>YES</td>
	    <td>File upload progress. It applies to sending messages that contain rich media such as images, audios, videos, and files. There is no callback for pure text, emoji, and location messages.</td>
   </tr>
	 <tr>
      <td>succ</td>
      <td>Callback for successful message sending</td>
      <td>YES</td>
      <td>YES</td>
	    <td>-</td>
   </tr>
	 <tr>
      <td>fail</td>
      <td>Callback for failed message sending</td>
      <td>YES</td>
      <td>YES</td>
	    <td>Callback failure error code and error description.</td>
   </tr>
</table>
:::
</dx-tabs>

<dx-alert infotype="notice" title="">
If both `groupID` and `receiver` are set, targeted group messages are sent to `receiver`. For more information, see [Targeted Group Message](https://intl.cloud.tencent.com/document/product/1047/48029).
</dx-alert>


## Sending a Text Message
Text messages include one-to-one messages and group messages, which are different in terms of API and parameters.

The ordinary and advanced APIs can be used to send text messages. The latter supports more sending parameters (such as priority and offline push message).
The ordinary API is as described below, while the advanced API is `sendMessage` mentioned above.

### One-to-one text message

#### Ordinary API

Call the `sendC2CTextMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a59a8ba6e4a973b4c40a09ae7dfdc6981) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618)) to send a one-to-one text message simply by passing in the message content and receiver's `userID`.

Sample code:
<dx-tabs>
::: Android
```java
// `msgID` returned by the API for on-demand use
String msgID = V2TIMManager.getInstance().sendC2CTextMessage("One-to-one text message", "receiver_userID", new V2TIMValueCallback<V2TIMMessage>() {
	@Override
	public void onSuccess(V2TIMMessage message) {
		// The one-to-one text message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the one-to-one text message
	}
});
```
:::
::: iOS and macOS
```objectivec
// `msgID` returned by the API for on-demand use
NSString *msgID = [[V2TIMManager sharedInstance] sendC2CTextMessage:@"One-to-one text message" 
                                                                 to:@"receiver_userID"
                                                               succ:^{
    // The one-to-one text message sent successfully
} fail:^(int code, NSString *msg) {
    // Failed to send the one-to-one text message
}];
```
:::
</dx-tabs>


#### Advanced API

The advanced API can be called to send a one-to-one text message in two steps:
1. Call `createTextMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a3ea254cd12aa0bcfd004f26f759b76a0) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a609f4d4c374d9df3abf9974ff8112fc3)) to create a text message.
2. Call `sendMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send the message.

Sample code:
<dx-tabs>
::: Android
```java
// Create a text message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage("content");
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// The progress is not called back for the text message.
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The text message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the text message
	}
});
```
:::
::: iOS and macOS
```objectivec
// Create a text message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"content"];
// Send the message
[V2TIMManager.sharedInstance sendMessage:message
                                receiver:@"userID"
                                 groupID:nil
                                priority:V2TIM_PRIORITY_NORMAL
                          onlineUserOnly:NO
                         offlinePushInfo:nil
                                progress:nil
                                succ:^{
    // The text message sent successfully
}
                                fail:^(int code, NSString *desc) {
    // Failed to send the text message
}];
```
:::
</dx-tabs>



### Group text message

#### Ordinary API

Call `sendGroupTextMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7)) to send a group message simply by passing in the message content, `groupID` of the group chat, and message priority.

For message priorities, see the `V2TIMMessagePriority` definition.

Sample code:
<dx-tabs>
::: Android
```java
// `msgID` returned by the API for on-demand use
String msgID = V2TIMManager.getInstance().sendGroupTextMessage("Group text message", "groupID", V2TIMMessage.V2TIM_PRIORITY_NORMAL, new V2TIMValueCallback<V2TIMMessage>() {
	@Override
	public void onSuccess(V2TIMMessage message) {
		// The group text message sent successfully
	}
		
	@Override
	public void onError(int code, String desc) {
		// Failed to send the group text message
	}
});
```
:::
::: iOS and macOS
```objectivec
// `msgID` returned by the API for on-demand use
NSString *msgID = [[V2TIMManager sharedInstance] sendGroupTextMessage:@"Group text message" 
                                                                   to:@"groupID"  // `groupID` of the group chat
                                                             priority:V2TIM_PRIORITY_NORMAL // Message priority
                                                                 succ:^{
    // The group text message sent successfully
} fail:^(int code, NSString *msg) {
    // Failed to send the group text message
}];
```
:::
</dx-tabs>


#### Advanced API

The advanced API can be called to send a group text message in two steps:
1. Call `createTextMessage` ([Android]() / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a609f4d4c374d9df3abf9974ff8112fc3)) to create a text message.
2. Call `sendMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send the message.

Sample code:
<dx-tabs>
::: Android
```java
// Create a text message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage("content");
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, null, "receiver_groupID", V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// The progress is not called back for the text message.
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The group text message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the group text message
	}
});
```
:::
::: iOS and macOS
```objectivec
// Create a text message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:content];
// Send the message
[V2TIMManager.sharedInstance sendMessage:message
                                receiver:nil
                                 groupID:@"receiver_groupID"  // `groupID` of the group chat
                                priority:V2TIM_PRIORITY_NORMAL // Message priority
                          onlineUserOnly:NO   // For online users only
                         offlinePushInfo:nil  // Custom information for offline push
                                progress:nil
                                    succ:^{
    // The text message sent successfully
}
                                fail:^(int code, NSString *desc) {
    // Failed to send the text message
}];
```
:::
</dx-tabs>


## Sending a Custom Message

Custom messages include one-to-one messages and group messages, which are different in terms of APIs and parameters. The ordinary and advanced APIs can be used to send custom messages.
The advanced API is `sendMessage` mentioned above ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)), which supports more sending parameters (such as priority and offline push message) than the ordinary API.


### Custom one-to-one message

#### Ordinary API

Call `sendC2CCustomMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af3e08b936df77210c6cdd0ce5c7fa87f) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90)) to send a custom one-to-one message simply by passing in the binary content and receiver's `userID`.

Sample code:
<dx-tabs>
::: Android
```java

String msgID = V2TIMManager.getInstance().sendC2CCustomMessage("Custom one-to-one message".getBytes(), "receiver_userID", new V2TIMValueCallback<V2TIMMessage>() {
	@Override
	public void onSuccess(V2TIMMessage message) {
		// The custom one-to-one message sent successfully
	}
	
	@Override
	public void onError(int code, String desc) {
		// Failed to send the custom one-to-one message
	}
});
```
:::
::: iOS and macOS
```objectivec
NSData *customData = [@"Custom one-to-one message"  dataUsingEncoding:NSUTF8StringEncoding];
NSString *msgID = [[V2TIMManager sharedInstance] sendC2CCustomMessage:customData
                                                                   to:@"receiver_userID"  // Receiver's `userID`
                                                                 succ:^{
    // The custom one-to-one message sent successfully
} 
                                                                fail:^(int code, NSString *msg) {
    // Failed to send the custom one-to-one message
}];
```
:::
</dx-tabs>


#### Advanced API

The advanced API can be called to send a custom one-to-one message in two steps:
1. Call `createCustomMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5c2495d4b7ecd66e5636aeb865c17efd) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316)) to create a custom message.
2. Call `sendMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send the message.

Sample code:
<dx-tabs>
::: Android
```java
// Create a custom message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createCustomMessage("Custom one-to-one message".getBytes());
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// The progress is not called back for the custom message.
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The custom one-to-one message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the custom one-to-one message
	}
});
```
:::
::: iOS and macOS
```objectivec
V2TIMMessage *message = [[V2TIMManager sharedInstance] createCustomMessage:data];
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:@"receiver_userID"  // Receiver's `userID`
                                   groupID:nil
                                  priority:V2TIM_PRIORITY_DEFAULT  // Message priority
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:nil
                                      succ:^{
    // The custom one-to-one message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the custom one-to-one message
}];
```
:::
</dx-tabs>


### Custom group message

#### Ordinary API

Call `sendGroupCustomMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65)) to send a custom group message simply by passing in the binary content, `groupID` of the group chat, and priority.
For message priorities, see the `V2TIMMessagePriority` definition.

Sample code:
<dx-tabs>
::: Android
```java
String msgID = V2TIMManager.getInstance().sendGroupCustomMessage("Custom group message".getBytes(), "groupID", V2TIMMessage.V2TIM_PRIORITY_NORMAL, new V2TIMValueCallback<V2TIMMessage>() {
	@Override
	public void onSuccess(V2TIMMessage message) {
		// The custom group message sent successfully
	}
	
	@Override
	public void onError(int code, String desc) {
		// Failed to send the custom group message
	}
});
```
:::
::: iOS and macOS
```objectivec
NSData *customData = [@"Custom group message"  dataUsingEncoding:NSUTF8StringEncoding];
NSString *msgID = [[V2TIMManager sharedInstance] sendGroupCustomMessage:customData
                                                                     to:@"receiver_groupID"  // `groupID` of the group chat
                                                               priority:V2TIM_PRIORITY_HIGH  // Message priority
                                                                   succ:^{
    // The custom group message sent successfully
} fail:^(int code, NSString *msg) {
    // Failed to send the custom group message
}];
```
:::
</dx-tabs>


#### Advanced API

The advanced API can be called to send a custom group message in two steps:
1. Call `createCustomMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5c2495d4b7ecd66e5636aeb865c17efd) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316)) to create a custom message.
2. Call `sendMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send the message.

Sample code:
<dx-tabs>
::: Android
```java
// Create a custom message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createCustomMessage("Custom group message".getBytes());
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// The progress is not called back for the custom message.
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The custom group message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the custom group message
	}
});
```
:::
::: iOS and macOS
```objectivec
V2TIMMessage *message = [[V2TIMManager sharedInstance] createCustomMessage:data];
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:nil
                                   groupID:@"receiver_groupID"  // `groupID` of the group chat
                                  priority:V2TIM_PRIORITY_DEFAULT  // Message priority
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:nil
                                      succ:^{
    // The custom group message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the custom group message
}];
```
:::
</dx-tabs>



## Sending a Rich Media Message

A rich media message can be sent in the following steps:

1. Call `createXxxMessage` to create a rich media message object of a specified type. Here, `Xxx` indicates the specific message type.
2. Call `sendMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send the message.
3. Get the callback for message sending success or failure.

### Image message

To create an image message, you need to get the local image path first.
During message sending, the image is uploaded to the server, and the upload progress is called back. The message is sent after the image is uploaded successfully.

Sample code:
<dx-tabs>
::: Android
```java
// Create an image message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createImageMessage("/sdcard/xxx");
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// Image upload progress in the range of [0, 100]
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The image message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the image message
	}
});
```
:::
::: iOS and macOS
```objectivec
// Get the local image path
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
// Create an image message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createImageMessage:imagePath];
// Send the message
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:@"userID"
                                   groupID:nil
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:^(uint32_t progress) {
    // Image upload progress in the range of [0, 100]
} succ:^{
    // The image message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the image message
}];
```
:::
</dx-tabs>


### Audio message

To create an audio message, you need to get the local audio file path and audio duration first, the latter of which can be used for display on the receiver UI.
During message sending, the audio is uploaded to the server, and the upload progress is called back. The message is sent after the audio is uploaded successfully.

Sample code:
<dx-tabs>
::: Android
```java
// Create an audio message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createSoundMessage("/sdcard/xxx", 5);
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// Audio upload progress in the range of [0, 100]
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The audio message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the audio message
	}
});
```
:::
::: iOS and macOS
```objectivec
// Get the local audio file path
NSString *soundPath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"m4a"];
// Get the audio duration (which is only used for UI display)
AVURLAsset *asset = [AVURLAsset assetWithURL:[NSURL fileURLWithPath:soundPath]];
CMTime time = [asset duration];
int duration = ceil(time.value/time.timescale);
// Create an audio message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createSoundMessage:soundPath duration:duration];
// Send the message
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:@"userID"
                                   groupID:nil
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:^(uint32_t progress) {
    // Audio upload progress in the range of [0, 100]
} succ:^{
    // The audio message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the audio message
}];
```
:::
</dx-tabs>


### Video message

To create a video message, you need to get the local video file path, video duration, and video thumbnail first, the latter two of which can be used for display on the receiver UI.
During message sending, the video is uploaded to the server, and the upload progress is called back. The message is sent after the video is uploaded successfully.

Below is the sample code:
<dx-tabs>
::: Android
```java
// Create a video message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createVideoMessage("/sdcard/xxx", "mp4", 10, "/sdcard/xxx");
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// Video upload progress in the range of [0, 100]
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The video message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the video message
	}
});
```
:::
::: iOS and macOS
```objectivec
// Get the local video file path
NSString *videoPath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"mp4"];
// Get the local video thumbnail path
NSString *snapShotPath = [[NSBundle mainBundle] pathForResource:@"testpng" ofType:@""];
// Get the video duration
AVURLAsset *asset = [AVURLAsset assetWithURL:[NSURL fileURLWithPath:path]];
CMTime time = [asset duration];
int duration = ceil(time.value/time.timescale);
// Create a video message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createVideoMessage:videoPath  
                                                                     type:@"mp4" 
                                                                 duration:duration 
                                                             snapshotPath:snapShotPath];
// Send the message
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:@"userID"
                                   groupID:nil
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:^(uint32_t progress) {
    // Video upload progress in the range of [0, 100]
} succ:^{
    // The video message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the video message
}];
```
:::
</dx-tabs>


### File message

To create a file message, you need to get the local file path first.
During message sending, the file is uploaded to the server, and the upload progress is called back. The message is sent after the file is uploaded successfully.

Sample code:
<dx-tabs>
::: Android
```java
// Create a file message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createFileMessage("/sdcard/xxx", "Filename");
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// File upload progress in the range of [0, 100]
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The file message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the file message
	}
});
```
:::
::: iOS and macOS
```objectivec
// Get the local file path
NSString *filePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"mp4"];
// Create a file message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createFileMessage:filePath fileName:@"Send the file message"];
// Send the message
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:@"userID"
                                   groupID:nil
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:^(uint32_t progress) {
    // File upload progress in the range of [0, 100]
} succ:^{
    // The file message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the file message
}];
```
:::
</dx-tabs>


### Location message

Latitude and longitude information is sent in a location message, which requires a map control for display.

Sample code:
<dx-tabs>
::: Android
```java
// Create a location message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createLocationMessage("Geographical location", 0.5, 0.5);
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// The progress is not called back for the location message.
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The location message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the location message
	}
});
```
:::
::: iOS and macOS
```objectivec
// Create a location message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createLocationMessage:@"Send the geographical location message" longitude:0.5 latitude:0.5];
// Send the message
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:@"userID"
                                   groupID:nil
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:nil
                                      succ:^{
    // The location message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the location message
}];
```
:::
</dx-tabs>


### Emoji message

Emoji codes are sent in an emoji message and need to be converted into icons by the receiver.

Sample code:
<dx-tabs>
::: Android
```java
// Create an emoji message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createFaceMessage(1, "tt00".getBytes());
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// The progress is not called back for the emoji message.
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The emoji message sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the emoji message
	}
});
```
:::
::: iOS and macOS
```objectivec
// Create an emoji message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createFaceMessage:1 data:[@"tt00" dataUsingEncoding:NSUTF8StringEncoding]];
// Send the message
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:@"userID"
                                   groupID:nil
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:nil
                                      succ:^{
    // The emoji message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the emoji message
}];
```
:::
</dx-tabs>


## Sending a Message Containing Multiple Element Objects

To include multiple elements in a message, create a Message object and call the `appendElem` method ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMElem.html#a5f5d86bb659d7a3775829eaa2e102866) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMElem.html#a632f3740c4c42014dc38a4c074a700c9)) through the element members of the Message object to add another element member.
	
`appendElem` only supports adding `V2TIMTextElem`, `V2TIMCustomElem`, `V2TIMFaceElem`, and `V2TIMLocationElem` after the original `V2TIMElem` (which can be any type).
Therefore, "image + text", "video + text", and "location + text" are supported, but "image + image" and "text + image" are not supported.

Sample code for "text message + custom message":
<dx-tabs>
::: Android
```java
// Create a text message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage("test");
// Create a custom element
V2TIMCustomElem customElem = new V2TIMCustomElem();
customElem.setData("Custom message".getBytes());
// Add the custom element to `message.textElem`
v2TIMMessage.getTextElem().appendElem(customElem);
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onProgress(int progress) {
		// The progress is not called back.
	}

	@Override
	public void onSuccess(V2TIMMessage message) {
		// The message containing multiple elements sent successfully
	}

	@Override
	public void onError(int code, String desc) {
		// Failed to send the message containing multiple element objects
	}
});
```
:::
::: iOS and macOS
```objectivec
// Create a text message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"text"];

// Create a custom element
V2TIMCustomElem *customElem = [[V2TIMCustomElem alloc] init];
customElem.data = [@"Custom message" dataUsingEncoding:NSUTF8StringEncoding];

// Add the custom element to `message.textElem`
[message.textElem appendElem:customElem];

// Send the message
[[V2TIMManager sharedInstance] sendMessage:message
                                  receiver:@"userID"
                                   groupID:nil
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:nil
                                      succ:^{
    // The message containing multiple elements sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the message containing multiple element objects
}];
```
:::
</dx-tabs>
