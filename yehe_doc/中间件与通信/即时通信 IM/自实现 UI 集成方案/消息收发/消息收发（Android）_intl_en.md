## Message Classification
IM messages are classified by message destination into two types: one-to-one messages (also called C2C messages) and group messages.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| One-to-one message | C2CMessage | Also called C2C message. When sending a one-to-one message, you must specify the UserID of the message recipient, and only the recipient can receive this message. |
| Group message | GroupMessage | When sending a group message, you must specify the groupID of the target group, and all users in this group can receive this message. |

IM messages can also be classified by content into text messages, custom (signaling) messages, image messages, video messages, voice messages, file messages, location messages, combined messages, and group tips.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| Custom message | CustomElem | It is a section of binary buffer and often used to transfer custom signaling in your application. |
| Image message | ImageElem | When the IM SDK sends an original image, it automatically generates two images in different sizes. The three images are called the original image, large image, and thumbnail. |
| Video message | VideoElem | A video message contains a video file and an image. |
| Voice message | SoundElem | It supports displaying a red dot upon playback of the voice message. |
| File message | FileElem | A file message cannot exceed 100 MB. |
| Location message | LocationElem | A location message contains three fields: location description, longitude, and latitude. |
| Combined message | MergerElem | Up to 300 messages can be combined. |
| Group tip | GroupTipsElem | A group tip is often used to carry a system notification in a group, such as a notification indicating the following: a member joins or leaves the group; the group description is modified; or the profile of a group member is changed. |

## Sending and Receiving Simple Messages
[V2TIMManager](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html) provides a set of simple APIs for sending and receiving messages. Although these APIs can only be used to send or receive text messages and custom (signaling) messages, they are easy to use and it only takes a few minutes to complete interfacing.

### Sending text and signaling messages
To send text messages, call [sendC2CTextMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a59a8ba6e4a973b4c40a09ae7dfdc6981) or [sendGroupTextMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52). To send custom one-to-one (signaling) messages, call [sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af3e08b936df77210c6cdd0ce5c7fa87f) or [sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2). A custom message is essentially a section of binary buffer, and is often used to transfer custom signaling in your application.

### Receiving text and signaling messages
To listen to simple text and signaling messages, call [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b). To listen to image, video, and voice messages, call [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) defined in [V2TIMMessageManager](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html).

>! Do not use [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) together with [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823); otherwise, logic bugs may occur.

### Typical example: Sending and receiving on-screen comments
In the livestreaming scenario, it is a common way of communication to send or receive on-screen comments in an audio-video group. This can be easily implemented through the simple message APIs.

1. The anchor can call [createGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) to create an audio-video group (AVChatRoom) and record the group ID in the list of rooms in "Broadcasting" state.
2. The audience can select an anchor they like, and call [joinGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) to join the audio-video group created by this anchor.
3. A message sender can call [sendGroupTextMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52) to send a group text message as an on-screen comment.
4. A message recipient can call [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) to register a simple message listener, and use the listener callback function [onRecvGroupTextMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a1f9eaa4fdc323a8ec375b7068df7b7d4) to obtain text messages.

"FlyHeart" is an instruction. To configure the "FlyHeart" feature for a live room, perform the steps below:
1. Define a custom message type, such as a JSON string `{ "command": "favor", "value": 101 }`.
2. Call [sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2) to send a message, and call [onRecvGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a46b48869e411b41c25a98211d951335c) to receive the message.

## Sending and Receiving Rich Media Messages
Image, video, voice, file, and location messages are called rich media messages. Compared with sending or receiving simple messages, it is more complex to send or receive rich media messages.
- Before sending a rich media message, use the `create` function to create an object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html). Then, call the corresponding `send` API to send this message.
- To receive a rich media message, first check `elemType` and perform secondary parsing on `Elem` obtained based on `elemType`.

### Sending rich media messages
The following takes an image message as an example to describe the process of sending a rich media message.
1. The sender calls [createImageMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adef5bc7a67b9a69f70f6417fd810d4b1) to create an image message, and obtain the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html).
2. The sender calls [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send the created message object.

### Receiving rich media messages
1. The recipient calls [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) to set the advanced message listener.
2. The recipient obtains the image message [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html) through the listener callback [onRecvNewMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a6771cfa1a897e24b05c17788aba15ff6).
3. The recipient parses `elemType` in [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html), and performs secondary parsing based on the element type to obtain the content of `Elem` in the message.

### Typical example: Sending and receiving image messages
The sender creates and sends an image message.
```
// Create an image message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createImageMessage("/sdcard/test.png");
// Send the image message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "toUserID", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null,  new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onError(int code, String desc) {
		// The image message failed to be sent
	}
	@Override
	public void onSuccess(V2TIMMessage v2TIMMessage) {
		// The image message was sent successfully
	}
	@Override
	public void onProgress(int progress) {
		// Image upload progress (0-100)
	}
});
```

The recipient identifies the image message, and parses the message to obtain the original image, large image, and thumbnail contained in the message.
```
@Override
public void onRecvNewMessage(V2TIMMessage msg) {
	int elemType = msg.getElemType();
	if (elemType == V2TIMMessage.V2TIM_ELEM_TYPE_IMAGE) {
		V2TIMImageElem v2TIMImageElem = msg.getImageElem();
		// An image message contains an image in three different sizes: original image, large image, and thumbnail. The SDK automatically generates a large image and a thumbnail.
		// A large image is obtained after the original image is proportionally compressed. After the compression, the smaller one of the height and width is equal to 720 pixels.
		// A thumbnail is obtained after the original image is proportionally compressed. After the compression, the smaller one of the height and width is equal to 198 pixels.
		List<V2TIMImageElem.V2TIMImage> imageList = v2TIMImageElem.getImageList();
			for (V2TIMImageElem.V2TIMImage v2TIMImage : imageList) {
				String uuid = v2TIMImage.getUUID(); // Image ID
				int imageType = v2TIMImage.getType(); // Image type
				int size = v2TIMImage.getSize(); // Image size (bytes)
				int width = v2TIMImage.getWidth(); // Image width
				int height = v2TIMImage.getHeight(); // Image height
				// Set the image download path `imagePath`. Here, `uuid` can be used as an identifier to avoid repeated download.
				String imagePath = "/sdcard/im/image/" + "myUserID" + uuid;
				File imageFile = new File(imagePath);
				if (imageFile.exists()) {
					v2TIMImage.downloadImage(imagePath, new V2TIMDownloadCallback() {
						@Override
						public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
							// Image download progress. `v2ProgressInfo.getCurrentSize()` indicates the downloaded size, and `v2ProgressInfo.getTotalSize()` indicates the total file size.
						}
						@Override
						public void onError(int code, String desc) {
							// The image failed to be downloaded
						}
						@Override
						public void onSuccess() {
							// The image was successfully downloaded
						}
					});
			} else {
				// The image already exists
			}
		}   
	}
}
```

>? For more information on the message parsing sample code, see [FAQs > 5. How can I parse different types of messages](#msgAnalyze).

## Sending and Receiving Group @ Messages
For a group @ message, the sender can listen for the input of the @ character in the text box and call the group member selection interface. After selection is completed, the text box displays the content in the format of `"@A @B @C......"`, and then the sender can continue to edit the message content and send the message. On the group chat list of the recipient’s conversation interface, the identifier `"someone@me"` or `"@all members"` will be displayed to remind the user that the user was mentioned by someone in the group.
>? Currently, only text @ messages are supported.

### Sending group @ messages
1. The sender listens to the text input box on the chat interface and enables the group member selection interface. After selection is completed, the ID and nickname of the selected member are returned. The ID is used to create the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html), and the nickname is displayed in the text box.
2. The sender calls [createTextAtMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad255ff81ed0b9ee71273a1b20cf6d753) of [V2TIMMessageManager](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html) to create an @ text message and obtain the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html).
3. The sender calls [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send the created @ message object.

### Receiving group @ messages
1. During conversation loading and update, call the [getGroupAtInfoList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a54790b0fd99c2504a73b42b884fba8a9) API of [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html) to obtain the @ data list of the conversation List < for combined messages, it is on the chat interface [V2TIMGroupAtInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupAtInfo.html) >.
2. Obtain the @ data type through the API [getAtType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupAtInfo.html#aebb86a00883eb70fdab2c5f4728aae5d) of the object [V2TIMGroupAtInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupAtInfo.html) on the list, and update the @ information of the current conversation with the @ data type.

### Typical examples: sending and receiving group @ messages
- **Sending a group @ message**:
The sender creates and sends a group @ message:
```
// Obtain the IDs of group members
List<String> atUserList = updateAtUserList(mTextInput.getMentionList(true));
// Create a group @ message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextAtMessage(message, atUserList);
// Send the group @ message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, null, "toGroupID",  V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null,  new V2TIMSendCallback<V2TIMMessage>() {
    @Override
    public void onError(int code, String desc) {
        // The group @ message failed to be sent
    }
    @Override
    public void onSuccess(V2TIMMessage v2TIMMessage) {
        // The group @ message was successfully sent
    }
    @Override
    public void onProgress(int progress) {

    }
});
```

- **Receiving a group @ message**:
  During conversation loading and update, obtain the group @ data list:
```
boolean atMe = false;
boolean atAll = false;
// Obtain the group @ data list
List<V2TIMGroupAtInfo> atInfoList = conversation.getGroupAtInfoList();
if (atInfoList == null || atInfoList.isEmpty()){
    return V2TIMGroupAtInfo.TIM_AT_UNKNOWN;
}
// Obtain the @ data type
for(V2TIMGroupAtInfo atInfo : atInfoList){
    if (atInfo.getAtType() == V2TIMGroupAtInfo.TIM_AT_ME){
        atMe = true;
        continue;
    }
    if (atInfo.getAtType() == V2TIMGroupAtInfo.TIM_AT_ALL){
        atAll = true;
        continue;
    }
}

if (atAll && atMe){
    atInfoType = V2TIMGroupAtInfo.TIM_AT_ALL_AT_ME;
} else if (atAll){
    atInfoType = V2TIMGroupAtInfo.TIM_AT_ALL;
} else if (atMe){
    atInfoType = V2TIMGroupAtInfo.TIM_AT_ME;
} else {
    atInfoType = V2TIMGroupAtInfo.TIM_AT_UNKNOWN;
}
// Update the @ type to the current conversation
switch (atInfoType){
    case V2TIMGroupAtInfo.TIM_AT_ME:
        Log.d(TAG, "update to the current conversation to display [someone@me]");
        break;
    case V2TIMGroupAtInfo.TIM_AT_ALL:
        Log.d(TAG, "update to the current conversation to display [@all members]");
        break;
    case V2TIMGroupAtInfo.TIM_AT_ALL_AT_ME:
        Log.d(TAG, "update to the current conversation to display [someone@me][@all members]");
        break;
    default:
        break;

}
```

## Sending and Receiving Combined Messages
To implement the Combine and Forward feature, it is necessary to create a combined message according to the original message list, and then send the combined message to the peer end. After the peer end receives the combined message, it will parse out the original message list. A title and abstracts are required to display the combined message. 

>! Only available in Enhanced Edition v5.2.210 or later.

- **Sending a combined message**
Usually, when we receive a combined message, the chat UI will look like this:

| Chat History of Vinson and Lynx | Title |
|---------|---------|
| Vinson: When is the new version of SDK scheduled to go online? | abstract1 |
| Lynx: Next Monday. The specific time depends on the system test result in these two days. | abstract2 |
| Vinson: OK | abstract3 |

The chat UI will display only the title and abstract information of the combined message, and the combined message list will be displayed only when the user clicks the combined message. To create a combined message, it is necessary to set not only the combined message list, but also the title and abstract information. The implementation process is as follows: (supported only in v5.2.210 or later)
1. Call the API [createMergerMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#acebe275789ab49cc8abe6af5e07aa3b0) to create a combined message.
2. Call the API [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) to send the combined message.

- **Receiving a combined message**
When receiving a combined message [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html), use [V2TIMMergerElem](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html) to get [title](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html#a864916a91d453e2124c12e0ccbb66550) and [abstractList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html#a8d9dd51a05a5c1ee63dfb4e710c85aff) for UI display. When the user clicks the combined message, call the API [downloadMergerMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html#af34d8228a9842875652a726f24ac3d30) to download the combined message list for UI display.


### Typical examples: sending and receiving combined messages
- **Sending a combined message**
The sender creates and sends a combined message.
```java
// List of messages to be forwarded, which can contain combined messages but not group tips
List<V2TIMMessage> msgs = new ArrayList<>();
msgs.add(message1);
msgs.add(message2);
// Title of the combined message
String title = "Chat History of Vinson and Lynx"; 
// Abstract list of the combined message
List<String> abstactList = new ArrayList<>();
msgs.add("abstract1");
msgs.add("abstract2");
msgs.add("abstract3");
// Combined messages are compatible with text. If SDKs of early versions do not support combined messages, the user will receive a text message with the content `compatibleText`.
String compatibleText = "Please upgrade to the latest version to check the combined message"; 
// Create a combined message
V2TIMMessage mergeMessage = V2TIMManager.getMessageManager().createMergerMessage(msgs, title, abstractList, compatibleText);
// Send the combined message to the user Denny
V2TIMManager.getMessageManager().sendMessage(mergeMessage, "denny", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
			@Override
			public void onProgress(int progress) {}

			@Override
			public void onSuccess(V2TIMMessage v2TIMMessage) {}

			@Override
			public void onError(int code, String desc) {}
	})
```

- **Receiving a combined message**
The recipient receives and parses a combined message:
```java
@Override
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_MERGER) {
		// Get the combined message elements
		V2TIMMergerElem mergerElem = msg.getMergerElem();
		// Get the title
		String title = mergerElem.getTitle();
		// Get the abstract list
		List<String> abstractList = mergerElem.getAbstractList();
		// Download the combined message list when the user clicks the combined message
		mergerElem.downloadMergerMessage(new V2TIMValueCallback<List<V2TIMMessage>>() {
			@Override
			public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
			// Download succeeded. `v2TIMMessages` is the combined message list
			for (V2TIMMessage subMsg : v2TIMMessages) {
				// If the combined message list still contains combined messages, you can continue parsing
				if (subMsg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_MERGER) {
						V2TIMMergerElem mergerElem = subMsg.getMergerElem();
						// Get the title
						String title = mergerElem.getTitle();
						// Get the abstract list
						List<String> abstractList = mergerElem.getAbstractList();
						// Download the combined message list when the user clicks the combined message
						......
					}
				}
			}

			@Override
			public void onError(int code, String desc) {
				// Download failed
			}
		});
}
```

## Read Receipts for Group Messages

When sending a group message, you can set whether a message requires a read receipt. If yes, the receiver can send a read receipt only after the message is read.

>?
- Only available in Enhanced Edition v6.1.2155 or later.
- This feature requires the Flagship Edition package.
- You need to set the group types that support message receipts on the **Feature Configuration** > **Login and Message** > **Group Message Read Receipts** page in the [IM console](https://console.cloud.tencent.com/im).

### The sender specifies that group messages require read receipts

After creating a message, the sender specifies that the message requires a read receipt by using the [needReadReceipt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#aaf238c39e36b61c9390b8f6824e0e4de) field of the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html) and sends the message to the group.

```java
/// API call example
V2TIMMessage v2TIMMessage = V2TIMMessageManagerImpl.getInstance().createTextMessage("Read receipt for group message");
// Specify that the message requires a read receipt
v2TIMMessage.setNeedReadReceipt(true);
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, null, "groupA", V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
                    @Override
                    public void onProgress(int progress) {}

                    @Override
                    public void onError(int code, String desc) {}

                    @Override
                    public void onSuccess(V2TIMMessage v2TIMMessage) {}
                });
```

### The receiver sends the group message read receipt

When receiving a message, the receiver determines whether the message requires a read receipt by using the [needReadReceipt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#a53a9afe71275a00a54f1cb02f0e5eaaa) field of the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html). If a read receipt is required, and the user has read the message, the receiver calls the [sendMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a66ec09cb444ddca989e9518d5118275d) API to send the message read receipt.

```java
/// API call example
/// Assume that the message is read by user
if (!msg.isSelf() && msg.isNeedReadReceipt()) {
  List<V2TIMMessage> messageList = new ArrayList<>();
  messageList.add(msg);
  V2TIMManager.getMessageManager().sendMessageReadReceipts(messageList, new V2TIMCallback() {
    @Override
    public void onSuccess() {
      // Message read receipt sent successfully
    }

    @Override
    public void onError(int code, String desc) {
      // Failed to send the message read receipt
    }
  });
}
```



### The sender listens for notifications of group message read receipts

After the receiver sends a message read receipt, the sender can use the [onRecvMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a000a30bf4b1c26bd32ec9231f54ffd4d) callback of [V2TIMAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html) to listen for the notifications of group message read receipts.

```java
/// API call example
V2TIMManager.getMessageManager().addAdvancedMsgListener(new V2TIMAdvancedMsgListener() {
  @Override
  public void onRecvMessageReadReceipts(List<V2TIMMessageReceipt> receiptList) {
    for (V2TIMMessageReceipt receipt : receiptList) {
      // Unique ID of the message
      String msgID = receipt.getMsgID();
      // Latest message read count
      long readCount = receipt.getReadCount();
      // Latest message unread count
      long unreadCount = receipt.getUnreadCount();
    }
  }
});
```

### The sender proactively pulls group message read receipt information
When the sender enters the message list UI from other UIs, it pulls the message history first and then call the [getMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a50e3bc679e196866057415a7c192abf6) API to pull message read receipt information.

```java
/// API call example
V2TIMManager.getMessageManager().getGroupHistoryMessageList("groupA", 20, null, new V2TIMValueCallback<List<V2TIMMessage>>() {
  @Override
  public void onSuccess(final List<V2TIMMessage> v2TIMMessages) {
    List<V2TIMMessage> receiptMsgs = new ArrayList<>();
    // If the message is sent by you and it requires a read receipt, the message read receipt information needs to be pulled.
    for (V2TIMMessage msg : v2TIMMessages) {
      if (msg.isSelf() && msg.isNeedReadReceipt()) {
        receiptMsgs.add(msg);
      }
    }
    V2TIMManager.getMessageManager().getMessageReadReceipts(receiptMsgs, new V2TIMValueCallback<List<V2TIMMessageReceipt>>() {
      @Override
      public void onSuccess(List<V2TIMMessageReceipt> v2TIMMessageReceipts) {
        Map<String, V2TIMMessageReceipt> messageReceiptMap = new HashMap<>();
        for (V2TIMMessageReceipt receipt : v2TIMMessageReceipts) {
          messageReceiptMap.put(receipt.getMsgID(), receipt);
        }
        for (V2TIMMessage msg : v2TIMMessages) {
          V2TIMMessageReceipt receipt = messageReceiptMap.get(msg.getMsgID());
          if (receipt != null) {
            // Latest message read count
            long readCount = receipt.getReadCount();
            // Latest message unread count
            long unreadCount = receipt.getUnreadCount();
          }
        }
      }

      @Override
      public void onError(int code, String desc) {
        // Failed to pull the message read status
      }
    });
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to pull the message
  }
});
```

### The sender proactively pulls the list of members who have read a group message

The sender can call the [getGroupMessageReadMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a93c48782f3e127e8a50aef1bf8829099) API to pull the list of members who have read a group message in pagination mode.

```java
/// API call example
V2TIMManager.getMessageManager().getGroupMessageReadMemberList(message, V2TIMMessage.V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ, 0, 100, new V2TIMValueCallback<V2TIMGroupMessageReadMemberList>() {
  @Override
  public void onSuccess(V2TIMGroupMessageReadMemberList v2TIMGroupMessageReadMemberList) {
    // `members` is the list of members who have read the message pulled for the current page
    List<V2TIMGroupMemberInfo> members = v2TIMGroupMessageReadMemberList.getMemberInfoList();
    // `nextSeq` indicates the cursor position for the next page pulling
    long nextSeq = v2TIMGroupMessageReadMemberList.getNextSeq();
    // `isFinished` indicates whether the read member list has been fully pulled
    boolean isFinished = v2TIMGroupMessageReadMemberList.isFinished();
    // If the read member list is not fully pulled, continue with the next pulling (here is only the sample code. In pagination pulling mode, the action is recommended to be triggered by UI clicking by user).
    if (!isFinished) {
      V2TIMManager.getMessageManager().getGroupMessageReadMemberList(message, V2TIMMessage.V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ, nextSeq, 100, new V2TIMValueCallback<V2TIMGroupMessageReadMemberList>() {
        @Override
        public void onSuccess(V2TIMGroupMessageReadMemberList v2TIMGroupMessageReadMemberList) {
          // The read member list is pulled successfully
        }

        @Override
        public void onError(int code, String desc) {
          // Failed to pull the read member list
        }
      });
    }
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to pull the read member list
  }
});
```

## Read Receipts for One-to-One Messages

Currently, the one-to-one chat scenario does not support read receipts at the message level. In the scenario, when the receiver calls the [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) API to mark the conversation as read, and the sender will receive a read receipt, indicating that the peer has read the conversation. The read receipt carries the conversation read time of the receiver, and the sender can consider that all messages before this time are read by the peer.

### The receiver marks a conversation as read

 ```
 // Mark messages coming from Haven as read
 V2TIMManager.getMessageManager().markC2CMessageAsRead("haven", new V2TIMCallback() {
	@Override
	public void onError(int code, String desc) {
		// Messages failed to be marked as read
	}
	@Override
	public void onSuccess() {
		// Messages were successfully marked as read
	}
});
 ```

### The sender listens for the notifications of conversation read receipts

The event notification of the conversation read receipt is located in the advanced message listener [V2TIMAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html). To perceive the event, the sender must call [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) to set the listener. Then, the sender can perceive the event through the [onRecvC2CReadReceipt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a25acb98db29da33ae3e3eebab19b655c) callback.

```java
@Override
public void onRecvC2CReadReceipt(List<V2TIMMessageReceipt> receiptList) {
	// The sender may receive multiple read receipts at a time. Therefore, the array callback mode is used here.
	for (V2TIMMessageReceipt v2TIMMessageReceipt : receiptList) {
		// Message recipient
		String userID = v2TIMMessageReceipt.getUserID();
		// Time of the read receipt. A message is considered as read if the timestamp in the chat window is not later than `timestamp` here.
		long timestamp = v2TIMMessageReceipt.getTimest
	}
}
```

## Sending Messages Excluded from the Unread Count

Normally, both one-to-one chat messages and group messages are included in the unread count (you can get the unread count of a conversation via the API [getUnreadCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e) of the conversation object [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html)). If you need to send messages that are excluded from the unread count, such as tips and control messages, send them as follows:

> Only available in Enhanced Edition v5.3.425 or later.

```
// Create the message object
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage(content);
// Set the identifier for excluding from the unread message count
v2TIMMessage.setExcludedFromUnreadCount(true);
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "userA", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null, new V2TIMSendCallback<V2TIMMessage>() {
@Override
public void onError(int code, String desc) {
// The message failed to be sent
}
@Override
public void onSuccess(V2TIMMessage v2TIMMessage) {
// The message was successfully sent
}
@Override
public void onProgress(int progress) {
}
});
```


## Sending Messages Excluded from the Conversation lastMsg

In certain scenarios, if you need to send messages that are excluded from `lastMsg` of a conversation, send them as follows:

> Only available in Enhanced Edition v5.4.666 or later.

```
// Create the message object
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage(content);
// Set the identifier for excluding from lastMsg of the conversation
v2TIMMessage.setExcludedFromLastMessage(true);
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "userA", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null, new V2TIMSendCallback<V2TIMMessage>() {
@Override
public void onError(int code, String desc) {
// The message failed to be sent
}
@Override
public void onSuccess(V2TIMMessage v2TIMMessage) {
// The message was successfully sent
}
@Override
public void onProgress(int progress) {
}
});
```

## Sending Targeted Group Messages

A targeted group message is a message sent only to specified members in a group. You can send it as follows:
```java
// Create an original message object
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage(“This is a targeted group message”);
// Create a targeted group message object, and specify the recipients "Vinson" and "Denny"
List<String> targetGroupMemberList = new ArrayList<>();
targetGroupMemberList.add("vinson");
targetGroupMemberList.add("denny");
V2TIMMessage targetGroupMessage = V2TIMManager.getMessageManager().createTargetedGroupMessage(v2TIMMessage, targetGroupMemberList);

// Send the targeted group message in groupA
V2TIMManager.getMessageManager().sendMessage(targetGroupMessage, null, "groupA",  V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null, new V2TIMSendCallback<V2TIMMessage>() {
    @Override
    public void onError(int code, String desc) {
        // The message fails to be sent.
    }
    @Override
    public void onSuccess(V2TIMMessage v2TIMMessage) {
        // The message was successfully sent
    }
    @Override
    public void onProgress(int progress) {

    }
});
```
>?
>
> Only available in Enhanced Edition v6.0.1975 or later.
>- This feature requires the Flagship Edition package.
>- The original message object for creating a targeted group message cannot be a group @ message.
>- The targeted group message feature is not available for Community and AVChatRoom groups.
>- By default, targeted group messages are excluded from the unread count of the group conversation.

## Setting Offline Push
When the recipient's app is killed, the IM SDK cannot receive new messages through the normal network connection. In this scenario, the offline push service provided by mobile phone manufacturers must be used to notify the recipient of new messages. For more information, see [Offline Push (Android)](https://intl.cloud.tencent.com/document/product/1047/39156).

### Setting the title and content for offline push
When sending messages, you can use the `offlinePushInfo` field in the [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) API to set the title and content for offline push.

```
// Create and send a text message to groupA, and customize the title and content for offline push
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage(content);
V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
// Set the title of the notification bar
v2TIMOfflinePushInfo.setTitle("offline_title");
// Set the content of the notification bar
v2TIMOfflinePushInfo.setDesc("offline_desc");
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, null, "groupA", V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onError(int code, String desc) {
		// The message failed to be sent
	}
	@Override
	public void onSuccess(V2TIMMessage v2TIMMessage) {
		// The message was successfully sent
	}
	@Override
	public void onProgress(int progress) {
	}
});
```

### Clicking a pushed message to go to the corresponding chat window
To implement this feature, the sender needs to set the extended field `ext` of the offline push object `offlinePushInfo` when sending a message. When the recipient opens the app, the recipient can get `ext` by using the method for obtaining custom content provided by the corresponding mobile phone vendor, and then go to the corresponding chat window based on the content of `ext`.

The following example assumes that Denny sends a message to Vinson.
Sender: Denny needs to set `ext` before sending a message.

```
// Denny sets `offlinePushInfo` and specifies `ext` before sending a message
JSONObject jsonObject = new JSONObject();
try{
	jsonObject.put("action", "jump to denny");
} catch (JSONException e) {
	e.printStackTrace();
}
String extContent = jsonObject.toString();
V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
v2TIMOfflinePushInfo.setExt(extContent.getBytes());

V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "vinson", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onError(int code, String desc) {}
	@Override
	public void onSuccess(V2TIMMessage v2TIMMessage) {}
	@Override
	public void onProgress(int progress) {}
});
```
Recipient: although Vinson's app is offline, it can still receive the notification messages pushed offline by the corresponding mobile phone vendor (for example, OPPO). When Vinson clicks the pushed message, the app is started.

```
// After starting the app, Vinson obtains the custom content from the opened `Activity`
Bundle bundle = intent.getExtras();
Set<String> set = bundle.keySet();
if (set != null) {
	for (String key : set) {
		// `key` and `value` correspond to `extKey` and `ext content` set at the sender
		String value = bundle.getString(key);
		if (value.equals("jump to denny")) {
			// Go to the chat window with Denny
			...
		}
	}
}
```

## Setting onlineUserOnly for Message Receiving Only When Users Are Online
In some scenarios, you may want that sent messages can only be received by the recipient when he/she is online, which means the recipient will not be aware of the messages when he/she is offline. For this purpose, you can set `onlineUserOnly` to `true` when calling [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe). After the setting, the messages differ from common messages in the following ways:
- Messages cannot be stored offline, which means the recipient cannot receive messages unless the recipient is online.
- Multi-device roaming of messages is unavailable. This means that messages received on one terminal (read or not) cannot be received on any other terminal.
- Messages cannot be stored locally. That is, these messages cannot be retrieved from the local historical messages in the cloud.


**Typical example: displaying "The other party is typing..."**
In the one-to-one chat scenario, you can call [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send the "I am typing..." message. When the recipient receives this message, "The other party is typing..." is displayed on the UI. The sample code is as follows:
```
// Send the "I am typing..." message to userA
JSONObject jsonObject = new JSONObject();
try{
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

## Setting "Mute Notifications" for Message Receiving
The SDK supports the following types of message receiving options:

- V2TIM_RECEIVE_MESSAGE: Messages will be received when the user is online, and offline push notifications will be received when the user is offline.
- V2TIM_NOT_RECEIVE_MESSAGE: Messages will not be received regardless of the online or offline status.
- V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE: Messages will be received when the user is online, and offline push notifications will not be received when the user is offline.

You can call the [setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6524143895cdee25fabd9aeeae73a3c5) API to set the Mute Notifications option for one-to-one messages and call the [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e) API to set the Mute Notifications option for group messages.

> Only available in Enhanced Edition v5.3.425 or later.

## Recalling Messages

The sender can call the [revokeMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1) API to recall a successfully sent message. By default, the sender can recall a message that is sent within 2 minutes. You can change the time limit for message recall. For detailed operations, see [Message recall settings](https://intl.cloud.tencent.com/document/product/1047/34419).
Message recall requires cooperation of the UI code at the recipient side. When the sender recalls a message, the recipient will receive a message recall notification, [onRecvMessageRevoked](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a13d8197eaba83bfadc7a2f695d671272). This notification contains the `msgID` of the recalled message. Based on this `msgID`, you can identify the message that has been recalled and change the corresponding message bubble to the "Message recalled" state on the UI.

### The sender recalls a message

 ```
V2TIMManager.getMessageManager().revokeMessage(v2TIMMessage, new V2TIMCallback() {
	@Override
	public void onError(int code, String desc) {
		// The message failed to be recalled
	}
	@Override
	public void onSuccess() {
		// The message was successfully recalled
	}
});
 ```

### The recipient learns that the message is recalled

1. Call [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) to set the advanced message listener.
2. Call [onRecvMessageRevoked](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a13d8197eaba83bfadc7a2f695d671272) to receive the message recall notification.

```
@Override
public void onRecvMessageRevoked(String msgID) {
	// msgList is the message list on the current chat interface
	for (V2TIMMessage msg : msgList) {
		if (msg.getMsgID().equals(msgID)) {
				// msg is the recalled message. You need to change the corresponding message bubble state on the UI.
		}
	}
}
```

## Marking Unread Messages as Read
### Marking unread messages in a conversation as read
The recipient can call [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) or [markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69), respectively, to mark incoming messages in a C2C conversation or a group conversation as read, and perform callback of [onConversationChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a4ca1b0c3ec948d9cb76acd6022a1ebf9) to notify the UI to update.
### Quickly marking unread messages of all conversations as read
The recipient can call [markAllMessageAsRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2配置】>【登录与消_1_1V2TIMMessageManager.html#ad097a0da2ea0002f2b0f2d1d11f3a4ab) to quickly mark unread messages of all conversations as read, and perform callback of [onConversationChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a4ca1b0c3ec948d9cb76acd6022a1ebf9) to notify the UI to update.

> Only available in Enhanced Edition v5.8.1668 or later.

## Viewing Historical Messages
You can call [getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#afedccbe0e5229ae15e0e07b722ea39df) to obtain historical messages of one-to-one chats, or call [getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597) to obtain historical messages of group chats. If the network connection of the current device is normal, the IM SDK pulls historical messages from the server by default. If the network connection is unavailable, the IM SDK directly reads historical messages from the local database.

### Pulling historical messages by page
The IM SDK supports the feature of pulling historical messages by page. The number of messages pulled per page cannot be too large; otherwise, the pulling speed is affected. We recommend you pull 20 messages per page.
The following example assumes that historical messages of `groupA` are pulled by page, and the number of messages per page is 20. The sample code is as follows:

```
// The value `null` of `lastMsg` is passed in for the first pulling, indicating that starting from the latest message, a total of 20 messages are pulled
V2TIMManager.getMessageManager().getGroupHistoryMessageList("groupA", 20, null, new V2TIMValueCallback<List<V2TIMMessage>>() {
	@Override
	public void onError(int code, String desc) {
		// Messages failed to be pulled
	}
	@Override
	public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
		// Messages that are pulled by page are listed from new to old by default
		if (v2TIMMessages.size() > 0) {
			// Obtain the start message for the next pulling by page
			V2TIMMessage lastMsg = v2TIMMessages.get(v2TIMMessages.size() - 1);
			// Pull the remaining 20 messages
			V2TIMManager.getMessageManager().getGroupHistoryMessageList("groupA", 20, lastMsg, new V2TIMValueCallback<List<V2TIMMessage>>() {
				@Override
				public void onError(int code, String desc) {
					 // Failed to pull the message
				}

				@Override
				public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
					// Message pulling is completed
				}
			});
		}
	}
});
```

In actual scenarios, pulling by page is often triggered by your swipe operation. Each time when you swipe on the message list, pulling by page is triggered once. However, the principle is similar to the preceding sample code. In either case, `lastMsg` specifies the start message for pulling, and `count` specifies the number of messages pulled each time.

### Precautions
- The storage period of historical messages is as follows:<ul style="margin:0;"><li>Trial edition: free storage for 7 days, no extension supported. </li><li>Pro edition: free storage for 7 days, extension supported. </li><li>Flagship edition: free storage for 30 days, extension supported. </li></ul>It is a value-added service to extend the storage period of historical messages. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. For information about billing, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.
- Only the meeting group (corresponding to the ChatRoom of the earlier version) supports pulling historical messages of members **before they join the group**.
- Messages in an audio-video group (AVChatRoom) do not support local storage and multi-device roaming. Therefore, the [getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597) API does not take effect on an audio-video group.

## Deleting Messages
You can call the [deleteMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adb346fede13d493e415f6574df911e9a) API to delete historical messages. After deletion, historical messages cannot be recovered.

## Setting Message Permissions
### Allowing message sending and receiving only among friends
By default, the IM SDK does not prevent message sending and receiving among strangers. If you wish that one-to-one messages can be sent or received only among friends, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

### Not receiving messages from a specific user
To avoid receiving messages from a specific user, you can blocklist the user or set the Mute Notifications option for messages from the user. After setting the Mute Notifications option, you can change the [Mute Notifications status](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#a90a89f5b4855dad72b784101667998c5).
**Adding a user to the blocklist:**
Call the [addToBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456) API to add the user to the blocklist.
By default, the user will not be aware of this blocking operation, and the messages sent to you will still be displayed as sent successfully (in fact, you will not receive the messages). If you want a user in the blocklist to know that his/her messages are not sent, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message to you.
**Setting "Mute Notifications" for messages from a specified user: **
Call the [setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6524143895cdee25fabd9aeeae73a3c5) API to set the message receiving option to `V2TIM_NOT_RECEIVE_MESSAGE`.

> Only available in Enhanced Edition v5.3.425 or later.

### Rejecting messages from a specified group

For Enhanced Edition v5.3.425 or later, call the [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e) API to set the message receiving option to `V2TIM_NOT_RECEIVE_MESSAGE`.
For SDKs of other versions, call the `setReceiveMessageOpt` API to set the group message receiving option to `V2TIM_GROUP_NOT_RECEIVE_MESSAGE`.



## FAQs
### 1. Why am I receiving duplicate messages?
Check the service logic as follows:
- Check whether [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) is used together with [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823). If yes, when text or custom messages are received, both listeners trigger callback, and consequently duplicate messages are received.
- Check whether the same listener object is added repeatedly. If a listener object is no longer needed, call the corresponding [removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a86ac462d87f652960d2600a52009849a) or [removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93) API to remove this listener.

### 2. Why do the read receipts become invalid after the app is uninstalled and then reinstalled?
In the one-to-one chat scenario, if the recipient calls [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) to mark a message as read, the read receipt received by the sender contains `timestamp`. Based on `timestamp`, the SDK determines whether the other party reads the message. Currently, `timestamp` is stored locally, and will be lost when the app is reinstalled.

### 3. How can I send a message containing multiple `Elem`?
You can call [appendElem](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMElem.html#a5f5d86bb659d7a3775829eaa2e102866) after creating a `Message` object via the `Elem` member of the `Message` object to add the next `Elem` member.
Below is an example of text message + custom message:

```
V2TIMMessage message = V2TIMManager.getMessageManager().createTextMessage("test");
V2TIMCustomElem customElem = new V2TIMCustomElem();
customElem.setData("custom message".getBytes());
message.getTextElem().appendElem(customElem);

```

### 4. How can I parse a message containing multiple `Elem` objects?
1. Use the `Message` object to parse the first `Elem` object.
2. Use the [getNextElem](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMElem.html#aa903ed29cfa12e1ea88873eb1af39d68) method of the first `Elem` object to obtain the next `Elem` object. If the next `Elem` object exists, the `Elem` object instance is returned. Otherwise, `null` is returned.

```
@Override
public void onRecvNewMessage(V2TIMMessage msg) {
	// View the first Elem object
	int elemType = msg.getElemType();
	if (elemType == V2TIMMessage.V2TIM_ELEM_TYPE_TEXT) {
		// Text message
		V2TIMTextElem v2TIMTextElem = msg.getTextElem();
		String text = v2TIMTextElem.getText();
		// Check whether v2TIMTextElem is followed by more Elem objects
		V2TIMElem elem = v2TIMTextElem.getNextElem();
		while (elem != null) {
			// Identify the Elem type. Here, take V2TIMCustomElem as an example.
			if (elem instanceof V2TIMCustomElem) {
				V2TIMCustomElem customElem = (V2TIMCustomElem) elem;
				byte[] data = customElem.getData();
			}
			// Continue to check whether the current Elem is followed by more Elem objects
			elem = elem.getNextElem();
		}
		// If Elem is null, all Elem objects have been parsed.
	}
}
```

[](id:msgAnalyze)
### 5. How are different types of messages parsed?
It is complex to parse a message. We provide the [sample code](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/sampleCode/message.java) for parsing different types of messages. You can copy the code to your project, and perform secondary development based on your actual needs.
