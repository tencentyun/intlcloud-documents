## Feature Description

- The method for sending a message is included in the core class `TencentImSDKPlugin.v2TIMManager.getMessageManager()`.
- It supports sending text, custom, and rich media messages, all of which belong to the `V2TimMessage` type.
- `V2TimMessage` can contain different sub-types to indicate different types of messages.

## Key APIs

The `sendMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) API is the core API for sending a message. It supports sending all types of messages.

> ? The advanced message sending API mentioned below refers to `sendMessage`.

This API is detailed as follows:

```typescript
public sendMessage({
        id,
        receiver,
        groupID,
        onlineUserOnly = false,
        isExcludedFromLastMessage = false,
        isExcludedFromUnreadCount = false,
        needReadReceipt = false,
        offlinePushInfo,
        cloudCustomData,
        localCustomData,
        priority = MessagePriorityEnum.V2TIM_PRIORITY_NORMAL,
    }: {
        id: string;
        receiver: string;
        groupID: string;
        onlineUserOnly?: boolean;
        isExcludedFromUnreadCount?: boolean;
        isExcludedFromLastMessage?: boolean;
        needReadReceipt?: boolean;
        offlinePushInfo?: V2TimOfflinePushInfo;
        cloudCustomData?: string;
        localCustomData?: string;
        priority?: MessagePriorityEnum;
    })
```

Parameters:

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
			<td>Create the message using the `createXxxMessage` API in advance.</td>
   </tr>
   <tr>
      <td>receiver</td>
      <td>`userID` of the one-to-one message receiver.</td>
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
			<td>Set a higher priority for important messages (such as those for red packets and gifts) and a lower priority for frequent and unimportant messages (such as those for likes).</td>
   </tr>
	 <tr>
      <td>onlineUserOnly</td>
      <td>Whether only online users can receive the message.</td>
      <td>YES</td>
      <td>YES</td>
	    <td>If it is set to `true`, the message cannot be pulled by a receiver through historical messages. This is often used to implement weak prompts, such as "The other party is typing..." and unimportant prompts in a group.</td>
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

>? If both `groupID` and `receiver` are set, targeted group messages are sent to `receiver`. For more information, see the Sending a Targeted Group Message section of [Flutter](https://www.tencentcloud.com/document/product/1047/48028).

## Sending Text Messages

Text messages include one-to-one messages and group messages, which are different in terms of APIs and parameters.

The ordinary and advanced APIs can be used to send text messages. The latter supports more sending parameters (such as priority and offline push message).
The ordinary API is as described below, while the advanced API is `sendMessage` mentioned above.

### One-to-one text message

#### Advanced API

Take the following two steps to send a one-to-one text message with the advanced API:

1. Call `createTextMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/createTextMessage.html)) to create a text message.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) to send the message.

Sample code:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

// Create a text message
const createTextMessage = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextMessage("test");
 if(createTextMessage.code == 0){
    String id =  createTextMessage.data.id;

   	// Send the text message
   const sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "userID", groupID: "");
    if(sendMessageRes.code == 0){
      // Message sent successfully
    }
  }
```

### Group text message

#### Advanced API

Take the following two steps to send a group text message with the advanced API:

1. Call `createTextMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/createTextMessage.html)) to create a text message.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) to send the message.

Sample code:

```javascript
// Create a text message
const text = "test";
const atUserList = [];

const createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(text, atUserList);
 if(createTextAtMessageRes.code == 0){
    const id =  createTextAtMessageRes.data.id;

   	// Send the text message
    const sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // Message sent successfully
    }
  }
```

## Sending Custom Messages

Custom messages include one-to-one messages and group messages, which are different in terms of APIs and parameters. Custom messages can be sent with ordinary and advanced APIs.
The advanced API is `sendMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) mentioned above, which supports more sending parameters (such as priority and offline push message) than the ordinary API.

### Custom one-to-one message

#### Advanced API

Take the following two steps to send a custom one-to-one message with the advanced API:

1. Call `createCustomMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/createCustomMessage.html)) to create a custom message.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) to send the message.

Sample code:

```typescript
import { TencentImSDKPlugin } from 'react-native-tim-js';

// Create a custom message
const createCustomMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createCustomMessage(
    data: 'Custom data',
    desc: 'Custom desc',
    extension: 'Custom extension',
  );
  if(createCustomMessageRes.code == 0){
    const id =  createCustomMessageRes.data.id;
    // Send the custom message
    const sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "userID", groupID: "");
    if(sendMessageRes.code == 0){
      // Message sent successfully
    }
  }
```

### Custom group message

#### Advanced API

Take the following two steps to send a custom group message with the advanced API:

1. Call `createCustomMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/createCustomMessage.html)) to create a custom message.
2. Call `sendMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) to send the message.

Sample code:

```typescript
// Create a custom message
import { TencentImSDKPlugin } from 'react-native-tim-js';

// Create a custom message
const createCustomMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createCustomMessage(
    data: 'Custom data',
    desc: 'Custom desc',
    extension: 'Custom extension',
  );
  if(createCustomMessageRes.code == 0){
    const id =  createCustomMessageRes.data.id;
    // Send the custom message
    const sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // Message sent successfully
    }
  }
```

## Sending Rich Media Messages

A rich media message can be sent only with the advanced API in the following steps:

1. Call `createXxxMessage` to create a rich media message object of a specified type, where `Xxx` indicates the specific message type.
2. Call `sendMessage`([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) to send the message.
3. Get the callback for message sending success or failure.

### Image message

To create an image message, you need to get the path of a local image first.
During message sending, the image is uploaded to the server, and the upload progress is called back. The message is sent after the image is uploaded successfully.

Sample code:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

const imagePath = 'The absolute path of the local image';
const createImageMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createImageMessage(imagePath);
  if (createImageMessageRes.code == 0) {
    const id = createImageMessageRes.data.id;
    const sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // Message sent successfully
    }
  }
```

### Audio message

To create an audio message, you need to get the path and audio duration of a local audio file first, where the audio duration is for display on the receiver UI.
During message sending, the audio is uploaded to the server, and the upload progress is called back. The message is sent after the audio is uploaded successfully.

Sample code:

```typescript
import { TencentImSDKPlugin } from 'react-native-tim-js';

const soundPath = 'The absolute path of the local audio file';
const duration = 10; // The audio duration
const createSoundMessageRes =
      await TencentImSDKPlugin.v2TIMManager.getMessageManager().createSoundMessage(
        soundPath,
        duration// The audio duration
      );
  if (createSoundMessageRes.code == 0) {
    const id = createSoundMessageRes.data.id;
    const sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // Message sent successfully
    }
  }
```

### Video message

To create a video message, you need to get the path, video duration, and video thumbnail of a local video file first, where the video duration and thumbnail are for display on the receiver UI.
During message sending, the video is uploaded to the server, and the upload progress is called back. The message is sent after the video is uploaded successfully.

Sample code:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

const videoFilePath = 'The absolute path of the local video file';
const type = "mp4"; // The video type
const duration = 10; // The video duration
const snapshotPath = "The absolute path of the local video thumbnail file";
const createVideoMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createVideoMessage(
            videoFilePath,
            type, // The video type
            duration,// The video duration
            snapshotPath,
          );
  if (createVideoMessageRes.code == 0) {
    const id = createVideoMessageRes.data.id;
    const sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // Message sent successfully
    }
  }
```

### File message

To create a file message, you need to get the path of a local file first.
During message sending, the file is uploaded to the server, and the upload progress is called back. The message is sent after the file is uploaded successfully.

Sample code:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

filePath: "The absolute path of the local file",
const fileName = "Filename";
const createFileMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createFileMessage(
            filePath,
            fileName,
          );
  if (createFileMessageRes.code == 0) {
    const id = createFileMessageRes.data.id;
    const sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // Message sent successfully
    }
  }
```

### Location message

To send a location message, the corresponding latitude and longitude information is sent. This type of message requires a map control for display.

Sample code:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

const desc = "Shennan Boulevard, Nanshan District, Shenzhen"
const longitude = 34;
const latitude = 20;
const createLocationMessage =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createLocationMessage(
            desc,// The location info summary
            longitude,// The longitude
            latitude, // The latitude
          );
  if (createLocationMessage.code == 0) {
    const id = createLocationMessage.data.id;
    const sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // Message sent successfully
    }
  }
```

### Emoji message

To send an emoji message, the corresponding emoji code is sent and then converted into the icon in the receiver.

Sample code:

```javascript
const createFaceMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createFaceMessage(
            0,
            "",
          );
  if (createFaceMessageRes.code == 0) {
    const id = createFaceMessageRes.data.id;
    const sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // Message sent successfully
    }
  }
```
