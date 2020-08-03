## Message Classification
IM messages are classified by destination into two types: one-to-one messages (also called C2C messages) and group messages.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| C2C message | C2CMessage | When sending a C2C message, you must specify the UserID of the message recipient, and only the recipient can receive this message. |
| Group message | GroupMessage | When sending a group message, you must specify the groupID of the target group, and all users in this group can receive this message. |

IM messages can also be classified by content into text messages, custom (signaling) messages, image messages, video messages, voice messages, file messages, location messages, and group tips.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| Text message | TextMessage | This is a common text message. Sensitive words in text messages will be filtered out by the IM service. If a message containing sensitive words is sent, the 80001 error code is returned. |
| Custom message | CustomMessage | This is a section of the binary buffer, which is often used to transfer custom signaling in your app. Its content is not filtered for sensitive words. |
| Image message | ImageElem | When the IM SDK sends an original image, it automatically generates two smaller images of different sizes. The three images are called the original image, large image, and thumbnail. |
| Video message | VideoElem | A video message contains a video file and a thumbnail. |
| Voice message | SoundElem | Voice messages can display a red dot upon playback. |
| File message | FileElem | The maximum size of a file message is 100 MB. |
| Location message | LocationElem | A location message contains three fields: location description, longitude, and latitude. |
| Group tip | GroupTipsElem | A group tip is often used to carry a system notification for a group, such as a notification indicating that a member has joined or quit the group, the group description has been modified, or the profile of a group member has been changed. |

## Sending and Receiving a Simple Message
[V2TIMManager](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html) provides a set of simple APIs for sending and receiving messages. Although these APIs can be used to send or receive text messages and custom (signaling) messages, they are easy to use and only a few minutes are needed to configure access.

### Sending text and signaling messages (simplified APIs)
To send text messages, call [sendC2CTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a59a8ba6e4a973b4c40a09ae7dfdc6981) or [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52). Text messages will be filtered by IM for sensitive words. If a message containing sensitive words is sent, the 80001 error code is returned. To send C2C custom (signaling) messages, call [sendC2CCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af3e08b936df77210c6cdd0ce5c7fa87f) or [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2). A custom message is essentially a section of the binary buffer, which is often used to transfer custom signaling in your app. Its content is not filtered for sensitive words.

### Receiving text and signaling messages (simplified APIs)
To listen to simple text and signaling messages, call [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b). To listen to complex image, video, and voice messages, call [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) defined in [V2TIMMessageManager](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html).

> Do not use [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) together with [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) as this may produce logic bugs.

### Typical example: sending and receiving on-screen comments in a livestreaming group
In the livestreaming scenario, a common way of communicating is to send and receive on-screen comments in a livestreaming group. This can be easily implemented through the simple message APIs.

1. The anchor can call [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) to create a livestreaming group (AVChatRoom) and record the group ID in the list of rooms in the "Broadcasting" state.
2. A viewer can select an anchor that he/she likes and call [joinGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) to join the AVChatRoom created by this anchor.
3. The message sender can call [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52) to send a group text message as an on-screen comment.
4. The message recipients can call [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) to register a simple message listener and use the listener callback function [onRecvGroupTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a1f9eaa4fdc323a8ec375b7068df7b7d4) to obtain text messages.

"FlyHeart" is an instruction. To configure the "FlyHeart" floating heart feature for an AVChatRoom, perform the steps below:
1. Define a custom message type, for example, a JSON string ` { "command": "favor", "value": 101 }`.
2. Call [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2) to send a message and call [onRecvGroupCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a46b48869e411b41c25a98211d951335c) to receive the message.

## Sending and Receiving Rich Media Messages
Image, video, voice, file, and location messages are called rich media messages. Compared with simple messages, it is more complex to send or receive rich media messages.
- Before sending a rich media message, use the `create` function to create a [V2TIMMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html) object. Then, call the corresponding `send` API to send this message.
- When receiving the rich media message, check `elemType` and perform secondary parsing on the `Elem` obtained based on `elemType`.

### Sending Rich Media Messages
The following takes an image message as an example to describe the process of sending a rich media message.
1. The sender calls [createImageMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adef5bc7a67b9a69f70f6417fd810d4b1) to create an image message and obtain the [V2TIMMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html) message object.
2. The sender calls [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send the created message object.

### Receiving Rich Media Messages
1. The recipient calls [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) to set the advanced message listener.
2. The recipient obtains the image message [V2TIMMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html) through the listener callback [onRecvNewMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a6771cfa1a897e24b05c17788aba15ff6).
3. The recipient parses `elemType` in [V2TIMMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html) and performs secondary parsing based on the message type to obtain the content of `Elem` in the message.

### Typical example: sending and receiving image messages
The sender creates and sends an image message.
```
// Create an image message.
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createImageMessage("/sdcard/test.png");
// Send the image message.
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "toUserID", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, true, null,  new V2TIMSendCallback<V2TIMMessage>() {
@Override
public void onError(int code, String desc) {
// The image message failed to be sent.
}
@Override
public void onSuccess(V2TIMMessage v2TIMMessage) {
// The image message is successfully sent.
}
@Override
public void onProgress(int progress) {
// Image upload progress (0-100)
}
});
```

The recipient identifies the image message and parses the message to obtain the original image, large image, and thumbnail contained in the message.
```
@Override
public void onRecvNewMessage(V2TIMMessage msg) {
int elemType = msg.getElemType();
if (elemType == V2TIMMessage.V2TIM_ELEM_TYPE_IMAGE) {
V2TIMImageElem v2TIMImageElem = msg.getImageElem();
// An image message contains an image in three different sizes: original image, large image, and thumbnail. (The SDK automatically generates the large image and thumbnail.)
- A large image is an image obtained after the original image is proportionally compressed. After the compression, the compressed image has a height and width equal to 720 pixels.
- A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the compressed image has a height and width equal to 198 pixels.
List<V2TIMImageElem.V2TIMImage> imageList = v2TIMImageElem.getImageList();
for (V2TIMImageElem.V2TIMImage v2TIMImage : imageList) {
String uuid = v2TIMImage.getUUID(); // Image ID
int imageType = v2TIMImage.getType(); // Image type
int size = v2TIMImage.getSize(); // Image size (bytes)
int width = v2TIMImage.getWidth(); // Image width
int height = v2TIMImage.getHeight(); // Image height
// Set the image download path `imagePath`. Here, `uuid` can be used as an identifier to avoid repeated downloads.
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
// The image failed to be downloaded.
}
@Override
public void onSuccess() {
// The image download is completed.
}
});
} else {
// The image already exists.
}
}  
}
}
```

> For more information on the message parsing sample code, see [FAQs -> 5. How can I parse different types of messages?](#msgAnalyze).

## Setting Offline Push (offlinePushInfo)
When the recipient's app is killed, the IM SDK cannot receive new messages through the normal network connection. In this scenario, the offline push service provided by the mobile phone manufacturer must be used to notify the recipient of new messages. For more information, see [Offline Push (Android)](https://intl.cloud.tencent.com/document/product/1047/34336).

### Setting the title and content for offline push
When sending messages, you can use the **offlinePushInfo** field in the [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) API to set the title and content for offline push.

```
// Create and send a text message to groupA and customize the title and content for offline push.
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage(content);
V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
// Set the title of the notification bar.
v2TIMOfflinePushInfo.setTitle("offline_title");
// Set the content of the notification bar.
v2TIMOfflinePushInfo.setDesc("offline_desc");
// Send a message.
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, null, "groupA", V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
@Override
public void onError(int code, String desc) {
// The message failed to be sent.
}
@Override
public void onSuccess(V2TIMMessage v2TIMMessage) {
// The message is sent successfully.
}
@Override
public void onProgress(int progress) {
}
});
```

### Clicking a pushed message to go to the corresponding chat window
To implement this feature, the sender needs to set `ext`, which is the extended field of the offline push object `offlinePushInfo`, when sending a message. When the recipient opens the app, the recipient can obtain `ext` by using one of the different methods provided by different mobile phone vendors for obtaining custom content, and then go to the corresponding chat window based on the content of `ext`.

The following example assumes that Denny sends a message to Vinson.
Sender: Denny needs to set `ext` before sending a message.

```
// Denny sets `offlinePushInfo` and specifies `ext` before sending a message.
JSONObject jsonObject = new JSONObject();
try {
jsonObject.put("action", "jump to denny");
} catch (JSONException e) {
e.printStackTrace();
}
String extContent = jsonObject.toString();
V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
v2TIMOfflinePushInfo.setExt(extContent.getBytes());

V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "vinson", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
@Override
public void onError(int code, String desc) {}
@Override
public void onSuccess(V2TIMMessage v2TIMMessage) {}
@Override
public void onProgress(int progress) {}
});
```
Recipient: although Vinson's app is not online, it can still receive the notification message pushed offline by the mobile phone vendor’s offline push method (such as OPPO Push). When Vinson clicks the pushed message, the app is started.

```
// After starting the app, Vinson obtains the custom content from the opened `Activity`.
Bundle bundle = intent.getExtras();
Set<String> set = bundle.keySet();
if (set != null) {
for (String key : set) {
// `key` and `value` correspond to `extKey` and `ext content` set at the sender side.
String value = bundle.getString(key);
if (value.equals("jump to denny")) {
// Go to the chat window with Denny.
...
}
}
}
```

## Setting onlineUserOnly so that Messages Can Be Received Only Online
In some scenarios, you may wish that sent messages can only be received by online users. In this case, recipients are not aware of the message when they are offline. For this purpose, you can set `onlineUserOnly` to `true` when calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe). When this parameter is set, the sent messages differ from common messages in the following ways:
- Messages cannot be stored offline. That is, the recipient cannot receive messages unless he/she is online.
- Messages do not support multi-device roaming. That is, if the recipient has received a message on one terminal, this message cannot be received on any other terminal no matter whether it has been read or not.
- Messages cannot be stored locally. That is, these messages cannot be retrieved from historical messages that are stored locally or in cloud.


** Typical example: displaying "The other party is typing..."
In a one-to-one chat scenario, you can call [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send the "I am typing..." message. When the recipient receives this message, "The other party is typing..." is displayed on the UI. The sample code is as follows:
```
// Sending the "I am typing..." message to userA.
JSONObject jsonObject = new JSONObject();
try {
jsonObject.put("command", "textInput");
} catch (JSONException e) {
e.printStackTrace();
}
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createCustomMessage(jsonObject.toString().getBytes());
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "userA", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, true,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
@Override
public void onError(int code, String desc) {}
@Override
public void onSuccess(V2TIMMessage v2TIMMessage) {}
@Override
public void onProgress(int progress) {}
});
```

## Recalling Messages
The sender can call the [revokeMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1) API to recall a successfully sent message. By default, the sender can recall a message that has been sent within 2 minutes. You can change the time limit for message recall. For specific instructions, see [Message recall settings](https://intl.cloud.tencent.com/document/product/1047/34419)。
Message recall requires the support of the UI code at the recipient side. When the sender recalls a message, the recipient will receive a message recall notification, [onRecvMessageRevoked](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a13d8197eaba83bfadc7a2f695d671272). This notification contains the `msgID` of the recalled message. Based on this `msgID`, you can identify the message that has been recalled and change the corresponding message bubble to the "Message recalled" state on the UI.

### The sender recalls a message

 ```
V2TIMManager.getMessageManager().revokeMessage(v2TIMMessage, new V2TIMCallback() {
@Override
public void onError(int code, String desc) {
// The message failed to be recalled.
}
@Override
public void onSuccess() {
// The message is successfully recalled.
}
});
 ```

### The recipient learns that the message is recalled

1. Call [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) to set the advanced message listener.
2. Call [onRecvMessageRevoked](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a13d8197eaba83bfadc7a2f695d671272) to receive the message recall notification.

```
@Override
public void onRecvMessageRevoked(String msgID) {
// `msgList` is the message list on the current chat window.
for (V2TIMMessage msg : msgList) {
if (msg.getMsgID().equals(msgID)) {
// `msg` is the recalled message. You need to change the corresponding message bubble state on the UI.
}
}
}
```


## Adding Read Receipts for Messages
In the one-to-one chat scenario, when the recipient calls the [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) API to mark an incoming message as read, the message sender will receive a read receipt, indicating that the recipient has read his/her message.

> Currently, only C2C messages support the read receipt feature, and group messages do not support this feature. Although the [markGroupMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc) API is also available to group messages, the group message senders currently cannot receive any read receipts.

### The recipient marks messages as read

 ```
 // Mark messages coming from Haven as read.
 V2TIMManager.getMessageManager().markC2CMessageAsRead("haven", new V2TIMCallback() {
@Override
public void onError(int code, String desc) {
// Messages failed to be marked as read.
}
@Override
public void onSuccess() {
// Messages are successfully marked as read.
}
});
 ```

### The sender learns that the messages are read
The event notification for message read receipts is located in the advanced message listener [V2TIMAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html). To enable the sender to learn that a message has been read, call [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) to set the listener. Then, the sender can receive a read receipt from the recipient through the [onRecvC2CReadReceipt](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a25acb98db29da33ae3e3eebab19b655c) callback.

```
@Override
public void onRecvC2CReadReceipt(List<V2TIMMessageReceipt> receiptList) {
// The recipient may receive multiple read receipts at a time. Therefore, the array callback mode is used here.
for (V2TIMMessageReceipt v2TIMMessageReceipt : receiptList) {
// Message recipient
String userID = v2TIMMessageReceipt.getUserID();
// Time of the read receipt. A message is considered as read if the timestamp in the chat window is not later than `timestamp` here.
long timestamp = v2TIMMessageReceipt.getTimest
}
}
```

## Viewing Historical Messages
You can call [getC2CHistoryMessageList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#afedccbe0e5229ae15e0e07b722ea39df) to obtain historical messages of one-to-one chats, or call [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597) to obtain historical messages of group chats. If the network connection of the current device is normal, the IM SDK pulls historical messages from the server by default. If the network connection is unavailable, the IM SDK directly reads historical messages from the local database.

### Pulling historical messages by page
The IM SDK supports pulling historical messages by page. The number of messages pulled per page cannot be too large. Otherwise, the pulling speed will be slow. We recommend that you pull 20 messages per page.
The following example assumes that the historical messages of `groupA` are pulled by page, and the number of messages per page is 20. The sample code is as follows:

```
// The value `null` of `lastMsg` is passed in for the first pull, indicating that a total of 20 messages are pulled starting from the most recent message
V2TIMManager.getMessageManager().getGroupHistoryMessageList("groupA", 20, null, new V2TIMValueCallback<List<V2TIMMessage>>() {
@Override
public void onError(int code, String desc) {
// Messages failed to be pulled.
}
@Override
public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
// Messages pulled by page are listed from new to old by default.
if (v2TIMMessages.size() > 0) {
// Obtain the start message for the next pull by page.
V2TIMMessage lastMsg = v2TIMMessages.get(v2TIMMessages.size() - 1);
// Pull the remaining 20 messages.
V2TIMManager.getMessageManager().getGroupHistoryMessageList("groupA", 20, lastMsg, new V2TIMValueCallback<List<V2TIMMessage>>() {
@Override
public void onError(int code, String desc) {
// Messages failed to be pulled.
}

@Override
public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
// Message pulling is completed.
}
});
}
}
});
```

In actual scenarios, pulling by page is often triggered when the user swipes the interface. Each time the user swipes the message list, pulling by page is triggered once. However, the principle is similar to the preceding sample code. In either case, `lastMsg` specifies the start message for pulling, and `count` specifies the number of messages pulled each time.

### Precautions
- The storage period of historical messages is as follows:<ul style="margin:0;"><li>Trial edition: free storage for 7 days, no extension supported. </li><li>Pro edition: free storage for 7 days, extension supported.</li><li>Flagship edition: free storage for 30 days, extension supported.</li></ul>Extending the storage period of historical messages is a value-added service. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. For more information about billing, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.
- Only the meeting group (corresponding to the ChatRoom of the earlier version) supports pulling the historical messages of members **before members join the group**.
- Messages in the AVChatRoom do not support local storage and multi-device roaming. Therefore, the [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597) API does not work for AVChatRooms.

## Deleting Messages
You can call the [deleteMessageFromLocalStorage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa31e3b48fb666b970120fc0bc6343534) API to delete received messages locally.

### Deleting local messages

```
V2TIMManager.getMessageManager().deleteMessageFromLocalStorage(v2TIMMessage, new V2TIMCallback() {
@Override
public void onError(int code, String desc) {
// Messages failed to be deleted.
}
@Override
public void onSuccess() {
// Messages are deleted successfully.
}
});
```
> Why are the deleted messages pulled again after the app is uninstalled and then reinstalled?
> Currently, IM supports the deletion of local messages only. When the app is reinstalled, as messages still exist in the cloud, historical messages deleted locally can still be pulled from the cloud.

### Deleting messages in the cloud
Currently, IM does not support the deletion of messages in the cloud. If messages in the cloud are deleted, a reverse mapping relationship will be set up in the cloud, affecting the overall performance of the system.

## Setting Message Permissions
### Allowing message sending and receiving only among friends
By default, the IM SDK does not prevent message sending and receiving among strangers. If you want C2C messages to be sent and received only among friends, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** -> **Login and Messages** -> **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

### Blocking messages from a specified user
If you want to block messages from a specified user, call the [addToBlackList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456) API to add this user to the blocklist.
When a user is added to the blocklist, by default, the user does not know that he/she is in the blocklist. That is, after this user sends a message, the prompt still indicates that the message was sent successfully, but in fact, the recipient will not receive the message. If you want a user in the blocklist to know that his/her message failed to be sent, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** -> **Login and Messages** -> **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.

### Blocking messages from a specified group
To block messages from a specified group, you can call the [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6bf8f3eafb5ffcb1d13bd69231de8bd4) API to set the group message receiving option to the `V2TIM_GROUP_NOT_RECEIVE_MESSAGE` state.

## Filtering Sensitive Words
Text messages sent by the IM SDK are filtered by IM for sensitive words. If a sent text message contains sensitive words, the IM SDK will return the 80001 error code.

## FAQs
### 1. Why am I receiving duplicate messages?
Check whether the following logic is correct:
- Check whether [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) is used together with [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823). If yes, when text or custom messages are received, both listeners trigger callback, so duplicate messages are received..
- Check whether the same listener object is added repeatedly. If a listener object is no longer needed, call the corresponding [removeSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a86ac462d87f652960d2600a52009849a) or [removeAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93) API to remove this listener.

### 2. Why are deleted messages pulled again after the app is uninstalled and then reinstalled?
Currently, IM supports the deletion of local messages only. When the app is reinstalled, as messages still exist in the cloud, historical messages deleted locally can still be pulled from the cloud.

### 3. Why do read receipts become invalid after the app is uninstalled and then reinstalled?
In the one-to-one chat scenario, if the recipient calls [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) to mark a message as read, the read receipt received by the sender contains `timestamp`. Based on `timestamp`, the SDK determines whether the other party has read the message. Currently, `timestamp` is stored locally, and will be lost when the app is reinstalled.

### 4. How is a message containing multiple `Elem` objects parsed?
To reduce the message complexity, 2.0 version APIs no longer support the creation of messages containing multiple `Elem` objects. If you receive a message containing multiple `Elem` objects from an earlier version API, perform the steps below:
1. Parse the first `Elem` object as usual.
2. Use the [getNextElem](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMElem.html#aa903ed29cfa12e1ea88873eb1af39d68) method of the first `Elem` object to obtain the next `Elem` object. If the next `Elem` object exists, the `Elem` object instance is returned. Otherwise, `null` is returned.

```
@Override
public void onRecvNewMessage(V2TIMMessage msg) {
// View the first `Elem` object.
int elemType = msg.getElemType();
if (elemType == V2TIMMessage.V2TIM_ELEM_TYPE_TEXT) {
// Text message
V2TIMTextElem v2TIMTextElem = msg.getTextElem();
String text = v2TIMTextElem.getText();
// Check whether `v2TIMTextElem` is followed by more `Elem` objects.
V2TIMElem elem = v2TIMTextElem.getNextElem();
while (elem != null) {
// Identify the Elem type. Here, `V2TIMCustomElem` is used as an example.
if (elem instanceof V2TIMCustomElem) {
V2TIMCustomElem customElem = (V2TIMCustomElem) elem;
byte[] data = customElem.getData();
}
// Continue to check whether the current `Elem` is followed by more `Elem` objects.
elem.getNextElem();
}
// If `elem` is `null`, all `Elem` objects have been parsed.
}
}
```

<span id ="msgAnalyze"></span>
### 5. How are different types of messages parsed?
Message parsing is a complex process. We provide [sample code](https://github.com/tencentyun/TIMSDK/blob/master/Android/tuikit/sampleCode/message.java) for parsing different types of messages. You can copy the code to your project and perform secondary development based on your actual needs.
