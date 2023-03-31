## Feature Description
* The `addSimpleMsgListener` API is used to listen for and receive text and custom messages, with the callback defined in the `V2TIMSimpleMsgListener` protocol.
* The `addAdvancedMsgListener` API is used to listen for and receive all types of messages (text, custom, and rich media messages), with the callback defined in the `V2TIMAdvancedMsgListener` protocol.
  

## Setting a Message Listener
The SDK provides the `V2TIMSimpleMsgListener` simple message listener and the `V2TIMAdvancedMsgListener` advanced message listener.
They differ in that:
1. The simple message listener **can only** receive text and custom messages. You can use it if your business only requires these two types of messages.
2. The advanced message listener can receive **all** types of messages. You can use it if your business also requires rich media, merged, and other messages.

> ! 
> 1. `addSimpleMsgListener` and `addAdvancedMsgListener` are exclusive. **Do not use both of them**; otherwise, unpredictable logic bugs will occur.
> 2. A message listener **must** be added first to receive the following types of messages.


### Simple message listener

#### Adding a listener
The receiver calls the `addSimpleMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88)) to add the simple message listener. We recommend it be called early, such as after the chat page is initialized, to ensure timely message receiving in the application.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);
```
:::
::: iOS and macOS
```objectivec
// `self` is id<V2TIMSignalingListener>
[[V2TIMManager sharedInstance] addSimpleMsgListener:self];
```
:::
</dx-tabs>

#### Listener callback event
After adding the simple message listener, the receiver can receive different types of messages in the callback of `V2TIMSimpleMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html)), as described below:

<dx-tabs>
::: Android
```java
public abstract class V2TIMSimpleMsgListener {
	// Received the one-to-one text message
	public void onRecvC2CTextMessage(String msgID, V2TIMUserInfo sender, String text) {}

	// Received the custom one-to-one (signaling) message
	public void onRecvC2CCustomMessage(String msgID, V2TIMUserInfo sender, byte[] customData) {}

	// Received the group text message
	public void onRecvGroupTextMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, String text) {}

	// Received the custom group (signaling) message
	public void onRecvGroupCustomMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, byte[] customData) {}
}
```
:::
::: iOS and macOS
```objectivec
/// Basic message callback of the IM SDK
@protocol V2TIMSimpleMsgListener <NSObject>
@optional

/// Received a one-to-one text message
- (void)onRecvC2CTextMessage:(NSString *)msgID  sender:(V2TIMUserInfo *)info text:(NSString *)text;

/// Received a custom one-to-one (signaling) message
- (void)onRecvC2CCustomMessage:(NSString *)msgID  sender:(V2TIMUserInfo *)info customData:(NSData *)data;

/// Received a group text message
- (void)onRecvGroupTextMessage:(NSString *)msgID groupID:(NSString *)groupID sender:(V2TIMGroupMemberInfo *)info text:(NSString *)text;

/// Received a custom group (signaling) message
- (void)onRecvGroupCustomMessage:(NSString *)msgID groupID:(NSString *)groupID sender:(V2TIMGroupMemberInfo *)info customData:(NSData *)data;
@end
```
:::
</dx-tabs>


#### Removing a listener
To stop receiving messages, the receiver can call `removeSimpleMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a86ac462d87f652960d2600a52009849a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#afa3040f676105f3fb78d4835ee3c898b)) to remove the simple message listener.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().removeSimpleMsgListener(simpleMsgListener);
```
:::
::: iOS and macOS
```objectivec
// `self` is id<V2TIMSignalingListener>
[[V2TIMManager sharedInstance] removeSimpleMsgListener:self];
```
:::
</dx-tabs>


### Advanced message listener

#### Adding a listener
The receiver calls the `addAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab)) to add the advanced message listener. We recommend it be called early, such as after the chat page is initialized, to ensure timely message receiving in the application.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().addAdvancedMsgListener(advancedMsgListener);
```
:::
::: iOS and macOS
```objectivec
// `self` is id<V2TIMAdvancedMsgListener>
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];
```
:::
</dx-tabs>

#### Listener callback event
After adding the advanced message listener, the receiver can receive different types of messages in the callback of `V2TIMAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html)), as described below:

<dx-tabs>
::: Android
```java
public abstract class V2TIMAdvancedMsgListener {
	// Received a new message
	public void onRecvNewMessage(V2TIMMessage msg) {}

	// one-to-one message read notification (a notification is received when the receiver calls `markC2CMessageAsRead`)
	public void onRecvC2CReadReceipt(List<V2TIMMessageReceipt> receiptList) {}

	// Message read receipt notification (if read receipts are supported, the notification is received when the receiver calls `sendMessageReadReceipts`)
	public void onRecvMessageReadReceipts(List<V2TIMMessageReceipt> receiptList) {}

	// Received a message recall notification
	public void onRecvMessageRevoked(String msgID) {}

	// The message content is modified.
	public void onRecvMessageModified(V2TIMMessage msg) {}
}
```
:::
::: iOS and macOS
```objectivec
/// Advanced message listener
@protocol V2TIMAdvancedMsgListener <NSObject>
@optional
/// Received a new message
- (void)onRecvNewMessage:(V2TIMMessage *)msg;

/// Message read receipt notification (if read receipts are supported, the notification is received when the receiver calls `sendMessageReadReceipts`)
- (void)onRecvMessageReadReceipts:(NSArray<V2TIMMessageReceipt *> *)receiptList;

/// One-to-one message read notification (a notification is received when the receiver calls `markC2CMessageAsRead`)
- (void)onRecvC2CReadReceipt:(NSArray<V2TIMMessageReceipt *> *)receiptList;

/// Received a message recall notification
- (void)onRecvMessageRevoked:(NSString *)msgID;

/// The message content is modified
- (void)onRecvMessageModified:(V2TIMMessage *)msg;
@end
```
:::
</dx-tabs>

#### Removing a listener
To stop receiving messages, the receiver can call `removeAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6)) to remove the advanced message listener.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().removeAdvancedMsgListener(advancedMsgListener);
```
:::
::: iOS and macOS
```objectivec
// `self` is id<V2TIMAdvancedMsgListener>
[[V2TIMManager sharedInstance] removeAdvancedMsgListener:self];
```
:::
</dx-tabs>


## Receiving a Text Message

### Receiving a message with the simple message listener

#### One-to-one text message
The receiver can receive a one-to-one text message by using the simple message listener in the following steps:
1. Call `addSimpleMsgListener` to set the event listener.
2. Listen for the `onRecvC2CTextMessage` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a59343bacf7c68b560157cdd1417348db) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#a1b467b330291b233c6c15e7e218762b2)) to receive text messages.
3. To stop receiving messages, call `removeSimpleMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:
<dx-tabs>
::: Android
```java
// Set the event listener
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);

// Receive the one-to-one text message
/**
 * Received the one-to-one text message
 *
 * @param msgID Unique message ID
 * @param sender Sender information
 * @param text The sent content
 */
public void onRecvC2CTextMessage(String msgID, V2TIMUserInfo sender, String text) {
	// Parse the message and display it on the UI
}
```
:::
::: iOS and macOS 
```objectivec
// Set the event listener
[[V2TIMManager sharedInstance] addSimpleMsgListener:self];

/// Receive the one-to-one text message
/// @param msgID Message ID
/// @param info Sender information
/// @param text Text content
- (void)onRecvC2CTextMessage:(NSString *)msgID sender:(V2TIMUserInfo *)info text:(NSString *)text {
    // Parse the message and display it on the UI
}
```
:::
</dx-tabs>

#### Group text message
The receiver can receive a group text message by using the simple message listener in the following steps:
1. Call `addSimpleMsgListener` to set the event listener.
2. Listen for the `onRecvGroupTextMessage` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a1f9eaa4fdc323a8ec375b7068df7b7d4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#abee1960a3674e490ce1291889f366d3c)) to receive text messages.
3. To stop receiving messages, call `removeSimpleMsgListener` to remove the listener. This step is optional and can be performed as needed.
   

Sample code:
<dx-tabs>
::: Android
```java
// Set the event listener
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);

// Receive the group text message
/**
 * Received the group text message
 *
 * @param msgID Unique message ID
 * @param groupID Group ID
 * @param sender The group member information of the sender
 * @param text The sent content
 */
public void onRecvGroupTextMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, String text) {
	// Parse the message and display it on the UI
}
```
:::
::: iOS and macOS
```objectivec
// Set the event listener
[[V2TIMManager sharedInstance] addSimpleMsgListener:self];

/// Receive the group text message
/// @param msgID Message ID
/// @param groupID Group ID
/// @param info Sender information
/// @param text Text content
- (void)onRecvGroupTextMessage:(NSString *)msgID groupID:(NSString *)groupID sender:(V2TIMGroupMemberInfo *)info text:(NSString *)text {
    // Parse the message and display it on the UI
}
```
:::
</dx-tabs>


### Receiving a message with the advanced message listener
The receiver can receive a one-to-one or group text message by using the advanced message listener in the following steps:
1. Call `addAdvancedMsgListener` to set the event listener.
2. Listen for the `onRecvNewMessage` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a6771cfa1a897e24b05c17788aba15ff6) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#ae36dde0fab51c29f6d1620ab4b13d7a3)) to receive text messages.
3. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:
<dx-tabs>
::: Android
```java
// Set the event listener
V2TIMManager.getMessageManager().addAdvancedMsgListener(advancedMsgListener);

/**
 * Received a new message
 * @param msg Message
 */
public void onRecvNewMessage(V2TIMMessage msg) {
	// Parse the `groupID` and `userID`
	String groupID = msg.getGroupID();
	String userID = msg.getUserID();

	// Determine whether it's a one-to-one chat or group chat
	// If `groupID` is not empty, the message is from a group chat; if `userID` is not empty, the message is from a one-to-one chat.

	// Parse the text message in `msg`
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_TEXT) {
		V2TIMTextElem textElem = msg.getTextElem();
		String text = textElem.getText();
		Log.i("onRecvNewMessage", "text:" + text);
	}
}
```
:::
::: iOS and macOS
```objectivec
// Set the event listener
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];

/// Receive the message
/// @param msg Message object
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // Parse the `groupID` and `userID`
    NSString *groupID = msg.groupID;
    NSString *userID = msg.userID;

    // Determine whether it's a one-to-one chat or group chat
    // If `groupID` is not empty, the message is from a group chat; if `userID` is not empty, the message is from a one-to-one chat.

    // Parse the text message in `msg`
    if (msg.elemType == V2TIM_ELEM_TYPE_TEXT) {
        V2TIMTextElem *textElem = msg.textElem;
        NSString *text = textElem.text;
        NSLog(@"onRecvNewMessage, text: %@", text);
    }
}
```
:::
</dx-tabs>


## Receiving a Custom Message

### Receiving a message with the simple message listener

#### Custom one-to-one message

The receiver can receive a custom one-to-one message by using the simple message listener in the following steps:
1. Call `addSimpleMsgListener` to set the event listener.
2. Listen for the `onRecvC2CCustomMessage` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a13d77741c8286b011c1eb7513a9eb2c7) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#ae6eec84f9664f08591bc743f20f2360b)) to receive custom one-to-one messages.
3. To stop receiving messages, call `removeSimpleMsgListener` to remove the listener. This step is optional and can be performed as needed.
   

Sample code:
<dx-tabs>
::: Android
```java
/**
 * Receive the custom one-to-one message
 * @param msgID Message ID
 * @param sender Sender information
 * @param customData The sent content
 */
public void onRecvC2CCustomMessage(String msgID, V2TIMUserInfo sender, byte[] customData) {
	Log.i("onRecvC2CCustomMessage", "msgID:" + msgID + ", from:" + sender.getNickName() + ", content:" + new String(customData));
}
```
:::
::: iOS and macOS
```objectivec
/// Receive the custom one-to-one message
/// @param msgID Message ID
/// @param info Sender information
/// @param data The binary content of the custom message
- (void)onRecvC2CCustomMessage:(NSString *)msgID sender:(V2TIMUserInfo *)info customData:(NSData *)data {
    NSLog(@"onRecvC2CCustomMessage, msgID: %@, sender: %@, customData: %@", msgID, info, data);
}
```
:::
</dx-tabs>


#### Custom group message
The receiver can receive a custom group message by using the simple message listener in the following steps:
1. Call `addSimpleMsgListener` to set the event listener.
2. Listen for the `onRecvGroupCustomMessage` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a46b48869e411b41c25a98211d951335c) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#abd21785aa5bfcee78ffb1a94383077d1)) to receive custom group messages.
3. To stop receiving messages, call `removeSimpleMsgListener` to remove the listener. This step is optional and can be performed as needed.
   

<dx-tabs>
::: Android
```java
/**
 * Receive the custom group message
 * @param msgID Message ID
 * @param groupID Group ID
 * @param sender The group member information of the sender
 * @param customData The sent content
 */
public void onRecvGroupCustomMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, byte[] customData) {
	Log.i("onRecvGroupCustomMessage", "msgID:" + msgID + ", groupID:" + groupID + ", from:" + sender.getNickName() + ", content:" + new String(customData));
}
```
:::
::: iOS and macOS
```objectivec
/// Receive the custom group message
/// @param msgID Message ID
/// @param groupID Group ID
/// @param info Sender information
/// @param text The binary content of the custom message
- (void)onRecvGroupCustomMessage:(NSString *)msgID groupID:(NSString *)groupID sender:(V2TIMGroupMemberInfo *)info customData:(NSData *)data {
	NSLog(@"onRecvGroupCustomMessage, msgID: %@, groupID: %@, sender: %@, customData: %@", msgID, groupID, info, data);
}
```
:::
</dx-tabs>


### Receiving a message with the advanced message listener
The receiver can receive a custom one-to-one or group message by using the advanced message listener in the following steps:
1. Call `addAdvancedMsgListener` to set the event listener.
2. Listen for the `onRecvNewMessage` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a6771cfa1a897e24b05c17788aba15ff6) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#ae36dde0fab51c29f6d1620ab4b13d7a3)) to receive custom messages.
3. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:
<dx-tabs>
::: Android
```java
// Set the event listener
V2TIMManager.getMessageManager().addAdvancedMsgListener(v2TIMAdvancedMsgListener);

// Receive the message
public void onRecvNewMessage(V2TIMMessage msg) {
	// Parse the `groupID` and `userID`
	String groupID = msg.getGroupID();
	String userID = msg.getUserID();

	// Determine whether it's a one-to-one chat or group chat
	// If `groupID` is not empty, the message is from a group chat; if `userID` is not empty, the message is from a one-to-one chat.

	// Parse the custom message in `msg`
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_CUSTOM) {
		V2TIMCustomElem customElem = msg.getCustomElem();
		String data = new String(customElem.getData());
		Log.i("onRecvNewMessage", "customData:" + data);
	}
}
```
:::
::: iOS and macOS
```objectivec
// Set the event listener
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];

/// Receive the message
/// @param msg Message object
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // Parse the `groupID` and `userID`
    NSString *groupID = msg.groupID;
    NSString *userID = msg.userID;

    // Determine whether it's a one-to-one chat or group chat
    // If `groupID` is not empty, the message is from a group chat; if `userID` is not empty, the message is from a one-to-one chat.

    // Parse the custom message in `msg`
    if (msg.elemType == V2TIM_ELEM_TYPE_CUSTOM) {
        V2TIMCustomElem *customElem = msg.customElem;
        NSData *customData = customElem.data;
        NSLog(@"onRecvNewMessage, customData: %@", customData);
    }
}
```
:::
</dx-tabs>


## Receiving a Rich Media Message
The receiver can receive a rich media message **only by using** the advanced message listener in the following steps:
1. Call the `addAdvancedMsgListener` API to set the advanced message listener.
2. Listen for the `onRecvNewMessage` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a6771cfa1a897e24b05c17788aba15ff6) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#ae36dde0fab51c29f6d1620ab4b13d7a3)) to receive the `V2TIMMessage` message.
3. Parse the `elemType` attribute in the `V2TIMMessage` message and then parse the message again according to the type to get the specific content of the elements in the message.
4. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.


### Image message

The image in an image message can be in three formats: original, large, and thumbnail. The latter two are automatically generated by the SDK during message sending and can be ignored.
* Large image: A large image is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 720 pixels.
* Thumbnail: A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 198 pixels.

After the image message is received, we recommend you call the SDK's `downloadImage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMImageElem_1_1V2TIMImage.html#a9114c16b095bbf608027c71eb40e9025) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMImage.html#a2ef83a4fb5c2a047acaf881ee90df58e)) to download the image and then render it to the UI layer.

To avoid repeated download and save resources, we recommend you set the `uuid` attribute value of the `V2TIMImage` object to the image download path to identify the image.

The following sample code demonstrates how to parse the image content from `V2TIMMessage`:

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_IMAGE) {
		// Image message
		V2TIMImageElem v2TIMImageElem = msg.getImageElem();
		// The image in an image message can be in three formats: original, large, and thumbnail. The latter two are automatically generated by the SDK during message sending and can be ignored.
		// Large image: A large image is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 720 pixels.
		// Thumbnail: A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 198 pixels.
		List<V2TIMImageElem.V2TIMImage> imageList = v2TIMImageElem.getImageList();
		for (V2TIMImageElem.V2TIMImage v2TIMImage : imageList) {
			// Image ID, which is an internal ID and can be used as an external cache key
			String uuid = v2TIMImage.getUUID();
			// Image type
			int imageType = v2TIMImage.getType();
			// Image size (bytes)
			int size = v2TIMImage.getSize();
			// Image width
			int width = v2TIMImage.getWidth();
			// Image height
			int height = v2TIMImage.getHeight();
			// Set the image download path `imagePath`. Here, `uuid` can be used as an identifier to avoid repeated download.
			String imagePath = "/sdcard/im/image/" + "myUserID" + uuid;
			File imageFile = new File(imagePath);
			// Determine whether there is a downloaded image file in `imagePath`
			if (!imageFile.exists()) {
				// Download the image
				v2TIMImage.downloadImage(imagePath, new V2TIMDownloadCallback() {
					@Override
					public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
						// Callback for download progress. `v2ProgressInfo.getCurrentSize()` indicates the downloaded file size, and `v2ProgressInfo.getTotalSize()` indicates the total file size.
					}
					@Override
					public void onError(int code, String desc) {
						// Download failed
					}
					@Override
					public void onSuccess() {
						// Downloaded
					}
				});
			} else {
				// The image already exists.
			}
		}
	}
}
```
:::
::: iOS and macOS
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_IMAGE) {
        V2TIMImageElem *imageElem = msg.imageElem;
        // The list of original images, large images, and thumbnails
        NSArray<V2TIMImage *> *imageList = imageElem.imageList;
        for (V2TIMImage *timImage in imageList) {
            // Image ID, which is an internal ID and can be used as an external cache key
            NSString *uuid = timImage.uuid;
            // Image type
            V2TIMImageType type = timImage.type;
            // Image size (bytes)
            int size = timImage.size;
            // Image width
            int width = timImage.width;
            // Image height
            int height = timImage.height;
            // Set the image download path `imagePath`. Here, `uuid` can be used as an identifier to avoid repeated download.
            NSString *imagePath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testImage%@", timImage.uuid]];
            // Determine whether there is a downloaded image file in `imagePath`
            if (![[NSFileManager defaultManager] fileExistsAtPath:imagePath]) {
                // Download the image
                [timImage downloadImage:imagePath progress:^(NSInteger curSize, NSInteger totalSize) {
                    // Download progress
                    NSLog(@"Image download progress: curSize: %lu,totalSize:%lu",curSize,totalSize);
                } succ:^{
                    // Downloaded successfully
                    NSLog(@"Image downloaded");
                } fail:^(int code, NSString *msg) {
                    // Download failed
                    NSLog(@"Failed to download the image: code: %d,msg:%@",code,msg);
                }];
            } else {
                // The image already exists.
            }
            NSLog(@"Image information: uuid:%@, type:%ld, size:%d, width:%d, height:%d", uuid, (long)type, size, width, height);
        }
    }
}
```
:::
</dx-tabs>


### Video message

After a video message is received, a video preview is displayed on the chat page, and the video is played back after the user clicks the message.
Two steps are required:
1. Download the video screenshot. We recommend you call the SDK's `downloadSnapshot` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMVideoElem.html#abee852d50627376a147a98a7375dea1a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMVideoElem.html#a7ae717400d7a9df3f337f0759a6b3163)) for download.
2. Download the video. We recommend you call the SDK's `downloadVideo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMVideoElem.html#a0adbdd0bcaed5093176db51d284976ea) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMVideoElem.html#a6e83b77be6db2005e91b90d2e2ac2f6a)) for download.

To avoid repeated download and save resources, we recommend you set the `videoUUID` attribute value of the `V2TIMVideoElem` object to the video download path to identify the video.

The following sample code demonstrates how to parse the video content from `V2TIMMessage`:

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_VIDEO) {
		// Video message
		V2TIMVideoElem v2TIMVideoElem = msg.getVideoElem();
		// Video screenshot ID, which is an internal ID and can be used as an external cache key
		String snapshotUUID = v2TIMVideoElem.getSnapshotUUID();
		// Video screenshot file size
		int snapshotSize = v2TIMVideoElem.getSnapshotSize();
		// Video screenshot width
		int snapshotWidth = v2TIMVideoElem.getSnapshotWidth();
		// Video screenshot height
		int snapshotHeight = v2TIMVideoElem.getSnapshotHeight();
		// Video ID, which is an internal ID and can be used as an external cache key
		String videoUUID = v2TIMVideoElem.getVideoUUID();
		// Video file size
		int videoSize = v2TIMVideoElem.getVideoSize();
		// Video duration
		int duration = v2TIMVideoElem.getDuration();
		// Set the video screenshot file path. Here, `uuid` can be used as an identifier to avoid repeated download.
		String snapshotPath = "/sdcard/im/snapshot/" + "myUserID" + snapshotUUID;
		File snapshotFile = new File(snapshotPath);
		if (!snapshotFile.exists()) {
			v2TIMVideoElem.downloadSnapshot(snapshotPath, new V2TIMDownloadCallback() {
				@Override
				public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
					// Callback for download progress. `v2ProgressInfo.getCurrentSize()` indicates the downloaded file size, and `v2ProgressInfo.getTotalSize()` indicates the total file size.
				}
				@Override
				public void onError(int code, String desc) {
					// Download failed
				}
				@Override
				public void onSuccess() {
					// Downloaded
				}
			});
		} else {
			// The file already exists.
		}

		// Set the video file path. Here, `uuid` can be used as an identifier to avoid repeated download.
		String videoPath = "/sdcard/im/video/" + "myUserID" + videoUUID;
		File videoFile = new File(videoPath);
		if (!videoFile.exists()) {
			v2TIMVideoElem.downloadVideo(videoPath, new V2TIMDownloadCallback() {
				@Override
				public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
				// Callback for download progress. `v2ProgressInfo.getCurrentSize()` indicates the downloaded file size, and `v2ProgressInfo.getTotalSize()` indicates the total file size.
				}
				@Override
				public void onError(int code, String desc) {
				// Download failed
				}
				@Override
				public void onSuccess() {
				// Downloaded
				}
			});
		} else {
			// The file already exists.
		}
	}
}
```
:::
::: iOS and macOS
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_VIDEO) {
        V2TIMVideoElem *videoElem = msg.videoElem;
        // Video screenshot ID, which is an internal ID and can be used as an external cache key
        NSString *snapshotUUID = videoElem.snapshotUUID;
        // Video screenshot file size
        int snapshotSize = videoElem.snapshotSize;
        // Video screenshot width
        int snapshotWidth = videoElem.snapshotWidth;
        // Video screenshot height
        int snapshotHeight = videoElem.snapshotHeight;
        // Video ID, which is an internal ID and can be used as an external cache key
        NSString *videoUUID = videoElem.videoUUID;
        // Video file size
        int videoSize = videoElem.videoSize;
        // Video duration
        int duration = videoElem.duration;
        // Set the video screenshot file path. Here, `uuid` can be used as an identifier to avoid repeated download.
        NSString *snapshotPath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testVideoSnapshot%@",snapshotUUID]];
        if (![[NSFileManager defaultManager] fileExistsAtPath:snapshotPath]) {
            // Download the video screenshot
            [videoElem downloadSnapshot:snapshotPath progress:^(NSInteger curSize, NSInteger totalSize) {
                // Download progress
                NSLog(@"%@", [NSString stringWithFormat:@"Video screenshot download progress: curSize: %lu,totalSize:%lu",curSize,totalSize]);
            } succ:^{
                // Downloaded successfully
                NSLog(@"Video screenshot downloaded");
            } fail:^(int code, NSString *msg) {
                // Download failed
                NSLog(@"%@", [NSString stringWithFormat:@"Failed to download the video screenshot: code: %d,msg:%@",code,msg]);
            }];
        } else {
            // The video screenshot already exists.
        }
        NSLog(@"Video screenshot information: snapshotUUID:%@, snapshotSize:%d, snapshotWidth:%d, snapshotWidth:%d, snapshotPath:%@", snapshotUUID, snapshotSize, snapshotWidth, snapshotHeight, snapshotPath);
        
        // Set the video file path. Here, `uuid` can be used as an identifier to avoid repeated download.
        NSString *videoPath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testVideo%@",videoUUID]];
        if (![[NSFileManager defaultManager] fileExistsAtPath:videoPath]) {
            // Download the video
            [videoElem downloadVideo:videoPath progress:^(NSInteger curSize, NSInteger totalSize) {
                // Download progress
                NSLog(@"%@", [NSString stringWithFormat:@"Video download progress: curSize: %lu,totalSize:%lu",curSize,totalSize]);
            } succ:^{
                // Downloaded successfully
                NSLog(@"Video downloaded");
            } fail:^(int code, NSString *msg) {
                // Download failed
                NSLog(@"%@", [NSString stringWithFormat:@"Failed to download the video: code: %d,msg:%@",code,msg]);
            }];
        } else {
            // The video already exists.
        }
        NSLog(@"Video information: videoUUID:%@, videoSize:%d, duration:%d, videoPath:%@", videoUUID, videoSize, duration, videoPath);
    }
}
```
:::
</dx-tabs>

### Audio message

After the audio message is received, we recommend you call the SDK's `downloadSound` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSoundElem.html#a24cb6b4e90687833a6de8fa62e868b3a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMSoundElem.html#ac06d3cc1193da9e6b10d6256dc95f2b2)) to download the audio and then play it back.

To avoid repeated download and save resources, we recommend you set the `uuid` attribute value of the `V2TIMSoundElem` object to the audio download path to identify the audio.

The following sample code demonstrates how to parse the audio content from `V2TIMMessage`:

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_SOUND) {
		// Audio message
		V2TIMSoundElem v2TIMSoundElem = msg.getSoundElem();
		// Audio ID, which is an internal ID and can be used as an external cache key
		String uuid = v2TIMSoundElem.getUUID();
		// Audio file size
		int dataSize = v2TIMSoundElem.getDataSize();
		// Audio duration
		int duration = v2TIMSoundElem.getDuration();
		// Set the audio file path `soundPath`. Here, `uuid` can be used as an identifier to avoid repeated download
		String soundPath = "/sdcard/im/sound/" + "myUserID" + uuid;
		File imageFile = new File(soundPath);
		// Determine whether there is a downloaded audio file in `soundPath`
		if (!imageFile.exists()) {
			v2TIMSoundElem.downloadSound(soundPath, new V2TIMDownloadCallback() {
				@Override
				public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
					// Callback for download progress. `v2ProgressInfo.getCurrentSize()` indicates the downloaded file size, and `v2ProgressInfo.getTotalSize()` indicates the total file size.
				}
				@Override
				public void onError(int code, String desc) {
					// Download failed
				}
				@Override
				public void onSuccess() {
					// Downloaded
				}
			});
		} else {
			// The file already exists.
		}
	}
}
```
:::
::: iOS and macOS
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_SOUND) {
        V2TIMSoundElem *soundElem = msg.soundElem;
        // Audio ID, which is an internal ID and can be used as an external cache key
        NSString *uuid = soundElem.uuid;
        // Audio file size
        int dataSize = soundElem.dataSize;
        // Audio duration
        int duration = soundElem.duration;
        // Set the audio file path `soundPath`. Here, `uuid` can be used as an identifier to avoid repeated download
        NSString *soundPath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testSound%@",uuid]];
        // Determine whether there is a downloaded audio file in `soundPath`
        if (![[NSFileManager defaultManager] fileExistsAtPath:soundPath]) {
            // Download the audio
            [soundElem downloadSound:soundPath progress:^(NSInteger curSize, NSInteger totalSize) {
                // Download progress
                NSLog(@"Audio download progress: curSize: %lu,totalSize:%lu",curSize,totalSize);
            } succ:^{
                // Downloaded successfully
                NSLog(@"Audio downloaded");
            } fail:^(int code, NSString *msg) {
                // Download failed
                NSLog(@"Failed to download the audio: code: %d,msg:%@",code,msg);
            }];
        } else {
            // The audio already exists.
        }
        NSLog(@"Audio information: uuid:%@, dataSize:%d, duration:%d, soundPath:%@", uuid, dataSize, duration, soundPath);
    }
}
```
:::
</dx-tabs>

### File message

After the file message is received, we recommend you call the SDK's `downloadFile` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFileElem.html#a932e3acc34504d83f0e1e94799057d5a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFileElem.html#a6ecb2ec506745c2fce99f78bab616009)) to download the file and then display it.

To avoid repeated download and save resources, we recommend you set the `uuid` attribute value of the `V2TIMFileElem` object to the file download path to identify the file.

The following sample code demonstrates how to parse the file content from `V2TIMMessage`:

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_FILE) {
		// File message
		V2TIMFileElem v2TIMFileElem = msg.getFileElem();
		// File ID, which is an internal ID and can be used as an external cache key
		String uuid = v2TIMFileElem.getUUID();
		// Filename
		String fileName = v2TIMFileElem.getFileName();
		// File size
		int fileSize = v2TIMFileElem.getFileSize();
		// Set the file path. Here, `uuid` can be used as an identifier to avoid repeated download.
		String filePath = "/sdcard/im/file/" + "myUserID" + uuid;
		File file = new File(filePath);
		if (!file.exists()) {
			v2TIMFileElem.downloadFile(filePath, new V2TIMDownloadCallback() {
				@Override
				public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
					// Callback for download progress. `v2ProgressInfo.getCurrentSize()` indicates the downloaded file size, and `v2ProgressInfo.getTotalSize()` indicates the total file size.
				}
				@Override
				public void onError(int code, String desc) {
					// Download failed
				}
				@Override
				public void onSuccess() {
					// Downloaded
				}
			});
		} else {
			// The file already exists.
		}
	}
}
```
:::
::: iOS and macOS
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_FILE) {
        V2TIMFileElem *fileElem = msg.fileElem;
        // File ID, which is an internal ID and can be used as an external cache key
        NSString *uuid = fileElem.uuid;
        // Filename
        NSString *filename = fileElem.filename;
        // File size
        int fileSize = fileElem.fileSize;
        // Set the file path. Here, `uuid` can be used as an identifier to avoid repeated download.
        NSString *filePath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testFile%@",uuid]];
        if (![[NSFileManager defaultManager] fileExistsAtPath:filePath]) {
            // Download the file
            [fileElem downloadFile:filePath progress:^(NSInteger curSize, NSInteger totalSize) {
                // Download progress
                NSLog(@"%@", [NSString stringWithFormat:@"File download progress: curSize: %lu,totalSize:%lu",curSize,totalSize]);
            } succ:^{
                // Downloaded successfully
                NSLog(@"File downloaded");
            } fail:^(int code, NSString *msg) {
                // Download failed
                NSLog(@"%@", [NSString stringWithFormat:@"Failed to download the file: code: %d,msg:%@",code,msg]);
            }];
        } else {
            // The file already exists.
        }
        NSLog(@"File information: uuid:%@, filename:%@, fileSize:%d, filePath:%@", uuid, filename, fileSize, filePath);
    }
}
```
:::
</dx-tabs>

### Geographical location message

After receiving the geographical location message, the receiver can parse the latitude and longitude information directly from `V2TIMLocationElem`.
The following sample code demonstrates how to parse the geographical location content from `V2TIMMessage`:

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_LOCATION) {
		// Geographical location message
		V2TIMLocationElem v2TIMLocationElem = msg.getLocationElem();
		// Geographical location information description
		String desc = v2TIMLocationElem.getDesc();
		// Longitude
		double longitude = v2TIMLocationElem.getLongitude();
		// Latitude
		double latitude = v2TIMLocationElem.getLatitude();
	}
}
```
:::
::: iOS and macOS
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_LOCATION) {
        V2TIMLocationElem *locationElem = msg.locationElem;
        // Geographical location information description
        NSString *desc = locationElem.desc;
        // Longitude
        double longitude = locationElem.longitude;
        // Latitude
        double latitude = locationElem.latitude;
        NSLog(@"Geographical location information: desc: %@, longitude:%f, latitude:%f", desc, longitude, latitude);
    }
}
```
:::
</dx-tabs>

### Emoji message

The SDK provides a passthrough channel only for emoji messages. For message content fields, see the definition of `V2TIMFaceElem` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFaceElem.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFaceElem.html)). Here, `index` and `data` can be customized.

For example, the sender can set `index` to `1` and `data` to `x12345` to indicate the smile emoji.
The receiver parses the received emoji message as `1` and `x12345` and displays the message as the smile emoji according to the preset rules.

The following sample code demonstrates how to parse the emoji content from `V2TIMMessage`:
<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_FACE) {
		// Emoji message
		V2TIMFaceElem v2TIMFaceElem = msg.getFaceElem();
		// Emoji location
		int index = v2TIMFaceElem.getIndex();
		// Custom emoji data
		byte[] data = v2TIMFaceElem.getData();
	}
}
```
:::
::: iOS and macOS
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_FACE) {
        V2TIMFaceElem *faceElem = msg.faceElem;
        // Emoji location
        int index = faceElem.index;
        // Custom emoji data
        NSData *data = faceElem.data;
        NSLog(@"Emoji information: index: %d, data: %@", index, data);
    }
}
```
:::
</dx-tabs>

## Receiving a Message Containing Multiple Element Objects

1. Parse the first element object through the Message object.
2. Get the next element object through the `nextElem` method of the first element object. If the next object exists, an element object instance is returned; otherwise, `nil` or `null` is returned.

Sample code:
<dx-tabs>
::: Android
```java
@Override
public void onRecvNewMessage(V2TIMMessage msg) {
	// View the first element
	int elemType = msg.getElemType();
	if (elemType == V2TIMMessage.V2TIM_ELEM_TYPE_TEXT) {
		// Text message
		V2TIMTextElem v2TIMTextElem = msg.getTextElem();
		String text = v2TIMTextElem.getText();
		// Check whether `v2TIMTextElem` is followed by more elements
		V2TIMElem elem = v2TIMTextElem.getNextElem();
		while (elem != null) {
			// Identify the element type. Here, `V2TIMCustomElem` is used as an example.
			if (elem instanceof V2TIMCustomElem) {
			V2TIMCustomElem customElem = (V2TIMCustomElem) elem;
			byte[] data = customElem.getData();
		}
		// Further check whether the current element is followed by more elements
		elem = elem.getNextElem();
		}
		// If the element is `null`, all the elements have been parsed.
	}
}
```
:::
::: iOS and macOS
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // View the first element
    if (msg.elemType == V2TIM_ELEM_TYPE_TEXT) {
        V2TIMTextElem *textElem = msg.textElem;
        NSString *text = textElem.text;
        NSLog(@"Text information: %@", text);
        // Check whether `textElem` is followed by more elements
        V2TIMElem *elem = textElem.nextElem;
        while (elem != nil) {
            // Identify the element type
            if ([elem isKindOfClass:[V2TIMCustomElem class]]) {
                V2TIMCustomElem *customElem = (V2TIMCustomElem *)elem;
                NSData *customData = customElem.data;
                NSLog(@"Custom information: %@",customData);
            }
            // Further check whether the current element is followed by more elements
            elem = elem.nextElem;
        }
        // If the element is `nil`, all the elements have been parsed.
    }
}
```
:::
</dx-tabs>
