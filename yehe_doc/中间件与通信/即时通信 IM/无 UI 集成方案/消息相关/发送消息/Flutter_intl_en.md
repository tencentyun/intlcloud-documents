## Feature Description
* The method for sending a message is in the core class `TencentImSDKPlugin.v2TIMManager.getMessageManager()`.
* It supports sending text, custom, and rich media messages, and all of which belong to the `V2TimMessage` type.
* `V2TimMessage` can contain different sub-types to indicate different types of messages.

## Key API Description
The `sendMessage` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) is one of core APIs for message sending. It supports sending messages of all types.

> ? The advanced message sending API mentioned below refers to `sendMessage`.

The API is as described below:
```dart
Future<V2TimValueCallback<V2TimMessage>> sendMessage(
{
  required String id,
  required String receiver,
  required String groupID,
  int priority = 0,
  bool onlineUserOnly = false,
  bool needReadReceipt = false,
  bool isExcludedFromUnreadCount = false,
  bool isExcludedFromLastMessage = false,
  Map<String, dynamic>? offlinePushInfo,
  String? cloudCustomData,
  String? localCustomData,
}
)
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
      <td>id</td>
      <td>ID returned after message creation</td>
      <td>YES</td>
      <td>YES</td>
			<td>It needs to be first created through the `createXxxMessage` API.</td>
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
      <td>needReadReceipt</td>
      <td>Whether a read receipt is supported for the sent group message</td>
      <td><b>NO</td>
      <td>YES</td>
	    <td>Whether a read receipt is supported for the sent group message</td>
   </tr>
 <tr>
      <td>isExcludedFromUnreadCount</td>
      <td>Whether the sent message is counted as the unread message of the conversation</td>
      <td>YES</td>
      <td>YES</td>
	    <td>If it is set to `true`, the sent message is not counted as the unread message of the conversation. It defaults to `false`.</td>
   </tr>
<tr>
      <td>isExcludedFromLastMessage</td>
      <td>Whether the sent message is included in the `lastMessage` of the conversation</td>
      <td>YES</td>
      <td>YES</td>
	    <td>If it is set to `true`, the sent message is not included in the `lastMessage` of the conversation. It defaults to `false`.</td>
   </tr>
<tr>
      <td>cloudCustomData</td>
      <td>Cloud message data</td>
      <td>YES</td>
      <td>YES</td>
	    <td>Extra data of the message that is stored in the cloud and can be accessed by the receiver.</td>
   </tr>
<tr>
      <td>localCustomData</td>
      <td>Local message data</td>
      <td>YES</td>
      <td>YES</td>
	    <td>Extra data of the message that is stored locally. It cannot be accessed by the receiver and will be lost after the application is uninstalled.</td>
   </tr></dx-tabs>
</table>

>?If both `groupID` and `receiver` are set, targeted group messages are sent to `receiver`. For more information, see [Targeted Group Message](https://intl.cloud.tencent.com/document/product/1047/48028).


## Sending a Text Message
Text messages include one-to-one messages and group messages, which are different in terms of API and parameters.

The ordinary and advanced APIs can be used to send text messages. The latter supports more sending parameters (such as priority and offline push message).
The ordinary API is as described below, while the advanced API is `sendMessage` mentioned above.

### One-to-one text message


#### Advanced API

The advanced API can be called to send a one-to-one text message in two steps:
1. Call `createTextMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createTextMessage.html)) to create a text message.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) to send the message.

Sample code:
```dart
// Create a text message
V2TimValueCallback<V2TimMsgCreateInfoResult> createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(
    text: "test",
    atUserList: [],
  );
 if(createTextAtMessageRes.code == 0){
    String id =  createTextAtMessageRes.data.id;
   	
   	// Send the text message
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "userID", groupID: "");
    if(sendMessageRes.code == 0){
      // The message sent successfully
    }
  }
```



### Group text message


#### Advanced API

The advanced API can be called to send a group text message in two steps:
1. Call `createTextMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createTextMessage.html)) to create a text message.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) to send the message.

Sample code:
```dart
// Create a text message
V2TimValueCallback<V2TimMsgCreateInfoResult> createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(
    text: "test",
    atUserList: [],
  );
 if(createTextAtMessageRes.code == 0){
    String id =  createTextAtMessageRes.data.id;
   	
   	// Send the text message
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // The message sent successfully
    }
  }
```


## Sending a Custom Message

Custom messages include one-to-one messages and group messages, which are different in terms of API and parameters. The ordinary and advanced APIs can be used to send custom messages.
The advanced API is the `sendMessage` mentioned above ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)), which supports more sending parameters (such as priority and offline push message) than the ordinary API.


### Custom one-to-one message


#### Advanced API

The advanced API can be called to send a custom one-to-one message in two steps:
1. Call `createCustomMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html)) to create a custom message.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) to send the message.

Sample code:
```java
// Create a custom message
V2TimValueCallback<V2TimMsgCreateInfoResult> createCustomMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createCustomMessage(
    data: 'Custom data',
    desc: 'Custom desc',
    extension: 'Custom extension',
  );
  if(createCustomMessageRes.code == 0){
    String id =  createCustomMessageRes.data.id;
    // Send the custom message
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "userID", groupID: "");
    if(sendMessageRes.code == 0){
      // The message sent successfully
    }
  }
```



### Custom group message


#### Advanced API

The advanced API can be called to send a custom group message in two steps:
1. Call `createCustomMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html)) to create a custom message.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) to send the message.

Sample code:
```java
// Create a custom message
V2TimValueCallback<V2TimMsgCreateInfoResult> createCustomMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createCustomMessage(
    data: 'Custom data',
    desc: 'Custom desc',
    extension: 'Custom extension',
  );
  if(createCustomMessageRes.code == 0){
    String id =  createCustomMessageRes.data.id;
    // Send the custom message
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // The message sent successfully
    }
  }
```




## Sending a Rich Media Message

A rich media message can be sent only by using the advanced API in the following steps:

1. Call `createXxxMessage` to create a rich media message object of a specified type. Here, `Xxx` indicates the specific message type.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) to send the message.
3. Get the callback for message sending success or failure.

### Image message

To create an image message, you need to get the local image path first.
During message sending, the image is uploaded to the server, and the upload progress is called back. The message is sent after the image is uploaded successfully.

Sample code:
```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createImageMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createImageMessage(
        imagePath: "Absolute path of the local image", 
);
  if (createImageMessageRes.code == 0) {
    String id = createImageMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // The message sent successfully
    }
  }
```


### Audio message

To create an audio message, you need to get the local audio file path and audio duration first, the latter of which can be used for display on the receiver UI.
During message sending, the audio is uploaded to the server, and the upload progress is called back. The message is sent after the audio is uploaded successfully.

Sample code:
```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createSoundMessageRes =
      await TencentImSDKPlugin.v2TIMManager.getMessageManager().createSoundMessage(
        soundPath: "Absolute path of the local audio file",
        duration: 10,// Audio duration
      );
  if (createSoundMessageRes.code == 0) {
    String id = createSoundMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // The message sent successfully
    }
  }
```


### Video message

To create a video message, you need to get the local video file path, video duration, and video thumbnail first, the latter two of which can be used for display on the receiver UI.
During message sending, the video is uploaded to the server, and the upload progress is called back. The message is sent after the video is uploaded successfully.

Sample code:
```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createVideoMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createVideoMessage(
            videoFilePath: "Absolute path of the local video file",
            type: "mp4", // Video type
            duration: 10,// Video duration
            snapshotPath: "Absolute path of the local video thumbnail file",
          );
  if (createVideoMessageRes.code == 0) {
    String id = createVideoMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // The message sent successfully
    }
  }
```



### File message

To create a file message, you need to get the local file path first.
During message sending, the file is uploaded to the server, and the upload progress is called back. The message is sent after the file is uploaded successfully.

Sample code:
```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createFileMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createFileMessage(
            filePath: "Absolute path of the local file",
            fileName: "Filename",
          );
  if (createFileMessageRes.code == 0) {
    String id = createFileMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // The message sent successfully
    }
  }
```



### Location message

Latitude and longitude information is sent in a location message, which requires a map control for display.

Sample code:
```dart
 V2TimValueCallback<V2TimMsgCreateInfoResult> createLocationMessage =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createLocationMessage(
            desc: "Shennan Boulevard, Nanshan District, Shenzhen",// Location information digest
            longitude: 34,// Longitude
            latitude: 20, // Latitude
          );
  if (createLocationMessage.code == 0) {
    String id = createLocationMessage.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // The message sent successfully
    }
  }
```


### Emoji message

Emoji codes are sent in an emoji message and need to be converted into icons by the receiver.

Sample code:
```java
V2TimValueCallback<V2TimMsgCreateInfoResult> createFaceMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createFaceMessage(
            index: 0,
            data: "",
          );
  if (createFaceMessageRes.code == 0) {
    String id = createFaceMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // The message sent successfully
    }
  }
```



